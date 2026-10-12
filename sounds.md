# SiteGPT: Sound library

Companion file to the SiteGPT V12 CatWeb guide (https://raw.githubusercontent.com/Began2/SiteGPT/main/SiteGPT%20V12.md). All pre-uploaded UI sound asset IDs. Section references (§) point to sections of the main guide.

---

## 11. Sound Library

A set of **8 pre-uploaded UI sound assets** for interface feedback. **To use:** play with the audio actions from §5.5 — `Play audio` (id `5`) for one-shots, `Play looped audio` (id `26`) for loops; capture the returned handle in the optional `<var?>` slot, then control it with `Set volume` (id `73`), `Set speed` (id `77`), `Stop audio` (id `74`), `Pause` (id `75`), `Resume` (id `76`), or `Stop all audio` (id `7`).

**Durations shown are nominal — several read as `0:00` because the clip is under a second, not because it is empty.** Do not treat a `0:00` sound as faulty.

**Concurrent-sound limit is 150 (§8).** For rapid-fire feedback (e.g. a click on every keystroke), reuse a single handle and restart it rather than spawning a new sound each time.

| # | Name | Asset ID | Nominal length | Intended use |
|---|---|---|---|---|
| 1 | `click` | `88442833509532` | 0:00 | Primary button / tap feedback (simple UI click) |
| 2 | `hover` | `107511012621133` | 0:00 | Subtle tick on mouse-enter for interactive elements |
| 3 | `toggle` | `94316899429786` | 0:00 | Switch / checkbox on-off |
| 4 | `success` | `136211732441165` | 0:02 | Confirmation / completed action (positive chime) |
| 5 | `error` | `131661013076677` | 0:00 | Invalid input / failed action (soft buzz) |
| 6 | `notification` | `131039887376992` | 0:00 | Incoming message / alert |
| 7 | `send` | `5485567028` | 0:00 | Message / form submit (outgoing) |
| 8 | `transition` | `119137729729534` | 0:01 | Page / view change (whoosh) |

**Play-sound example (with the §5.1a `()` convention):**
```json
{"id":"5","text":["Play audio (88442833509532)",{"value":"88442833509532","t":"string","assetbrowser":"audio","l":"id"},"→ (o!20)",{"value":"o!20","t":"string","l":"variable?"}],"globalid":"p1"}
```

Wire these to the natural events: `click`/`toggle` on `When <button> pressed` (id `1`), `hover` on `When mouse enters` (id `3`), `success`/`error` after a form's `When <input> submitted` (id `8`) branch, `notification` on `When message received` (id `9`), `send` on submit, `transition` before a `Redirect` (id `4`) or a view swap. **These are the only confirmed pre-uploaded sound IDs — never invent additional sound asset IDs; flag any other sound the user needs.**
