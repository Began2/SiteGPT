# SiteGPT: Decoder

Companion file to the SiteGPT V12 CatWeb guide (https://raw.githubusercontent.com/Began2/SiteGPT/main/SiteGPT%20V12.md). The character code table, the decoder script and how to call it. Section references (§) point to sections of the main guide.

---

## 9. The decoder: for really long strings only

Roblox runs its text filter over CatWeb display text, so a string can come out masked as `######`. **For ordinary site copy this is rare, so write your text normally.** Headings, nav items, button labels, stat numbers and short body copy all go straight into `text` as plain strings.

The decoder exists for one case: **really long strings you wrote as site copy**, such as a long paragraph of body text, where there is more surface for the filter to trip on by mistake. **Never use it on user-entered text, on broadcast payloads, or on anything the filter would rightly block.** It is for false positives on your own copy, nothing else.

**Do not encode by default.** Every encoded string is hand-computed, and a miscount fails *silently*: you get garbled characters, not an obvious `######`. Reach for the decoder only when a string is genuinely long.

**When you do use it:**
1. Add the decoder script (§9.2) as a `"class":"script"` element.
2. Encode the string with the table (§9.1).
3. Leave that label's JSON `text` as `""`.
4. Set the text at runtime with a caller event (§9.3).

**Compute encodings by reasoning, never with a tool call.** The `d`/`e` functions run inside the published site at runtime, so you do not need to execute them. Look each character up in §9.1 and build the digit string yourself.

### 9.1 Character → code table

Each character has a **code**: a number that never contains the digit `0`. That is what makes the format work, because `0` is the separator.

**To encode:** look up each character's code, join the codes with `0`, and add one `0` at the start and one at the end.

```
"Cat"  ->  C=33, a=69, t=91  ->  0 33 0 69 0 91 0  ->  "0330690910"
```

Codes are **variable length** (1–3 digits). Do not pad them. Never write `00`.

**Core table: space, punctuation, letters, digits.** This is everything normal site copy needs.

| char | code | char | code | char | code | char | code | char | code | char | code |
|---|---|---|---|---|---|---|---|---|---|---|---|
| *(space)* | `1` | `!` | `2` | `"` | `3` | `#` | `4` | `$` | `5` | `%` | `6` |
| `'` | `7` | `(` | `8` | `)` | `9` | `+` | `11` | `,` | `12` | `-` | `13` |
| `.` | `14` | `/` | `15` | `{` | `16` | `\|` | `17` | `}` | `18` | `@` | `19` |
| `~` | `21` | `→` | `22` | `’` | `23` | `—` | `24` | `&` | `25` | `:` | `26` |
| `;` | `27` | `?` | `28` | `=` | `29` | `A` | `31` | `B` | `32` | `C` | `33` |
| `D` | `34` | `E` | `35` | `F` | `36` | `G` | `37` | `H` | `38` | `I` | `39` |
| `J` | `41` | `K` | `42` | `L` | `43` | `M` | `44` | `N` | `45` | `O` | `46` |
| `P` | `47` | `Q` | `48` | `R` | `49` | `S` | `51` | `T` | `52` | `U` | `53` |
| `V` | `54` | `W` | `55` | `X` | `56` | `Y` | `57` | `Z` | `58` | `[` | `59` |
| `\` | `61` | `]` | `62` | `^` | `63` | `_` | `64` | `` ` `` | `65` | `<` | `66` |
| `>` | `67` | `*` | `68` | `a` | `69` | `b` | `71` | `c` | `72` | `d` | `73` |
| `e` | `74` | `f` | `75` | `g` | `76` | `h` | `77` | `i` | `78` | `j` | `79` |
| `k` | `81` | `l` | `82` | `m` | `83` | `n` | `84` | `o` | `85` | `p` | `86` |
| `q` | `87` | `r` | `88` | `s` | `89` | `t` | `91` | `u` | `92` | `v` | `93` |
| `w` | `94` | `x` | `95` | `y` | `96` | `z` | `97` | `1` | `98` | `2` | `99` |
| `3` | `111` | `4` | `112` | `5` | `113` | `6` | `114` | `7` | `115` | `8` | `116` |
| `9` | `117` | `0` | `118` |  |  |  |  |  |  |  |  |

**Extended Latin** (accented names, symbols, currency). Same rules.

| char | code | char | code | char | code | char | code | char | code | char | code |
|---|---|---|---|---|---|---|---|---|---|---|---|
| `⌦` | `119` | `€` | `121` | `ƒ` | `122` | `„` | `123` | `…` | `124` | `†` | `125` |
| `‡` | `126` | `ˆ` | `127` | `‰` | `128` | `Š` | `129` | `‹` | `131` | `Œ` | `132` |
| `Ž` | `133` | `‘` | `134` | *(unused)* | `135` | `“` | `136` | `”` | `137` | `•` | `138` |
| `–` | `139` | *(unused)* | `141` | `˜` | `142` | `™` | `143` | `š` | `144` | `›` | `145` |
| `œ` | `146` | `ž` | `147` | `Ÿ` | `148` | `¡` | `149` | `¢` | `151` | `£` | `152` |
| `¤` | `153` | `¥` | `154` | `¦` | `155` | `§` | `156` | `¨` | `157` | `©` | `158` |
| `ª` | `159` | `«` | `161` | `¬` | `162` | `®` | `163` | `¯` | `164` | `°` | `165` |
| `±` | `166` | `²` | `167` | `³` | `168` | `´` | `169` | `µ` | `171` | `¶` | `172` |
| `·` | `173` | `¸` | `174` | `¹` | `175` | `º` | `176` | `»` | `177` | `¼` | `178` |
| `½` | `179` | `¾` | `181` | `¿` | `182` | `À` | `183` | `Á` | `184` | `Â` | `185` |
| `Ã` | `186` | `Ä` | `187` | `Å` | `188` | `Æ` | `189` | `Ç` | `191` | `È` | `192` |
| `É` | `193` | `Ê` | `194` | `Ë` | `195` | `Ì` | `196` | `Í` | `197` | `Î` | `198` |
| `Ï` | `199` | `Ð` | `211` | `Ñ` | `212` | `Ò` | `213` | `Ó` | `214` | `Ô` | `215` |
| `Õ` | `216` | `Ö` | `217` | `×` | `218` | `Ø` | `219` | `Ù` | `221` | `Ú` | `222` |
| `Û` | `223` | `Ü` | `224` | `Ý` | `225` | `Þ` | `226` | `ß` | `227` | `à` | `228` |
| `á` | `229` | `â` | `231` | `ã` | `232` | `ä` | `233` | `å` | `234` | `æ` | `235` |
| `ç` | `236` | `è` | `237` | `é` | `238` | `ê` | `239` | `ë` | `241` | `ì` | `242` |
| `í` | `243` | `î` | `244` | `ï` | `245` | `ð` | `246` | `ñ` | `247` | `ò` | `248` |
| `ó` | `249` | `ô` | `251` | `õ` | `252` | `ö` | `253` | `÷` | `254` | `ø` | `255` |
| `ù` | `256` | `ú` | `257` | `û` | `258` | `ü` | `259` | `ý` | `261` | `þ` | `262` |
| `ÿ` | `263` | *(newline)* | `264` |  |  |  |  |  |  |  |  |

**Two unused slots.** Codes `135` and `141` are placeholders (`!!`) in the decoder's table. Never use them. Characters not in these tables cannot be encoded; rephrase without them.

### 9.2 The decoder script: copy it exactly

The decoder is **three blocks**: a `When website loaded` setup event that builds the character tables, `Define function d` (decode) and `Define function e` (encode, which you will rarely need). Copy them exactly as given:

- **Do not edit, rename, reformat or reorder anything** in these three blocks. Keep every globalid, action id, variable name, `x`/`y` value and escape sequence (`\u000B`, `\f`, `\\{`, `%%`).
- **It is the one exception to the house rules.** Its globalids use punctuation (and one, `" a"`, starts with a space), its variables have word names (`o!nums`, `l!temp`), and its functions take a numeric parameter (`3`). Do not "fix" any of this. The rules in §2.1, §5.3a and §5.7 apply to everything *you* generate.
- **Never reuse a decoder globalid** elsewhere in the file. The alphanumeric ones are: `XD fT ri Pr np 7W Eh UX Ub ig Vn dN rO gs 29 ci 0H wh gb b9 M8 ph qT Ua`.
- **It is exported as a one-item array** (`[{...}]`). Place the object inside the brackets into a `children` array. Do not nest the brackets.
- **The only thing you may add** is your own caller event(s) appended to the end of its `content` array (§9.3). If a user pastes a decoder carrying other extra blocks, strip it back to these three blocks plus your callers.

```json
[{"enabled":"true","content":[{"y":"4626","x":"5498","globalid":" a","id":"0","text":["When website loaded..."],"actions":[{"id":"11","text":["Set",{"value":"o!1","t":"string","l":"variable"},"to",{"value":"! \" # $ !! ' ( ) + , - . / \\{ | \\} @ ~ → ’ — & : ; ? = A B C D E F G H I J K L M N O P Q R S T U V W X Y Z [ \\ ] ^ _ ` < > * a b c d e f g h i j k l m n o p q r s t u v w x y z ","t":"string","l":"any"}],"globalid":"#W"},{"id":"11","text":["Set",{"value":"o!1","t":"string","l":"variable"},"to",{"value":"{o!1}1 2 3 4 5 6 7 8 9 0 ","t":"string","l":"any"}],"globalid":"fT"},{"id":"11","text":["Set",{"value":"o!1","t":"string","l":"variable"},"to",{"value":"{o!1}⌦ € ƒ „ … † ‡ ˆ ‰ Š ‹ Œ Ž ‘ !! “ ” • – !! ˜ ™ š › œ ž Ÿ ¡ ¢ £ ¤ ¥ ¦ § ¨ © ª « ¬ ® ¯ ° ± ² ³ ´ µ ¶ · ¸ ¹ º » ¼ ½ ¾ ¿ À Á Â Ã Ä Å Æ Ç È É Ê Ë Ì Í Î Ï Ð Ñ Ò Ó Ô Õ Ö × Ø Ù Ú Û Ü Ý Þ ß à á â ã ä å æ ç è é ê ë ì í î ï ð ñ ò ó ô õ ö ÷ ø ù ú û ü ý þ ÿ \n","t":"string","l":"any"}],"globalid":"3#"},{"id":"57","text":["Split",{"value":"{o!1}","t":"string"},{"value":" ","t":"string","l":"separator"},"→",{"value":"o!2","t":"string","l":"table"}],"globalid":"$x"},{"id":"89","text":["Insert",{"value":" ","t":"string","l":"any"},"at position",{"value":"1","t":"number","l":"number?"},"of",{"value":"o!2","t":"string","l":"array"}],"globalid":"=L"},{"text":["Set entry",{"value":"6","t":"string","l":"entry"},"of",{"value":"o!2","t":"string","l":"table"},"to",{"value":"%%","t":"string","l":"any"}],"globalid":"$|","id":"55"},{"id":"57","text":["Split",{"value":"1 2 3 4 5 6 7 8 9 11 12 13 14 15 16 17 18 19 21 22 23 24 25 26 27 28 29 31 32 33 34 35 36 37 38 39 41 42 43 44 45 46 47 48 49 51 52 53 54 55 56 57 58 59 61 62 63 64 65 66 67 68 69 71 72 73 74 75 76 77 78 79 81 82 83 84 85 86 87 88 89 91 92 93 94 95 96 97 98 99 111 112 113 114 115 116 117 118 119 121 122 123 124 125 126 127 128 129 131 132 133 134 135 136 137 138 139 141 142 143 144 145 146 147 148 149 151 152 153 154 155 156 157 158 159 161 162 163 164 165 166 167 168 169 171 172 173 174 175 176 177 178 179 181 182 183 184 185 186 187 188 189 191 192 193 194 195 196 197 198 199 211 212 213 214 215 216 217 218 219 221 222 223 224 225 226 227 228 229 231 232 233 234 235 236 237 238 239 241 242 243 244 245 246 247 248 249 251 252 253 254 255 256 257 258 259 261 262 263 264 265 266 267 268 269 271 272 273 274 275 276 277 278 279 281 282 283 284 285 286 287 288 289 291 292 293 294 295 296 297 298 299","t":"string"},{"value":" ","t":"string","l":"separator"},"→",{"value":"{o!nums}","t":"string","l":"table"}],"globalid":"ri"},{"id":"57","text":["Split",{"value":"0123456789","t":"string"},{"value":"","t":"string","l":"separator"},"→",{"value":"o!rnum","t":"string","l":"table"}],"globalid":"Pr"}],"width":"350"},{"y":"4623","variable_overrides":[{"value":"3"}],"x":"5133","globalid":"np","id":"6","text":["Define function",{"value":"d","t":"string","l":"function"}],"actions":[{"text":["If",{"value":"{o!2}","t":"string","l":"variable"},"doesn't exist"],"globalid":"7W","id":"93"},{"id":"3","text":["Wait",{"value":"0.01","t":"number"},"seconds"],"globalid":"?U"},{"id":"25","text":["end"],"globalid":"Eh"},{"id":"43","text":["Replace",{"value":"0","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"\u000B\f","t":"string"}],"globalid":"*)"},{"id":"113","text":["Iterate through",{"value":"{o!nums}","t":"string","l":"table"},"({l!index},{l!value})"],"globalid":"d?"},{"text":["If",{"value":"{l!3}","t":"string"},"contains",{"value":"{l!value}","t":"string"}],"globalid":"UX","id":"37"},{"id":"56","text":["Get entry",{"value":"{l!index}","t":"string","l":"entry"},"of",{"value":"{o!2}","t":"string","l":"table"},"→",{"value":"{l!ac}","t":"string","l":"variable"}],"globalid":"Ub"},{"id":"43","text":["Replace",{"value":"\f{l!value}\u000B","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"{l!ac}","t":"string"}],"globalid":"S`"},{"id":"25","text":["end"],"globalid":"#%"},{"id":"25","text":["end"],"globalid":"ig"},{"id":"42","text":["Sub",{"value":"{l!3}","t":"string","l":"variable"},{"value":"2","t":"number","l":"start"},"-",{"value":"-2","t":"number","l":"end"}],"globalid":"Vn"},{"id":"115","text":["Return",{"value":"{l!3}","t":"string","l":"any"}],"globalid":"dN"}],"width":"350"},{"y":"4623","variable_overrides":[{"value":"3"}],"x":"4767","globalid":"rO","id":"6","text":["Define function",{"value":"e","t":"string","l":"function"}],"actions":[{"text":["If",{"value":"{o!2}","t":"string","l":"variable"},"doesn't exist"],"globalid":"gs","id":"93"},{"id":"3","text":["Wait",{"value":"0.01","t":"number"},"seconds"],"globalid":";|"},{"id":"25","text":["end"],"globalid":"29"},{"id":"43","text":["Replace",{"value":"\f","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"","t":"string"}],"globalid":"ci"},{"id":"43","text":["Replace",{"value":"\u000B","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"","t":"string"}],"globalid":"=x"},{"id":"113","text":["Iterate through",{"value":"o!2","t":"string","l":"table"},"({l!index},{l!value})"],"globalid":"'6"},{"text":["If",{"value":"{l!3}","t":"string"},"contains",{"value":"{l!value}","t":"string"}],"globalid":"!W","id":"37"},{"id":"43","text":["Replace",{"value":"{l!value}","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"{l!value}\f","t":"string"}],"globalid":"9?"},{"id":"25","text":["end"],"globalid":"0H"},{"id":"25","text":["end"],"globalid":"$p"},{"id":"113","text":["Iterate through",{"value":"o!2","t":"string","l":"table"},"({l!index},{l!value})"],"globalid":"a:"},{"text":["If",{"value":"{l!3}","t":"string"},"contains",{"value":"{l!value}","t":"string"}],"globalid":"n}","id":"37"},{"id":"56","text":["Get entry",{"value":"{l!index}","t":"string","l":"entry"},"of",{"value":"{o!nums}","t":"string","l":"table"},"→",{"value":"{l!an}","t":"string","l":"variable"}],"globalid":"wh"},{"id":"43","text":["Replace",{"value":"{l!value}\f","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"0{l!an}0","t":"string"}],"globalid":"'u"},{"id":"25","text":["end"],"globalid":"5-"},{"id":"25","text":["end"],"globalid":"gb"},{"id":"43","text":["Replace",{"value":"%","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"060","t":"string"}],"globalid":"b9"},{"id":"43","text":["Replace",{"value":"00","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"0","t":"string"}],"globalid":"=m"},{"id":"11","text":["Set",{"value":"{l!temp}","t":"string","l":"variable"},"to",{"value":"{l!3}","t":"string","l":"any"}],"globalid":"S{"},{"id":"113","text":["Iterate through",{"value":"o!rnum","t":"string","l":"table"},"({l!index},{l!value})"],"globalid":"e,"},{"id":"43","text":["Replace",{"value":"{l!value}","t":"string"},"in",{"value":"{l!temp}","t":"string","l":"variable"},"by",{"value":"","t":"string"}],"globalid":")w"},{"id":"25","text":["end"],"globalid":":k"},{"text":["If",{"value":"{l!temp}","t":"string","l":"any"},"is not equal to",{"value":"","t":"string","l":"any"}],"globalid":"<B","id":"19"},{"id":"57","text":["Split",{"value":"{l!temp}","t":"string"},{"value":"","t":"string","l":"separator"},"→",{"value":"{l!temp}","t":"string","l":"table"}],"globalid":"]p"},{"id":"113","text":["Iterate through",{"value":"{l!temp}","t":"string","l":"table"},"({l!index},{l!value})"],"globalid":"M8"},{"id":"43","text":["Replace",{"value":"{l!value}","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"","t":"string"}],"globalid":"ph"},{"id":"25","text":["end"],"globalid":"z%"},{"id":"25","text":["end"],"globalid":"qT"},{"id":"43","text":["Replace",{"value":"00","t":"string"},"in",{"value":"{l!3}","t":"string","l":"variable"},"by",{"value":"0","t":"string"}],"globalid":"I("},{"id":"115","text":["Return",{"value":"{l!3}","t":"string","l":"any"}],"globalid":"Ua"}],"width":"350"}],"globalid":"XD","class":"script","alias":"Decode"}]
```

### 9.3 Calling pattern

The decoder's character tables live in **object-scoped** variables (`{o!2}`, `{o!nums}`), which are private to the decoder's script element (§5.7). So **every `Run function d` call goes in a caller event appended to the decoder's own `content` array**, not in a separate script. A different script element cannot see those tables and will render blank or garbled text. Reference the target label by `globalid`, which resolves anywhere in the file.

Start the caller with a short `Wait`. The setup event runs in parallel with yours, and `d` waits only one tick for the tables to exist.

```json
{"id":"0","text":["When website loaded..."],"globalid":"dc","x":"5498","y":"5100","width":"350","actions":[
  {"id":"3","text":["Wait (0.1)",{"value":"0.1","t":"number"},"seconds"],"globalid":"dw"},
  {"id":"132","text":["Run function (d)",{"value":"d","t":"string","l":"function"},{"value":[{"value":"0330690910","t":"string","l":"any"}],"t":"tuple"},"→ (80)",{"value":"80","t":"string","l":"variable?"}],"globalid":"dr"},
  {"id":"10","text":["Set (lb1)",{"value":"lb1","t":"object"},"text to ({80})",{"value":"{80}","t":"string"}],"globalid":"ds"}
]}
```

For several strings, repeat the `Run function` + `Set text` pair inside the same caller event, with a different numeric output variable each time.
