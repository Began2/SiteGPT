# SiteGPT: Scripts reference

Companion file to the SiteGPT V12 CatWeb guide (https://raw.githubusercontent.com/Began2/SiteGPT/main/SiteGPT%20V12.md). Every event and action with its exact shape, plus complete worked scripts. Section references (§) point to the main guide, except §5.8a and §5.9, which are in this file.

---

## Full block reference (§5.5)

**Transcribed verbatim from CatWeb's own block-palette export: 16 events, 131 actions (three of them deprecated). That is the entire vocabulary. Never emit an `id` that is not in these tables.** Event and action ids overlap; see the overlap table in §5.5 of the main guide.

**How to read the shape column.** `{t:object}` is shorthand for the parameter object `{"value":"<yours>","t":"object"}` — you supply `value`, and copy `t` / `l` / `assetbrowser` / `href` **exactly as shown, adding nothing and dropping nothing**. Quoted segments are fixed literal text; the only change allowed is appending a `(value)` annotation (§5.1a). Never add or remove a segment. A `?` inside an `l` (e.g. `variable?`) is literal — keep it. Output slots after `→` still take a real `value` (or `""` when you don't capture the result).

**Events — only these may be a top-level `content` entry.**

| `id` | Event | Exact `text` array |
|---|---|---|
| `0` | When website loaded | `["When website loaded..."]` |
| `1` | When button pressed | `["When", {t:object,l:button}, "pressed..."]` |
| `2` | When key pressed | `["When", {t:key}, "pressed..."]` |
| `3` | When mouse enters | `["When mouse enters", {t:object}, "..."]` |
| `5` | When mouse leaves | `["When mouse leaves", {t:object}, "..."]` |
| `6` | Define function | `["Define function", {t:string,l:function}]` |
| `7` | When avataritem bought | `["When", {t:object,l:avataritem}, "bought..."]` |
| `8` | When input submitted | `["When", {t:object,l:input}, "submitted..."]` |
| `9` | When message received | `["When message received..."]` |
| `10` | When object changed | `["When", {t:object}, "changed..."]` |
| `11` | When mouse down on | `["When mouse down on", {t:object,l:button}, "..."]` |
| `12` | When mouse up on | `["When mouse up on", {t:object,l:button}, "..."]` |
| `13` | When button right clicked | `["When", {t:object,l:button}, "right clicked..."]` |
| `14` | When cross-site message received | `["When cross-site message received..."]` |
| `15` | When donation completed | `["When donation completed..."]` |
| `16` | When any key pressed | `["When any key pressed..."]` |

**Actions — control flow & conditionals**

| `id` | Action | Exact `text` array |
|---|---|---|
| `18` | If equal | `["If", {t:string,l:any}, "is equal to", {t:string,l:any}]` |
| `19` | If not equal | `["If", {t:string,l:any}, "is not equal to", {t:string,l:any}]` |
| `20` | If greater | `["If", {t:string,l:any}, "is greater than", {t:string,l:any}]` |
| `125` | If greater or equal | `["If", {t:string,l:any}, "is greater or equal to", {t:string,l:any}]` |
| `21` | If lower | `["If", {t:string,l:any}, "is lower than", {t:string,l:any}]` |
| `126` | If lower or equal | `["If", {t:string,l:any}, "is lower or equal to", {t:string,l:any}]` |
| `37` | If contains | `["If", {t:string}, "contains", {t:string}]` |
| `38` | If doesn't contain | `["If", {t:string}, "doesn't contain", {t:string}]` |
| `92` | If exists | `["If", {t:string,l:variable}, "exists"]` |
| `93` | If doesn't exist | `["If", {t:string,l:variable}, "doesn't exist"]` |
| `44` | If AND | `["If", {t:string,l:variable}, "AND", {t:string,l:variable}]` |
| `45` | If OR | `["If", {t:string,l:variable}, "OR", {t:string,l:variable}]` |
| `46` | If NOR | `["If", {t:string,l:variable}, "NOR", {t:string,l:variable}]` |
| `47` | If XOR | `["If", {t:string,l:variable}, "XOR", {t:string,l:variable}]` |
| `79` | If left mouse down | `["If left mouse button down"]` |
| `80` | If middle mouse down | `["If middle mouse button down"]` |
| `81` | If right mouse down | `["If right mouse button down"]` |
| `82` | If key down | `["If", {t:key}, "down"]` |
| `108` | If dark theme | `["If dark theme enabled"]` |
| `103` | If is ancestor | `["If", {t:object}, "is ancestor of", {t:object}]` |
| `104` | If is child | `["If", {t:object}, "is child of", {t:object}]` |
| `105` | If is descendant | `["If", {t:object}, "is descendant of", {t:object}]` |
| `112` | else | `["else"]` |
| `25` | end | `["end"]` |
| `22` | Repeat n times | `["Repeat", {t:number}, "times"]` |
| `23` | Repeat forever | `["Repeat forever"]` |
| `24` | Break | `["Break"]` |

**Actions — logging & timing**

| `id` | Action | Exact `text` array |
|---|---|---|
| `0` | Log | `["Log", {t:any}]` |
| `1` | Warn | `["Warn", {t:any}]` |
| `2` | Error | `["Error", {t:any}]` |
| `3` | Wait | `["Wait", {t:number}, "seconds"]` |

**Actions — variables & math**

| `id` | Action | Exact `text` array |
|---|---|---|
| `11` | Set variable | `["Set", {t:string,l:variable}, "to", {t:string,l:any}]` |
| `96` | Delete variable | `["Delete", {t:string,l:variable}]` |
| `12` | Increase | `["Increase", {t:string,l:variable}, "by", {t:number}]` |
| `13` | Decrease | `["Decrease", {t:string,l:variable}, "by", {t:number}]` |
| `14` | Multiply | `["Multiply", {t:string,l:variable}, "by", {t:number}]` |
| `15` | Divide | `["Divide", {t:string,l:variable}, "by", {t:number}]` |
| `40` | Power | `["Raise", {t:string,l:variable}, "to the power of", {t:number}]` |
| `41` | Modulo | `[{t:string,l:variable}, "modulo", {t:number}]` |
| `16` | Round | `["Round", {t:string,l:variable}]` |
| `17` | Floor | `["Floor", {t:string,l:variable}]` |
| `78` | Ceil | `["Ceil", {t:string,l:variable}]` |
| `27` | Set to random | `["Set", {t:string,l:var}, "to random", {t:number,l:n}, "-", {t:number,l:n}]` |
| `114` | Run math function | `["Run math function", {t:string,l:function}, {t:tuple}, "→", {t:string,l:variable}]` |

**Actions — strings**

| `id` | Action | Exact `text` array |
|---|---|---|
| `42` | Substring | `["Sub", {t:string,l:variable}, {t:number,l:start}, "-", {t:number,l:end}]` |
| `43` | Replace | `["Replace", {t:string}, "in", {t:string,l:variable}, "by", {t:string}]` |
| `48` | Get string length | `["Get length of", {t:string}, "→", {t:string,l:variable}]` |
| `57` | Split | `["Split", {t:string}, {t:string,l:separator}, "→", {t:string,l:table}]` |
| `69` | Lowercase | `["Lower", {t:string}, "→", {t:string,l:variable}]` |
| `70` | Uppercase | `["Upper", {t:string}, "→", {t:string,l:variable}]` |
| `109` | Concatenate | `["Concatenate", {t:string}, "with", {t:string}, "→", {t:string,l:variable}]` |

**Actions — tables & arrays**

| `id` | Action | Exact `text` array |
|---|---|---|
| `54` | Create table | `["Create table", {t:string,l:table}]` |
| `55` | Set entry (value) | `["Set entry", {t:string,l:entry}, "of", {t:string,l:table}, "to", {t:string,l:any}]` |
| `66` | Set entry (object) | `["Set entry", {t:string,l:entry}, "of", {t:string,l:table}, "to", {t:object}]` |
| `131` | Set entry (function) | `["Set entry", {t:string,l:entry}, "of", {t:string,l:table}, "to", {t:string,l:function}]` |
| `56` | Get entry | `["Get entry", {t:string,l:entry}, "of", {t:string,l:table}, "→", {t:string,l:variable}]` |
| `90` | Delete entry | `["Delete entry", {t:string,l:entry}, "of", {t:string,l:table}]` |
| `89` | Insert at position | `["Insert", {t:string,l:any}, "at position", {t:number,l:number?}, "of", {t:string,l:array}]` |
| `91` | Remove at position | `["Remove entry at position", {t:number,l:number?}, "of", {t:string,l:array}]` |
| `59` | Get array length | `["Get length of", {t:string,l:array}, "→", {t:string,l:variable}]` |
| `113` | Iterate through | `["Iterate through", {t:string,l:table}, "({l!index},{l!value})"]` |
| `110` | Join array | `["Join", {t:string,l:array}, "using", {t:string,l:string}, "→", {t:string,l:variable}]` |

**Actions — objects & display**

| `id` | Action | Exact `text` array |
|---|---|---|
| `8` | Make invisible | `["Make", {t:object}, "invisible"]` |
| `9` | Make visible | `["Make", {t:object}, "visible"]` |
| `10` | Set text | `["Set", {t:object}, "text to", {t:string}]` |
| `106` | Set image | `["Set", {t:object}, "image to", {t:id,assetbrowser:image}]` |
| `107` | Set avatar image | `["Set", {t:object}, "image to avatar of", {t:number,l:userid}, {t:string,l:resolution?}]` |
| `31` | Set property | `["Set", {t:string,l:property}, "of", {t:object}, "to", {t:any}]` |
| `39` | Get property | `["Get", {t:string,l:property}, "of", {t:object}, "→", {t:string,l:variable}]` |
| `88` | Tween | `["Tween", {t:string,l:property}, "of", {t:object}, "to", {t:any}, "-", {t:number,l:time}, {t:string,l:style}, {t:string,l:direction}]` |
| `30` | Get text from input | `["Get text from", {t:object,l:input}, "→", {t:string,l:variable}]` |
| `49` | Duplicate | `["Duplicate", {t:object}, "→", {t:string,l:variable}]` |
| `50` | Delete object | `["Delete", {t:object}]` |
| `127` | Get objects at position | `["Get objects at position", {t:string,l:x}, {t:string,l:y}, "→", {t:string,l:array}]` |
| `129` | Get asset info | `["Get", {t:string,l:info}, "of asset", {t:string,l:id}, "→", {t:string,l:variable}]` |
| `138` | Set attribute | `["Set", {t:string,l:attribute}, "of", {t:object}, "to", {t:any,l:any?}]` |
| `139` | Get attribute | `["Get", {t:string,l:attribute}, "of", {t:object}, "→", {t:string,l:variable}]` |
| `140` | Get all attributes | `["Get all attributes of", {t:object}, "→", {t:string,l:table}]` |

**Actions — hierarchy**

| `id` | Action | Exact `text` array |
|---|---|---|
| `58` | Parent object | `["Parent", {t:object}, "under", {t:object}]` |
| `97` | Get parent | `["Get parent of", {t:object}, "→", {t:string,l:variable}]` |
| `99` | Find child | `["Find child named", {t:string}, "in", {t:object}, "→", {t:string,l:variable}]` |
| `98` | Find ancestor | `["Find ancestor named", {t:string}, "in", {t:object}, "→", {t:string,l:variable}]` |
| `100` | Find descendant | `["Find descendant named", {t:string}, "in", {t:object}, "→", {t:string,l:variable}]` |
| `101` | Get children | `["Get children of", {t:object}, "→", {t:string,l:table}]` |
| `102` | Get descendants | `["Get descendants of", {t:object}, "→", {t:string,l:table}]` |

**Actions — audio**

| `id` | Action | Exact `text` array |
|---|---|---|
| `5` | Play audio | `["Play audio", {t:string,l:id,assetbrowser:audio}, "→", {t:string,l:variable?}]` |
| `26` | Play looped audio | `["Play looped audio", {t:string,l:id,assetbrowser:audio}, "→", {t:string,l:variable?}]` |
| `73` | Set volume | `["Set volume of", {t:string,l:variable}, "to", {t:number}]` |
| `77` | Set speed | `["Set speed of", {t:string,l:variable}, "to", {t:number}]` |
| `74` | Stop audio | `["Stop audio", {t:string,l:variable}]` |
| `75` | Pause audio | `["Pause audio", {t:string,l:variable}]` |
| `76` | Resume audio | `["Resume audio", {t:string,l:variable}]` |
| `7` | Stop all audio | `["Stop all audio"]` |
| `94` | Set audio property | `["Set", {t:string,l:property}, "of", {t:string,l:variable}, "to", {t:any}]` |
| `95` | Get audio property | `["Get", {t:string,l:property}, "of", {t:string,l:variable}, "→", {t:string,l:variable}]` |

**Actions — input & viewport**

| `id` | Action | Exact `text` array |
|---|---|---|
| `84` | Get viewport size | `["Get viewport size →", {t:string,l:x}, {t:string,l:y}]` |
| `85` | Get cursor position | `["Get cursor position →", {t:string,l:x}, {t:string,l:y}]` |
| `135` | Set mouse icon | `["Set mouse icon to", {t:id,assetbrowser:image,l:id?}]` |
| `136` | Hide mouse cursor | `["Hide mouse cursor"]` |
| `137` | Show mouse cursor | `["Show mouse cursor"]` |

The mouse actions only affect desktop visitors. For a cursor that only changes while hovering one element, set that element's `mouse_icon` key (§2.1) instead; no script needed. Use an icon-sized image (the §10 icons work) for a custom cursor, and always pair `Hide mouse cursor` with a way to show it again.

**Actions — navigation & url**

| `id` | Action | Exact `text` array |
|---|---|---|
| `4` | Redirect to | `["Redirect to", {t:string,href:true}]` |
| `117` | Get URL | `["Get URL →", {t:string,l:variable}]` |
| `67` | Get query parameter | `["Get query string parameter", {t:string}, "→", {t:string,l:variable}]` |

**Actions — broadcast & user**

| `id` | Action | Exact `text` array |
|---|---|---|
| `32` | Broadcast page | `["Broadcast", {t:string,l:message}, "across page"]` |
| `33` | Broadcast site | `["Broadcast", {t:string,l:message}, "across site"]` |
| `130` | Broadcast cross-site | `["Broadcast", {t:string,l:message}, "cross-site to", {t:string,l:page,href:true}]` |
| `51` | Get username | `["Get local username →", {t:string,l:variable}]` |
| `53` | Get display name | `["Get local display name →", {t:string,l:variable}]` |
| `52` | Get user ID | `["Get local user ID →", {t:string,l:variable}]` |

**Actions — cookies**

| `id` | Action | Exact `text` array |
|---|---|---|
| `34` | Set cookie | `["Set", {t:string,l:cookie}, "to", {t:any}]` |
| `35` | Increase cookie | `["Increase", {t:string,l:cookie}, "by", {t:number}]` |
| `62` | Delete cookie | `["Delete cookie", {t:string,l:cookie}]` |
| `36` | Get cookie | `["Get cookie", {t:string,l:cookie}, "→", {t:string,l:variable}]` |

**Actions — time & date**

| `id` | Action | Exact `text` array |
|---|---|---|
| `68` | Get unix timestamp | `["Get unix timestamp →", {t:string,l:variable}]` |
| `116` | Get server unix timestamp | `["Get server unix timestamp →", {t:string,l:variable}]` |
| `83` | Get tick | `["Get tick →", {t:string,l:variable}]` |
| `118` | Get timezone | `["Get timezone →", {t:string,l:variable}]` |
| `71` | Format current date | `["Format current date/time", {t:string,l:format}, "→", {t:string,l:variable}]` |
| `72` | Format from unix | `["Format from unix", {t:number}, {t:string,l:format}, "→", {t:string,l:variable}]` |

**Actions — color**

| `id` | Action | Exact `text` array |
|---|---|---|
| `119` | Hex to RGB | `["Convert", {t:string,l:hex}, "to RGB →", {t:string,l:variable}]` |
| `120` | Hex to HSV | `["Convert", {t:string,l:hex}, "to HSV →", {t:string,l:variable}]` |
| `121` | RGB to hex | `["Convert", {t:string,l:RGB}, "to hex →", {t:string,l:variable}]` |
| `122` | HSV to hex | `["Convert", {t:string,l:HSV}, "to hex →", {t:string,l:variable}]` |
| `123` | Lerp color | `["Lerp", {t:string,l:hex}, "to", {t:string,l:hex}, "by", {t:number,l:alpha}, "→", {t:string,l:variable}]` |

**Actions — functions**

| `id` | Action | Exact `text` array |
|---|---|---|
| `132` | Run function | `["Run function", {t:string,l:function}, {t:tuple}, "→", {t:string,l:variable?}]` |
| `133` | Run in background | `["Run function in background", {t:string,l:function}, {t:tuple}]` |
| `134` | Run function protected | `["Run function protected", {t:string,l:function}, {t:tuple}, "→", {t:string,l:success_variable?}, {t:string,l:variable?}]` |
| `115` | Return | `["Return", {t:string,l:any}]` |

**Deprecated: `87` Run function, `63` Run in background, `128` Run function protected.** They have the same text arrays as `132`/`133`/`134`, but only warn when the function doesn't exist, while the new ids raise an error. Always write `132`/`133`/`134`. When checking older JSON, flag `87`/`63`/`128` as deprecated; they still run, so it isn't an import error.

---

### 5.8a `Run math function` (id `114`) — confirmed shape and worked example

This is the single most-guessed action in the whole vocabulary — it has no example anywhere in earlier versions of this guide, so every generation invented a slightly different, unpublishable layout. **Confirmed text-array shape, transcribed verbatim from CatWeb's own block-palette export:**

```
["Run math function", {"t":"string","l":"function"}, {"t":"tuple"}, "→", {"t":"string","l":"variable"}]
```

Read the shape carefully — it differs from `Run function` (id `132`) in two ways that are easy to miss:
- **No literal text segment between the function-name param and the tuple param.** The function name and its argument tuple sit back-to-back in the array — there is no `"with"` or similar connector string.
- **The output variable is not optional** — `"l":"variable"`, no `?`. `Run function` (id `132`) uses `"l":"variable?"` because a function may not return; a math function always produces a value.

**Worked example — square root of a variable, with the `()` convention (the empty/non-empty tuple rule applies here too):**

```json
{"id":"114","text":["Run math function (sqrt)",{"value":"sqrt","t":"string","l":"function"},{"value":[{"value":"{40}","t":"string","l":"any"}],"t":"tuple"},"→ (41)",{"value":"41","t":"string","l":"variable"}],"globalid":"m1"}
```

This reads: run the Luau `math.sqrt` function with the single argument `{40}`, store the result in `{41}`. The one confirmed function name (from the CatWeb wiki's own description of this block) is `abs`; `sqrt` above follows the identical pattern for a different Luau `math.*` name. **Only pass function names that exist in Luau's `math` library** (`abs`, `sqrt`, `sin`, `cos`, `floor`, `ceil`, `min`, `max`, etc.) — for a two-argument function like `min`/`max`, add a second entry to the tuple's `value` array, e.g. `{"value":[{"value":"{40}","t":"string","l":"any"},{"value":"{41}","t":"string","l":"any"}],"t":"tuple"}`. `Round`/`Floor`/`Ceil` already have their own dedicated single-purpose ids (`16`/`17`/`78`) — prefer those over routing the same operation through `Run math function`.

### 5.9 Worked Complete Scripts (study these end-to-end)

Real scripting fails at the **seams** — how events, functions, conditionals, and variable reads fit into one valid `content` array. These are complete and import-valid.

**5.9a — Counter button** (event + variable + conditional + Set text). Flat If→body→end; mutable `Increase`.

```json
{
  "class": "script", "globalid": "sc1", "alias": "logic1", "enabled": "true",
  "content": [
    {"id":"0","text":["When website loaded..."],"globalid":"e0","x":"4900","y":"4900","width":"340",
      "actions":[
        {"id":"11","text":["Set (40)",{"value":"40","t":"string","l":"variable"},"to (0)",{"value":"0","t":"string","l":"any"}],"globalid":"a1"},
        {"id":"10","text":["Set (lbl)",{"value":"lbl","t":"object"},"text to ({40})",{"value":"{40}","t":"string"}],"globalid":"a2"}
      ]},
    {"id":"1","text":["When (btn)",{"value":"btn","t":"object","l":"button"},"pressed..."],"globalid":"e1","x":"4900","y":"5050","width":"340",
      "actions":[
        {"id":"12","text":["Increase (40)",{"value":"40","t":"string","l":"variable"},"by (1)",{"value":"1","t":"number"}],"globalid":"b1"},
        {"id":"20","text":["If ({40})",{"value":"{40}","t":"string","l":"any"},"is greater than (4)",{"value":"4","t":"string","l":"any"}],"globalid":"b2"},
        {"id":"11","text":["Set (40)",{"value":"40","t":"string","l":"variable"},"to (0)",{"value":"0","t":"string","l":"any"}],"globalid":"b3"},
        {"id":"25","text":["end"],"globalid":"b4"},
        {"id":"10","text":["Set (lbl)",{"value":"lbl","t":"object"},"text to ({40})",{"value":"{40}","t":"string"}],"globalid":"b5"}
      ]}
  ]
}
```

Note every `Set <var> to <any>` (id `11`) and both operands of `If greater than` (id `20`) use `{"t":"string","l":"any"}` — never bare `{"t":"any"}` (§5.4a).

**5.9b — Reusable function with the global-passing pattern** (Define function + Run function + a global set by the caller, §5.3a).

```json
{
  "class": "script", "globalid": "sc2", "alias": "logic2", "enabled": "true",
  "content": [
    {"id":"6","text":["Define function (showmsg)",{"value":"showmsg","t":"string","l":"function"}],"globalid":"f1","x":"5200","y":"4900","width":"360",
      "actions":[
        {"id":"10","text":["Set (st)",{"value":"st","t":"object"},"text to ({60})",{"value":"{60}","t":"string"}],"globalid":"g1"},
        {"id":"9","text":["Make (st)",{"value":"st","t":"object"},"visible"],"globalid":"g2"}
      ]},
    {"id":"1","text":["When (sv)",{"value":"sv","t":"object","l":"button"},"pressed..."],"globalid":"e1","x":"4900","y":"5050","width":"340",
      "actions":[
        {"id":"11","text":["Set (60)",{"value":"60","t":"string","l":"variable"},"to (Saved)",{"value":"Saved","t":"string","l":"any"}],"globalid":"h1"},
        {"id":"132","text":["Run function (showmsg)",{"value":"showmsg","t":"string","l":"function"},{"value":[],"t":"tuple"},"→",{"value":"","t":"string","l":"variable?"}],"globalid":"h2"}
      ]}
  ]
}
```

The caller sets global `{60}` immediately before `Run function`, and the body reads `{60}` directly. There is no `variable_overrides` and the tuple is an explicit empty array.

**5.9c — Iterate a table to build rows, with a guard** (Split id 57 + Iterate id 113 + Find child id 99 + existence guard). Note the **two `end`s**: inner closes the `If`, outer closes the `Iterate`.

```json
{
  "class": "script", "globalid": "sc3", "alias": "logic3", "enabled": "true",
  "content": [
    {"id":"0","text":["When website loaded..."],"globalid":"e0","x":"4900","y":"4900","width":"360",
      "actions":[
        {"id":"57","text":["Split (one/two/three)",{"value":"one/two/three","t":"string"},{"value":"/","t":"string","l":"separator"},"→ (41)",{"value":"41","t":"string","l":"table"}],"globalid":"a1"},
        {"id":"113","text":["Iterate through (41)",{"value":"41","t":"string","l":"table"},"({l!index},{l!value})"],"globalid":"a2"},
        {"id":"99","text":["Find child named (row{l!index})",{"value":"row{l!index}","t":"string"},"in (list)",{"value":"list","t":"object"},"→ (l!5)",{"value":"l!5","t":"string","l":"variable"}],"globalid":"a3"},
        {"id":"92","text":["If (l!5)",{"value":"l!5","t":"string","l":"variable"},"exists"],"globalid":"a4"},
        {"id":"10","text":["Set ({l!5})",{"value":"{l!5}","t":"object"},"text to ({l!value})",{"value":"{l!value}","t":"string"}],"globalid":"a5"},
        {"id":"25","text":["end"],"globalid":"a6"},
        {"id":"25","text":["end"],"globalid":"a7"}
      ]}
  ]
}
```

`Find child named` matches on the child's `alias`, so the rows here must be aliased `row1`, `row2`, `row3`. Every `If` (with or without an `else`), `Repeat`, and `Iterate` needs exactly one matching `end`, all as flat siblings. Getting the count and order of `end` blocks right is the most common structural script error.

### 5.9d — A broken script and its fix

**WRONG** — `"globalid":"s x"` (space breaks references), flat-string event `text`, `If` nesting its body in a child `actions` array, `Define function` nested inside the event. **RIGHT** — alphanumeric globalids, text-arrays with the `()` convention, flat `If`→body→`end`, `Define function` as a top-level `content` sibling. (See §5.9a for the canonical correct shapes.)

### 5.9e — Loops + math + tables together (every parameter shape confirmed from the block-palette export)

Builds a table of square roots for 1–5: `Repeat n times` (id `22`) counts up, `Run math function` (id `114`) computes `sqrt` each pass, `Set entry of table` (id `55`) stores it, then `Iterate through` (id `113`) reads the table back out. This is the failure cluster the earlier guide never covered end-to-end — loops, math, and tables only ever appeared in isolation.

```json
{
  "class": "script", "globalid": "sc4", "alias": "logic4", "enabled": "true",
  "content": [
    {"id":"0","text":["When website loaded..."],"globalid":"e0","x":"4900","y":"4900","width":"360",
      "actions":[
        {"id":"54","text":["Create table (1)",{"value":"1","t":"string","l":"table"}],"globalid":"a1"},
        {"id":"11","text":["Set (2)",{"value":"2","t":"string","l":"variable"},"to (0)",{"value":"0","t":"string","l":"any"}],"globalid":"a2"},
        {"id":"22","text":["Repeat (5)",{"value":"5","t":"number"},"times"],"globalid":"a3"},
        {"id":"12","text":["Increase (2)",{"value":"2","t":"string","l":"variable"},"by (1)",{"value":"1","t":"number"}],"globalid":"a4"},
        {"id":"114","text":["Run math function (sqrt)",{"value":"sqrt","t":"string","l":"function"},{"value":[{"value":"{2}","t":"string","l":"any"}],"t":"tuple"},"→ (3)",{"value":"3","t":"string","l":"variable"}],"globalid":"a5"},
        {"id":"55","text":["Set entry ({2})",{"value":"{2}","t":"string","l":"entry"},"of (1)",{"value":"1","t":"string","l":"table"},"to ({3})",{"value":"{3}","t":"string","l":"any"}],"globalid":"a6"},
        {"id":"25","text":["end"],"globalid":"a7"},
        {"id":"113","text":["Iterate through (1)",{"value":"1","t":"string","l":"table"},"({l!index},{l!value})"],"globalid":"a8"},
        {"id":"0","text":["Log ({l!value})",{"value":"{l!value}","t":"any"}],"globalid":"a9"},
        {"id":"25","text":["end"],"globalid":"a10"}
      ]}
  ]
}
```

Points worth internalizing from this one:
- The counter `{2}` is incremented **before** it's used as both the math-function argument and the table entry index — table entries here run 1–5, never 0 (§5.7's "setting index 1 converts a table to an array" note).
- `Run math function`'s tuple has exactly one entry, each entry itself shaped `{"value":...,"t":"string","l":"any"}` (§5.4a) — not a bare string, not a bare number.
- Two `end`s in the whole script, one per opener (`Repeat` at a3, `Iterate` at a8) — flat siblings, no nesting (§5.9c).
- Swap the `Log` at the end for a `Set <object> text to ({l!value})` (id `10`) once you have a real label `globalid` to target; the loop/math/table mechanics above don't change.

---
