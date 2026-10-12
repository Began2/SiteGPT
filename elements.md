# SiteGPT: Elements reference

Companion file to the SiteGPT V12 CatWeb guide (https://raw.githubusercontent.com/Began2/SiteGPT/main/SiteGPT%20V12.md). Full properties and an import-valid example for every element class and styling modifier. Section references (§) point to sections of the main guide.

---

### 2.4 Element Classes

**11 visual classes**, plus `script` and `Folder` (non-visual), plus the styling modifiers in §2.7. Every one adds to the site's cost (§8).

Each section below gives the class's own properties. **Everything also accepts the common properties from §2.1** (`position`, `size`, `width`/`height`, `anchor`, `z_index`, `visible`, `rotation`, `tooltip`, `children`) — those aren't repeated per class. Every example is import-valid and uses the house palette, so they compose into one coherent page rather than standing alone: copy the shape, swap the values.

---

#### `Frame`

Inert container — layout wrappers, cards, dividers, backgrounds, decorative shapes. No properties of its own beyond the common set.

```json
{
  "class": "Frame",
  "globalid": "cd",
  "alias": "statcard",
  "position": "{0,0},{0,0}",
  "size": "auto_y",
  "width": "{1,0}",
  "background_color": "#16181a",
  "background_transparency": "0",
  "children": [
    {"class": "UICorner", "globalid": "rd", "radius": "0,10"},
    {"class": "UIStroke", "globalid": "cs", "stroke_color": "#262629", "stroke_thickness": "1"}
  ]
}
```

**Never use a `Frame` for anything that looks clickable** — nav items, tabs, filter chips, linking cards, toggles. Even in a static mockup those are `TextButton`s, so they can carry `auto_color` hover feedback and a press event. A `Frame` cannot respond to a click at all.

---

#### `TextLabel`

Static, non-interactive text.

```json
{
  "class": "TextLabel",
  "globalid": "ct",
  "alias": "cardtitle",
  "text": "Monthly revenue",
  "font": "BuilderSansBold",
  "font_size": "16",
  "font_color": "#ffffff",
  "font_weight": "Bold",
  "font_style": "Normal",
  "font_transparency": "0",
  "align_x": "Left",
  "align_y": "Center",
  "rich": "false",
  "wrap": "true",
  "truncate": "AtEnd",
  "line_height": "1",
  "background_transparency": "1",
  "position": "{0,0},{0,0}",
  "size": "{1,0},{0,24}"
}
```

**Values:** `font_size` a string number or `"scaled"` · `font_weight` `"Thin"`…`"Heavy"` · `font_style` `"Normal"`/`"Italic"` · `align_x` `"Left"`/`"Center"`/`"Right"` · `align_y` `"Top"`/`"Center"`/`"Bottom"` · `truncate` `"AtEnd"`/`"None"`/`"SplitWord"`.

`text` supports `\n`. Setting `rich:"true"` enables markup inside `text` — `<b>`, `<i>`, `<font color="#4e9bff">`. **Limits:** ~20,000 characters per text element before TEXT_OVERLOAD, 200,000 across all text elements on the page.

---

#### `TextButton`

Clickable button. Every `TextLabel` property, plus `auto_color`.

```json
{
  "class": "TextButton",
  "globalid": "pb",
  "alias": "ctaprimary",
  "text": "Create report",
  "font": "BuilderSansMedium",
  "font_size": "14",
  "font_color": "#ffffff",
  "align_x": "Center",
  "align_y": "Center",
  "auto_color": "true",
  "background_color": "#4e9bff",
  "position": "{0,0},{0,0}",
  "size": "auto",
  "children": [
    {"class": "UICorner", "globalid": "pr", "radius": "0,8"},
    {"class": "UIPadding", "globalid": "pp", "left": "0,16", "right": "0,16", "top": "0,10", "bottom": "0,10"}
  ]
}
```

`auto_color:"true"` darkens the button slightly on press for free — cheap feedback with no script. Drives the events `When <button> pressed...` (event id `1`), mouse enter/leave/down/up (event ids `3`/`5`/`11`/`12`) and right-click (event id `13`).

---

#### `TextButton?link`

Button that navigates instead of firing a script event.

```json
{
  "class": "TextButton?link",
  "globalid": "nd",
  "alias": "navdocs",
  "text": "Docs",
  "href": "mysite.rbx/docs",
  "new_tab": "false",
  "font": "BuilderSansMedium",
  "font_size": "14",
  "font_color": "#adadad",
  "align_x": "Center",
  "align_y": "Center",
  "auto_color": "true",
  "background_transparency": "1",
  "position": "{0,0},{0,0}",
  "size": "auto"
}
```

`href` is a CatWeb path (`"mysite.rbx/page"`), optionally with a query string (`"mysite.rbx/docs?view=intro"`; read it on the target page with `Get query string parameter`, action id `67`). `new_tab` is `"true"`/`"false"`. Use this for real navigation; use a plain `TextButton` + `Redirect to` (id `4`) only when the destination depends on runtime logic.

---

#### `TextButton?transfer`

Roblox purchase prompt.

```json
{
  "class": "TextButton?transfer",
  "globalid": "sp",
  "alias": "supportbtn",
  "text": "Support the project",
  "product": "123456789",
  "product_type": "Product",
  "thanks_href": "mysite.rbx/thanks",
  "font_size": "14",
  "font_color": "#08090a",
  "align_x": "Center",
  "align_y": "Center",
  "auto_color": "true",
  "background_color": "#68de5b",
  "background_transparency": "0",
  "position": "{0,0},{0,0}",
  "size": "auto"
}
```

**The class value is `TextButton?transfer` — never `TextButton?donation`.** Its default label reads "Donation", but that is the button's `text`, not its class; `?donation` is an unrecognised class and will not act as a purchase button. `product_type` is `"GamePass"`/`"Asset"`/`"Product"`; `thanks_href` is optional. Completion fires `When donation completed...` (id `15`), which is **parameterless** — it carries no bound object, so one handler cannot tell which button fired.

---

#### `TextButton?avataritem`

Avatar-item purchase button — same purchase family as `?transfer`.

```json
{
  "class": "TextButton?avataritem",
  "globalid": "ai",
  "alias": "itembtn",
  "text": "Get the hat",
  "font_size": "14",
  "font_color": "#08090a",
  "align_x": "Center",
  "align_y": "Center",
  "auto_color": "true",
  "background_color": "#68de5b",
  "background_transparency": "0",
  "position": "{0,0},{0,0}",
  "size": "auto"
}
```

Completion fires `When <avataritem> bought...` (id `7`) which — unlike `?transfer`'s event — **does** carry the purchased item as a bound object parameter, so a single handler can serve several buttons.

---

#### `ImageLabel`

Displays a Roblox image asset.

```json
{
  "class": "ImageLabel",
  "globalid": "is",
  "alias": "iconsearch",
  "image": "rbxassetid://76297972789266",
  "image_id": "76297972789266",
  "image_color": "#adadad",
  "image_transparency": "0",
  "scale_type": "Fit",
  "background_transparency": "1",
  "position": "{0,0},{0,0}",
  "size": "{0,16},{0,16}"
}
```

**`image` and `image_id` must reference the same asset** — `image` is the `rbxassetid://123` form, `image_id` the bare `123`. Both are normally present. `image_color` tints the asset (the icon library is pure white precisely so it tints cleanly). `scale_type` is `"Fit"`/`"Crop"`/`"Slice"`/`"Stretch"`/`"Tile"`; a `UIAspectRatioConstraint` child locks the natural ratio.

---

#### `ImageButton`

Clickable image. Every `ImageLabel` property, plus `auto_color`.

```json
{
  "class": "ImageButton",
  "globalid": "mt",
  "alias": "menutoggle",
  "image": "rbxassetid://84352806499655",
  "image_id": "84352806499655",
  "image_color": "#ffffff",
  "scale_type": "Fit",
  "auto_color": "true",
  "background_transparency": "1",
  "position": "{0,0},{0,0}",
  "size": "{0,24},{0,24}"
}
```

Fires the same events as `TextButton`. Swap the icon at runtime with `Set <object> image to` (action id `106`). That is how the hamburger/close toggle in §6 works.

---

#### `ImageButton?link`

Image that navigates. `ImageButton` plus `href` / `new_tab`.

```json
{
  "class": "ImageButton?link",
  "globalid": "bl",
  "alias": "brandlogo",
  "image": "rbxassetid://128490289676597",
  "image_id": "128490289676597",
  "href": "mysite.rbx/home",
  "new_tab": "false",
  "image_color": "#ffffff",
  "scale_type": "Fit",
  "auto_color": "true",
  "background_transparency": "1",
  "position": "{0,0},{0,0}",
  "size": "{0,28},{0,28}"
}
```

---

#### `TextBox`

User text input.

```json
{
  "class": "TextBox",
  "globalid": "si",
  "alias": "searchinput",
  "text": "",
  "placeholder": "Search projects",
  "placeholder_color": "#787878",
  "editable": "true",
  "multiline": "false",
  "rich": "false",
  "font": "BuilderSans",
  "font_size": "13",
  "font_color": "#d7d7d7",
  "align_x": "Left",
  "align_y": "Center",
  "background_color": "#0f1112",
  "background_transparency": "0",
  "position": "{0,0},{0,0}",
  "size": "{1,0},{0,34}",
  "children": [
    {"class": "UIPadding", "globalid": "sd", "left": "0,12", "right": "0,12"}
  ]
}
```

`text` is the live value and starts `""` — `placeholder` is the greyed hint shown while it is empty. Read the current value with `Get text from <input>` (action id `30`); pressing Enter fires `When <input> submitted...` (event id `8`). `multiline:"true"` makes it a textarea; `editable:"false"` makes it read-only, which is how you build a copyable output field.

---

#### `ScrollingFrame`

Scrollable container.

```json
{
  "class": "ScrollingFrame",
  "globalid": "bs",
  "alias": "bodyscroll",
  "canvassize": "auto_y",
  "scrollbar_thickness": "6",
  "scrollbar_color": "#262629",
  "scrollbar_transparency": "0",
  "background_transparency": "1",
  "position": "{0,0},{0,56}",
  "size": "{1,0},{1,-56}",
  "children": []
}
```

`canvassize` is `"auto_y"` (grows downward — most common), `"auto_x"` (carousels), `"auto_xy"` (rare), or a fixed UDim2 such as `"{0,0},{2,0}"` (a canvas twice the frame's height). **Never bare `"auto"`** — always pick an axis, and never leave the non-scrolling axis free. Reach for this only when content genuinely overflows a fixed-height viewport; a `Frame` with `size:"auto_y"` is the right call for content that merely grows.

**Scrollbar styling.** `scrollbar_thickness`, `scrollbar_color` and `scrollbar_transparency` set its size and colour, and scripts can change all three. To replace the scrollbar's images, set `scrollbar_top_image_id`, `scrollbar_mid_image_id` and `scrollbar_bottom_image_id`. Each is a bare asset ID with no `rbxassetid://`, e.g. `"scrollbar_mid_image_id":"6319951718"`. Their script names are `Top Image`, `Middle Image` and `Bottom Image` (§7). Leave all three out to keep the default scrollbar.

---

#### `script`

Event and function logic (§5). Not rendered.

```json
{
  "class": "script",
  "globalid": "lg",
  "alias": "logic",
  "enabled": "true",
  "content": []
}
```

`content` holds the event and `Define function` blocks (§5.2). Scripts can sit anywhere in the tree, and multiple scripts on a page share global variables and functions. Must be `"class":"script"` inside `webcontent` — a top-level `"script"` key in the JSON root throws `[INVALIDATED] invalid property script`.

---

#### `Folder`

Invisible organiser — groups elements in the editor tree without rendering anything.

```json
{
  "class": "Folder",
  "globalid": "ng",
  "alias": "navgroup",
  "children": []
}
```

Adds to the site's cost (§8) but renders nothing. It has no position or size, so it cannot lay anything out — a `Folder` only tidies the tree. When you need grouping that *affects layout*, use a `Frame`.

---

### 2.7 Styling Modifier Elements

**Styling elements must be children of a visual element.** Never siblings, never at the root, never inside a `Folder` — a modifier styles its parent, so a misplaced one either does nothing or fails import.

They carry no `position`, `size`, or `anchor` of their own (`UIGridLayout` and `UISizeConstraint` use `size`-shaped values, but as *settings*, not as their own geometry). Most work with zero configuration; the defaults below are what CatWeb writes for a freshly added modifier.

---

#### `UICorner`

Rounds the parent's corners.

```json
{"class": "UICorner", "globalid": "cr", "radius": "0,10"}
```

`radius` is a UDim — `"0,10"` is 10px, `"1,0"` is a full pill/circle.

**Individual corners.** Round each corner differently with `radius_top_left`, `radius_top_right`, `radius_bottom_left` and `radius_bottom_right`, each a UDim. Use them for a tab that is only rounded on top, a dropdown attached to the element above it, or a chat bubble with one sharp corner.

```json
{"class": "UICorner", "globalid": "tc", "radius_top_left": "0,10", "radius_top_right": "0,10", "radius_bottom_left": "0,0", "radius_bottom_right": "0,0"}
```

In scripts the four are `Top Left Radius`, `Top Right Radius`, `Bottom Left Radius` and `Bottom Right Radius` (§7).

---

#### `UIShadow`

Drop shadow behind the parent. Use it on things that float above the page, such as dropdowns, modals, popovers and a lifted card on hover.

```json
{
  "class": "UIShadow",
  "globalid": "sh",
  "shadow_color": "#000000",
  "shadow_transparency": "0.6",
  "shadow_offset": "{0,0},{0,4}",
  "shadow_spread": "{0,2},{0,2}",
  "blur_radius": "0,12"
}
```

| Key | Format | Notes |
|---|---|---|
| `shadow_color` | `"#rrggbb"` | Keep the `#`. Black, or a dark tint of the accent, on dark themes. |
| `shadow_transparency` | `"0"`–`"1"` | `0.5`–`0.7` reads as a soft shadow; lower is harsher. |
| `shadow_offset` | UDim2 | How far the shadow is shifted. Use pixel offsets (`"{0,0},{0,4}"` drops it 4px); scale values move it by a fraction of the parent's size. |
| `shadow_spread` | UDim2 | How much bigger than the parent the shadow is, per axis. |
| `blur_radius` | UDim | How soft the edge is, e.g. `"0,12"`. |

Every key is optional; a bare `UIShadow` uses CatWeb's default shadow. It also accepts `z_index`.

---

#### `UIStroke`

Outline/border on the parent.

```json
{
  "class": "UIStroke",
  "globalid": "sk",
  "stroke_color": "#262629",
  "stroke_thickness": "1",
  "stroke_transparency": "0",
  "stroke_mode": "Border"
}
```

`stroke_mode` is `"Border"` (outside the parent's edge) or `"Contextual"`.

---

#### `UIPadding`

Inner spacing. (§2.6).

```json
{
  "class": "UIPadding",
  "globalid": "pa",
  "top": "0,20",
  "bottom": "0,20",
  "left": "0,24",
  "right": "0,24"
}
```

Each side is a UDim and each is optional — set only the sides you need. Never fake padding by offsetting a child's `position` and shrinking its `size`; the parent's edge does not move, so the content still hugs it.

---

#### `UIListLayout`

Lays children out in a row or column. The backbone of nearly every real page — it is what makes sections stack without manual Y offsets.

```json
{
  "class": "UIListLayout",
  "globalid": "ll",
  "direction": "Vertical",
  "padding": "0,24",
  "sort": "LayoutOrder",
  "alignment_horizontal": "Left",
  "alignment_vertical": "Top",
  "wrap_list": "false"
}
```

`direction` is `"Vertical"`/`"Horizontal"`. `padding` is the **gap between children** as a UDim (`"0,24"` = 24px), not inner padding — that is `UIPadding`. Children need an integer `"order"` (§2.3); prefer `sort:"LayoutOrder"` over `"Name"`. `wrap_list:"true"` lets an overflowing horizontal row flow onto a second line (chips, tags).

**Flex distribution.** Add `horizontal_flex` on a `direction:"Horizontal"` layout, or `vertical_flex` on a `direction:"Vertical"` one, to control how children share the leftover space along the layout axis. Values: `"Fill"` `"None"` `"SpaceAround"` `"SpaceBetween"` `"SpaceEvenly"`.

```json
{"class":"UIListLayout","globalid":"xg","direction":"Horizontal","sort":"LayoutOrder","horizontal_flex":"SpaceBetween","padding":"0,0"}
```

Use `"Fill"` to stretch children to consume all remaining space, `"SpaceBetween"`/`"SpaceAround"`/`"SpaceEvenly"` to distribute gaps between fixed-size children (nav bars, pricing tiers), `"None"` for the default packed behavior. To opt one specific child out of the parent's flex behavior, give it a `UIFlexItem` child (no properties of its own — see below).

---

#### `UIGridLayout`

Lays children out in equal-sized cells.

```json
{
  "class": "UIGridLayout",
  "globalid": "gl",
  "size": "{0,340},{0,300}",
  "padding": "0,20",
  "sort": "LayoutOrder",
  "alignment_horizontal": "Left",
  "alignment_vertical": "Top"
}
```

**The cell size key is `size` — not `cell_size`.** `Cell Size` is the *script-side* display name for the same property (§2.1b); snake_casing it into the JSON throws `default not found for property cell_size`. Cells are uniform, so `UIGridLayout` suits card grids; for rows of differing heights use a `UIListLayout` instead.

---

#### `UIGradient`

Gradient fill across the parent. One of the cheapest ways to add depth.

```json
{
  "class": "UIGradient",
  "globalid": "gd",
  "gradient_color": "[[0,\"4e9bff\"],[1,\"7274e0\"]]",
  "gradient_transparency": "[[0,\"0\"],[1,\"0.6\"]]",
  "rotation": "90"
}
```

`gradient_color` is a **stringified array of `[position, "hex"]` stops**, position `0`–`1`. **The hex values inside this array carry no `#`**: write `"4e9bff"`, not `"#4e9bff"`. Element properties like `background_color` keep the `#`; gradient stops and script values drop it (full rule in §5.7a). `rotation` is degrees (`"90"` = top-to-bottom). Spend 2–3 gradient moments per page, not one everywhere.

---

#### `UIAspectRatioConstraint`

Locks the parent's width:height ratio.

```json
{"class": "UIAspectRatioConstraint", "globalid": "ar", "ratio": "1"}
```

`ratio` is width ÷ height — `"1"` square, `"1.78"` for 16:9. Use it on icons and avatars so they stay square while their container flexes, and on media thumbnails to stop them distorting.

---

#### `UISizeConstraint`

Clamps the parent's pixel size.

```json
{"class": "UISizeConstraint", "globalid": "sz", "min_size": "280,0", "max_size": "1200,inf"}
```

Values are `"x,y"` pixel pairs; `"inf"` means unclamped on that axis. The main use is a readable max width on a content column: let it scale to the viewport but stop it stretching to an unreadable line length.

---

#### `UIFlexItem`

Overrides how a single child flexes inside a `UIListLayout` parent.

```json
{"class": "UIFlexItem", "globalid": "fx"}
```

Only meaningful inside a `UIListLayout`. It is the per-child escape hatch — the layout distributes space, and this element opts one child out of that default.
