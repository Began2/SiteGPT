# SiteGPT: Datastore

Companion file to the SiteGPT V12 CatWeb guide (https://raw.githubusercontent.com/Began2/SiteGPT/main/SiteGPT%20V12.md). How to save data and share it between users with a relay account. Section references (§) point to sections of the main guide.

---

### 5.10 Persistent / cross-user data — the relay-account datastore (advanced)

CatWeb has **no global or server-side storage**: variables and tables are per-visitor and die on refresh. To persist data, or share it *between* users, you simulate a backend with an **always-online alt account** parked on one fixed page (e.g. `api.<site>.rbx`) acting as a relay server. Generate both sides of this; only offer it when the site actually needs saved/shared state (leaderboards, counters, saves, live presence).

**Prerequisite the AI cannot supply — state it plainly to the user:** they must run a Roblox account 24/7 without disconnecting, sitting on that page. Without it there is no datastore.

- **Store = the alt's cookies** (`34` set, `36` get, `35` increment, `62` delete) — persistent, **~10KB total**. Never use variables/tables as the store: they are volatile, so one crash or update and the data is gone.
- **Transport = broadcasts.** `Broadcast <msg> across page` (`32`) both directions; the alt listens with `When message received` (`9`), which exposes `{messageContent}`, `{messageSenderName}`, `{messageSenderId}`. **Broadcast cap is 979 bytes (§8)** — chunk anything larger.
- **Protocol:** tag every message with a one-char op code so each side can route it — `G` get, `P` post, `R` reply, `H` heartbeat. Format `<op>|<key>|<value>`.

**Broadcasts are a real message channel, so `{messageContent}` genuinely does pass through the filter** — unlike static page copy, this is the case the filter is actually built for, and it will tag payloads. **Design the protocol around it: keep keys and values numeric wherever possible** (`P|7|500`), since digits and spaces don't tag. Op codes (`G`/`P`/`R`/`H`) and the `|` separator are structural framing and stay raw. Usernames never need to travel in the payload, because the alt reads `{messageSenderName}` from the event. **Do not route user-entered text through the decoder to get it past the filter.** Broadcasts are exactly what the filter exists to check, so keep the datastore to numeric data.

**POST** (client saves): client broadcasts `P|<key>|<value>` with a numeric key, e.g. `P|7|500`. Alt on `When message received` splits `{messageContent}` by `|`; if op `P`, sets cookie `{messageSenderName}_<key>` to `<value>`.
**GET** (client reads): client broadcasts `G|<key>`, e.g. `G|7`. Alt reads cookie `{messageSenderName}_<key>` (`36`) and replies `Broadcast R|<key>|<value>` (`32`). The client's own `When message received` filters for the `R` prefix and updates its UI.
**Online check** — pick one: **pull** (client sends `H`, starts a timer, marks offline if no `H` reply in ~5s) or **push heartbeat** (alt broadcasts `H` every ~3s; client marks offline if none heard in ~5s — cheaper on request volume).

**Security — mandatory, not optional.** Broadcasts are visible to **every** visitor on the page, so any user can forge any request. The alt MUST (a) key all data by `{messageSenderName}` and **never trust a username carried inside the payload**, and (b) drop malformed / oversized messages. Concurrent POSTs to one key are last-write-wins — keep keys per-user to avoid clobbering.

**Server-side POST handler, built from ordinary actions already in §5.5 — no new JSON shape needed.** On the alt's `When message received` (`9`): `Split` (`57`) `{messageContent}` by `|` into a table; `Get entry` (`56`) 1 → `{30}` (op); branch with `If {30} is equal to "P"` (`18`); inside the branch, `Get entry` 2 → `{31}` (key) and `Get entry` 3 → `{32}` (value); then `Set <cookie>` (`34`) where the cookie name is `{messageSenderName}_{31}` and the value is `{32}`; close with `end` (`25`). Seven actions, all ordinary. The only trick is building the cookie name from a concatenated `{var}_{var}` reference instead of a literal.

The GET handler is the same skeleton: branch `{30} == "G"`, `Get cookie` (`36`) `{messageSenderName}_{31}` → `{33}`, then `Broadcast` (`32`) `R|{31}|{33}`. The client mirrors it with its own `When message received` filtering for the `R` prefix and updating its UI from the parsed value.
