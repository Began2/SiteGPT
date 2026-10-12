# SiteGPT: Example site

Companion file to the SiteGPT V12 CatWeb guide (https://raw.githubusercontent.com/Began2/SiteGPT/main/SiteGPT%20V12.md). A complete, import-valid landing page to model a site on. Section references (§) point to sections of the main guide.

---

## What it shows

**Nimbus**, a landing page for a made-up notes app, on a dark theme. It uses the patterns the guide recommends:

- **Fixed header + scrolling body.** The header is pinned at the top; everything else lives in a `ScrollingFrame` (`canvassize:"auto_y"`) filling the rest of the screen.
- **A centred content column.** One `Frame` at `position:"{0.5,0},{0,0}"` with `anchor:"0.5,0"` and a `UISizeConstraint` max width of 1080px (§2.1c).
- **Sections stacked by a `UIListLayout`**, each with an integer `order` (§2.3, §3.3). No section has a manual Y offset.
- **A 3-card feature grid** with `UIGridLayout`. The cell size key is `size` (§2.7).
- **Depth used sparingly**: one `UIGradient` on the highlighted pricing card and one `UIShadow` under it.
- **A small script**: a Monthly/Yearly billing toggle that swaps the Pro price, and a hover tween on the main button. It follows §5.1a annotations, numeric variables and the `#`-less hex rule for script values (§5.7a).
- **Real icon IDs** from §10 and an icon as the favicon. No placeholder IDs.

Palette: page `#0b0c0e`, surface `#16181a`, border `#262629`, text `#f2f2f3`, muted text `#adadad`, accent `#4e9bff`.

## The site

```json
{
  "favicon": "80429653768693",
  "title": "Nimbus",
  "background": "#0b0c0e",
  "webcontent": [
    {"class":"Frame","globalid":"rt","alias":"page","position":"{0,0},{0,0}","size":"{1,0},{1,0}","background_color":"#0b0c0e","background_transparency":"0",
     "children":[

      {"class":"Frame","globalid":"hd","alias":"header","position":"{0,0},{0,0}","size":"{1,0},{0,56}","background_color":"#0b0c0e","background_transparency":"0","z_index":"10",
       "children":[
        {"class":"UIStroke","globalid":"hs","stroke_color":"#1a1a1a","stroke_thickness":"1"},
        {"class":"UIPadding","globalid":"hp","left":"0,24","right":"0,24"},
        {"class":"ImageLabel","globalid":"li","alias":"logoicon","image":"rbxassetid://80429653768693","image_id":"80429653768693","image_color":"#4e9bff","scale_type":"Fit","background_transparency":"1",
         "position":"{0,0},{0.5,0}","anchor":"0,0.5","size":"{0,22},{0,22}"},
        {"class":"TextLabel","globalid":"lt","alias":"logotext","text":"Nimbus","font":"BuilderSansBold","font_size":"18","font_color":"#f2f2f3","align_x":"Left","align_y":"Center","background_transparency":"1",
         "position":"{0,30},{0.5,0}","anchor":"0,0.5","size":"auto_x","height":"{0,28}"},
        {"class":"Frame","globalid":"nv","alias":"navlinks","background_transparency":"1","position":"{0.5,0},{0.5,0}","anchor":"0.5,0.5","size":"auto_x","height":"{0,32}",
         "children":[
          {"class":"UIListLayout","globalid":"nl","direction":"Horizontal","padding":"0,28","sort":"LayoutOrder","alignment_vertical":"Center"},
          {"class":"TextButton?link","globalid":"n1","alias":"navfeatures","order":"1","href":"nimbus.rbx","new_tab":"false","text":"Features","font":"BuilderSansMedium","font_size":"14","font_color":"#adadad","align_x":"Center","align_y":"Center","auto_color":"true","background_transparency":"1","size":"auto_x","height":"{1,0}"},
          {"class":"TextButton?link","globalid":"n2","alias":"navpricing","order":"2","href":"nimbus.rbx/pricing","new_tab":"false","text":"Pricing","font":"BuilderSansMedium","font_size":"14","font_color":"#adadad","align_x":"Center","align_y":"Center","auto_color":"true","background_transparency":"1","size":"auto_x","height":"{1,0}"},
          {"class":"TextButton?link","globalid":"n3","alias":"navdocs","order":"3","href":"nimbus.rbx/docs","new_tab":"false","text":"Docs","font":"BuilderSansMedium","font_size":"14","font_color":"#adadad","align_x":"Center","align_y":"Center","auto_color":"true","background_transparency":"1","size":"auto_x","height":"{1,0}"}
         ]},
        {"class":"TextButton?link","globalid":"hc","alias":"headercta","href":"nimbus.rbx/signup","new_tab":"false","text":"Sign up","font":"BuilderSansMedium","font_size":"14","font_color":"#ffffff","align_x":"Center","align_y":"Center","auto_color":"true","background_color":"#4e9bff","background_transparency":"0",
         "position":"{1,0},{0.5,0}","anchor":"1,0.5","size":"auto",
         "children":[
          {"class":"UICorner","globalid":"hr","radius":"0,8"},
          {"class":"UIPadding","globalid":"hq","left":"0,14","right":"0,14","top":"0,7","bottom":"0,7"}
         ]}
       ]},

      {"class":"ScrollingFrame","globalid":"bd","alias":"body","canvassize":"auto_y","scrollbar_thickness":"6","scrollbar_color":"#262629","scrollbar_transparency":"0","background_transparency":"1",
       "position":"{0,0},{0,56}","size":"{1,0},{1,-56}",
       "children":[
        {"class":"Frame","globalid":"cl","alias":"column","background_transparency":"1","position":"{0.5,0},{0,0}","anchor":"0.5,0","size":"auto_y","width":"{1,0}",
         "children":[
          {"class":"UISizeConstraint","globalid":"cz","min_size":"0,0","max_size":"1080,inf"},
          {"class":"UIListLayout","globalid":"cy","direction":"Vertical","padding":"0,56","sort":"LayoutOrder","alignment_horizontal":"Center"},
          {"class":"UIPadding","globalid":"cp","top":"0,64","bottom":"0,40","left":"0,24","right":"0,24"},

          {"class":"Frame","globalid":"he","alias":"hero","order":"1","background_transparency":"1","size":"auto_y","width":"{1,0}",
           "children":[
            {"class":"UIListLayout","globalid":"hl","direction":"Vertical","padding":"0,16","sort":"LayoutOrder","alignment_horizontal":"Center"},
            {"class":"TextLabel","globalid":"hb","alias":"herobadge","order":"1","text":"Now with offline sync","font":"BuilderSansMedium","font_size":"12","font_color":"#8fc0ff","align_x":"Center","align_y":"Center","background_color":"#4e9bff","background_transparency":"0.85","size":"auto",
             "children":[
              {"class":"UICorner","globalid":"bc","radius":"1,0"},
              {"class":"UIPadding","globalid":"bp","left":"0,10","right":"0,10","top":"0,4","bottom":"0,4"}
             ]},
            {"class":"TextLabel","globalid":"ht","alias":"herotitle","order":"2","text":"Notes that keep up with you","font":"BuilderSansBold","font_size":"34","font_color":"#f2f2f3","align_x":"Center","align_y":"Center","wrap":"true","background_transparency":"1","size":"auto_y","width":"{1,0}"},
            {"class":"TextLabel","globalid":"hu","alias":"herosub","order":"3","text":"Write, sort and find everything in one fast workspace. Free to start.","font":"BuilderSans","font_size":"15","font_color":"#adadad","align_x":"Center","align_y":"Center","wrap":"true","background_transparency":"1","size":"auto_y","width":"{0,520}"},
            {"class":"Frame","globalid":"ha","alias":"heroactions","order":"4","background_transparency":"1","size":"auto",
             "children":[
              {"class":"UIListLayout","globalid":"al","direction":"Horizontal","padding":"0,12","sort":"LayoutOrder"},
              {"class":"TextButton?link","globalid":"ca","alias":"ctaprimary","order":"1","href":"nimbus.rbx/signup","new_tab":"false","text":"Start for free","font":"BuilderSansMedium","font_size":"14","font_color":"#ffffff","align_x":"Center","align_y":"Center","auto_color":"true","background_color":"#4e9bff","background_transparency":"0","size":"auto",
               "children":[
                {"class":"UICorner","globalid":"c1","radius":"0,8"},
                {"class":"UIPadding","globalid":"c2","left":"0,18","right":"0,18","top":"0,10","bottom":"0,10"}
               ]},
              {"class":"TextButton?link","globalid":"cb","alias":"ctasecondary","order":"2","href":"nimbus.rbx/docs","new_tab":"false","text":"Read the docs","font":"BuilderSansMedium","font_size":"14","font_color":"#f2f2f3","align_x":"Center","align_y":"Center","auto_color":"true","background_color":"#16181a","background_transparency":"0","size":"auto",
               "children":[
                {"class":"UICorner","globalid":"c3","radius":"0,8"},
                {"class":"UIStroke","globalid":"c4","stroke_color":"#262629","stroke_thickness":"1"},
                {"class":"UIPadding","globalid":"c5","left":"0,18","right":"0,18","top":"0,10","bottom":"0,10"}
               ]}
             ]}
           ]},

          {"class":"Frame","globalid":"fe","alias":"features","order":"2","background_transparency":"1","size":"auto_y","width":"{1,0}",
           "children":[
            {"class":"UIListLayout","globalid":"fl","direction":"Vertical","padding":"0,20","sort":"LayoutOrder"},
            {"class":"TextLabel","globalid":"ft","alias":"featurestitle","order":"1","text":"Everything in one place","font":"BuilderSansBold","font_size":"22","font_color":"#f2f2f3","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,30}"},
            {"class":"Frame","globalid":"fg","alias":"featuregrid","order":"2","background_transparency":"1","size":"auto_y","width":"{1,0}",
             "children":[
              {"class":"UIGridLayout","globalid":"gl","size":"{0.333,-14},{0,160}","padding":"0,20","sort":"LayoutOrder","alignment_horizontal":"Left","alignment_vertical":"Top"},

              {"class":"Frame","globalid":"f1","alias":"featuresearch","order":"1","background_color":"#16181a","background_transparency":"0",
               "children":[
                {"class":"UICorner","globalid":"f1r","radius":"0,10"},
                {"class":"UIStroke","globalid":"f1s","stroke_color":"#262629","stroke_thickness":"1"},
                {"class":"UIPadding","globalid":"f1p","top":"0,20","bottom":"0,20","left":"0,20","right":"0,20"},
                {"class":"UIListLayout","globalid":"f1l","direction":"Vertical","padding":"0,10","sort":"LayoutOrder"},
                {"class":"ImageLabel","globalid":"f1i","alias":"searchicon","order":"1","image":"rbxassetid://98819316845453","image_id":"98819316845453","image_color":"#4e9bff","scale_type":"Fit","background_transparency":"1","size":"{0,24},{0,24}"},
                {"class":"TextLabel","globalid":"f1t","alias":"searchtitle","order":"2","text":"Instant search","font":"BuilderSansBold","font_size":"16","font_color":"#f2f2f3","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,20}"},
                {"class":"TextLabel","globalid":"f1b","alias":"searchbody","order":"3","text":"Find any note in milliseconds, even across thousands of pages.","font":"BuilderSans","font_size":"13","font_color":"#adadad","align_x":"Left","align_y":"Top","wrap":"true","background_transparency":"1","size":"auto_y","width":"{1,0}"}
               ]},

              {"class":"Frame","globalid":"f2","alias":"featureprivate","order":"2","background_color":"#16181a","background_transparency":"0",
               "children":[
                {"class":"UICorner","globalid":"f2r","radius":"0,10"},
                {"class":"UIStroke","globalid":"f2s","stroke_color":"#262629","stroke_thickness":"1"},
                {"class":"UIPadding","globalid":"f2p","top":"0,20","bottom":"0,20","left":"0,20","right":"0,20"},
                {"class":"UIListLayout","globalid":"f2l","direction":"Vertical","padding":"0,10","sort":"LayoutOrder"},
                {"class":"ImageLabel","globalid":"f2i","alias":"privateicon","order":"1","image":"rbxassetid://99601667182985","image_id":"99601667182985","image_color":"#4e9bff","scale_type":"Fit","background_transparency":"1","size":"{0,24},{0,24}"},
                {"class":"TextLabel","globalid":"f2t","alias":"privatetitle","order":"2","text":"Private by default","font":"BuilderSansBold","font_size":"16","font_color":"#f2f2f3","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,20}"},
                {"class":"TextLabel","globalid":"f2b","alias":"privatebody","order":"3","text":"Your notes stay yours. Lock any page with one click.","font":"BuilderSans","font_size":"13","font_color":"#adadad","align_x":"Left","align_y":"Top","wrap":"true","background_transparency":"1","size":"auto_y","width":"{1,0}"}
               ]},

              {"class":"Frame","globalid":"f3","alias":"featuresync","order":"3","background_color":"#16181a","background_transparency":"0",
               "children":[
                {"class":"UICorner","globalid":"f3r","radius":"0,10"},
                {"class":"UIStroke","globalid":"f3s","stroke_color":"#262629","stroke_thickness":"1"},
                {"class":"UIPadding","globalid":"f3p","top":"0,20","bottom":"0,20","left":"0,20","right":"0,20"},
                {"class":"UIListLayout","globalid":"f3l","direction":"Vertical","padding":"0,10","sort":"LayoutOrder"},
                {"class":"ImageLabel","globalid":"f3i","alias":"syncicon","order":"1","image":"rbxassetid://122404692422803","image_id":"122404692422803","image_color":"#4e9bff","scale_type":"Fit","background_transparency":"1","size":"{0,24},{0,24}"},
                {"class":"TextLabel","globalid":"f3t","alias":"synctitle","order":"2","text":"Syncs everywhere","font":"BuilderSansBold","font_size":"16","font_color":"#f2f2f3","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,20}"},
                {"class":"TextLabel","globalid":"f3b","alias":"syncbody","order":"3","text":"Pick up on any device right where you left off.","font":"BuilderSans","font_size":"13","font_color":"#adadad","align_x":"Left","align_y":"Top","wrap":"true","background_transparency":"1","size":"auto_y","width":"{1,0}"}
               ]}
             ]}
           ]},

          {"class":"Frame","globalid":"pr","alias":"pricing","order":"3","background_transparency":"1","size":"auto_y","width":"{1,0}",
           "children":[
            {"class":"UIListLayout","globalid":"pl","direction":"Vertical","padding":"0,20","sort":"LayoutOrder","alignment_horizontal":"Center"},
            {"class":"TextLabel","globalid":"pt","alias":"pricingtitle","order":"1","text":"Simple pricing","font":"BuilderSansBold","font_size":"22","font_color":"#f2f2f3","align_x":"Center","align_y":"Center","background_transparency":"1","size":"{1,0},{0,30}"},
            {"class":"Frame","globalid":"tg","alias":"billingtoggle","order":"2","background_color":"#16181a","background_transparency":"0","size":"auto",
             "children":[
              {"class":"UICorner","globalid":"tr","radius":"1,0"},
              {"class":"UIPadding","globalid":"tp","left":"0,4","right":"0,4","top":"0,4","bottom":"0,4"},
              {"class":"UIListLayout","globalid":"tl","direction":"Horizontal","padding":"0,4","sort":"LayoutOrder"},
              {"class":"TextButton","globalid":"bm","alias":"billmonthly","order":"1","text":"Monthly","font":"BuilderSansMedium","font_size":"13","font_color":"#f2f2f3","align_x":"Center","align_y":"Center","auto_color":"true","background_color":"#262629","background_transparency":"0","size":"auto",
               "children":[
                {"class":"UICorner","globalid":"bmr","radius":"1,0"},
                {"class":"UIPadding","globalid":"bmp","left":"0,14","right":"0,14","top":"0,6","bottom":"0,6"}
               ]},
              {"class":"TextButton","globalid":"by","alias":"billyearly","order":"2","text":"Yearly","font":"BuilderSansMedium","font_size":"13","font_color":"#f2f2f3","align_x":"Center","align_y":"Center","auto_color":"true","background_color":"#262629","background_transparency":"1","size":"auto",
               "children":[
                {"class":"UICorner","globalid":"byr","radius":"1,0"},
                {"class":"UIPadding","globalid":"byp","left":"0,14","right":"0,14","top":"0,6","bottom":"0,6"}
               ]}
             ]},
            {"class":"Frame","globalid":"pc","alias":"plancards","order":"3","background_transparency":"1","size":"auto_y","width":"{1,0}",
             "children":[
              {"class":"UIListLayout","globalid":"pcl","direction":"Horizontal","padding":"0,20","sort":"LayoutOrder","alignment_horizontal":"Center"},

              {"class":"Frame","globalid":"p1","alias":"planfree","order":"1","background_color":"#16181a","background_transparency":"0","size":"auto_y","width":"{0,300}",
               "children":[
                {"class":"UICorner","globalid":"p1r","radius":"0,12"},
                {"class":"UIStroke","globalid":"p1s","stroke_color":"#262629","stroke_thickness":"1"},
                {"class":"UIPadding","globalid":"p1p","top":"0,24","bottom":"0,24","left":"0,24","right":"0,24"},
                {"class":"UIListLayout","globalid":"p1l","direction":"Vertical","padding":"0,8","sort":"LayoutOrder"},
                {"class":"TextLabel","globalid":"p1n","alias":"freename","order":"1","text":"Free","font":"BuilderSansBold","font_size":"16","font_color":"#f2f2f3","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,22}"},
                {"class":"TextLabel","globalid":"p1c","alias":"freeprice","order":"2","text":"0 R$","font":"BuilderSansBold","font_size":"30","font_color":"#f2f2f3","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,40}"},
                {"class":"TextLabel","globalid":"p1d","alias":"freenote","order":"3","text":"Up to 100 notes","font":"BuilderSans","font_size":"13","font_color":"#adadad","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,18}"}
               ]},

              {"class":"Frame","globalid":"p2","alias":"planpro","order":"2","background_color":"#16181a","background_transparency":"0","size":"auto_y","width":"{0,300}",
               "children":[
                {"class":"UICorner","globalid":"p2r","radius":"0,12"},
                {"class":"UIStroke","globalid":"p2s","stroke_color":"#4e9bff","stroke_thickness":"1"},
                {"class":"UIGradient","globalid":"p2g","gradient_color":"[[0,\"1b2433\"],[1,\"16181a\"]]","rotation":"90"},
                {"class":"UIShadow","globalid":"p2h","shadow_color":"#000000","shadow_transparency":"0.6","shadow_offset":"{0,0},{0,6}","shadow_spread":"{0,2},{0,2}","blur_radius":"0,16"},
                {"class":"UIPadding","globalid":"p2p","top":"0,24","bottom":"0,24","left":"0,24","right":"0,24"},
                {"class":"UIListLayout","globalid":"p2l","direction":"Vertical","padding":"0,8","sort":"LayoutOrder"},
                {"class":"TextLabel","globalid":"p2n","alias":"proname","order":"1","text":"Pro","font":"BuilderSansBold","font_size":"16","font_color":"#4e9bff","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,22}"},
                {"class":"TextLabel","globalid":"pp","alias":"proprice","order":"2","text":"99 R$ / month","font":"BuilderSansBold","font_size":"30","font_color":"#f2f2f3","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,40}"},
                {"class":"TextLabel","globalid":"p2d","alias":"pronote","order":"3","text":"Unlimited notes and offline sync","font":"BuilderSans","font_size":"13","font_color":"#adadad","align_x":"Left","align_y":"Center","background_transparency":"1","size":"{1,0},{0,18}"}
               ]}
             ]}
           ]},

          {"class":"TextLabel","globalid":"fo","alias":"footer","order":"4","text":"Nimbus. Made in CatWeb.","font":"BuilderSans","font_size":"12","font_color":"#787878","align_x":"Center","align_y":"Center","background_transparency":"1","size":"{1,0},{0,24}"}
         ]}
       ]},

      {"class":"script","globalid":"sc","alias":"logic","enabled":"true",
       "content":[
        {"id":"1","text":["When (bm)",{"value":"bm","t":"object","l":"button"},"pressed..."],"globalid":"e1","x":"4900","y":"4900","width":"350",
         "actions":[
          {"id":"10","text":["Set (pp)",{"value":"pp","t":"object"},"text to (99 R$ / month)",{"value":"99 R$ / month","t":"string"}],"globalid":"a1"},
          {"id":"31","text":["Set (Background Transparency)",{"value":"Background Transparency","t":"string","l":"property"},"of (bm)",{"value":"bm","t":"object"},"to (0)",{"value":"0","t":"any"}],"globalid":"a2"},
          {"id":"31","text":["Set (Background Transparency)",{"value":"Background Transparency","t":"string","l":"property"},"of (by)",{"value":"by","t":"object"},"to (1)",{"value":"1","t":"any"}],"globalid":"a3"}
         ]},
        {"id":"1","text":["When (by)",{"value":"by","t":"object","l":"button"},"pressed..."],"globalid":"e2","x":"4900","y":"5150","width":"350",
         "actions":[
          {"id":"10","text":["Set (pp)",{"value":"pp","t":"object"},"text to (999 R$ / year)",{"value":"999 R$ / year","t":"string"}],"globalid":"b1"},
          {"id":"31","text":["Set (Background Transparency)",{"value":"Background Transparency","t":"string","l":"property"},"of (by)",{"value":"by","t":"object"},"to (0)",{"value":"0","t":"any"}],"globalid":"b2"},
          {"id":"31","text":["Set (Background Transparency)",{"value":"Background Transparency","t":"string","l":"property"},"of (bm)",{"value":"bm","t":"object"},"to (1)",{"value":"1","t":"any"}],"globalid":"b3"}
         ]},
        {"id":"3","text":["When mouse enters (ca)",{"value":"ca","t":"object"},"..."],"globalid":"e3","x":"5300","y":"4900","width":"350",
         "actions":[
          {"id":"88","text":["Tween (Background Color)",{"value":"Background Color","t":"string","l":"property"},"of (ca)",{"value":"ca","t":"object"},"to (6aacff)",{"value":"6aacff","t":"any"},"- (0.15)",{"value":"0.15","t":"number","l":"time"},{"value":"Sine","t":"string","l":"style"},{"value":"Out","t":"string","l":"direction"}],"globalid":"c6"}
         ]},
        {"id":"5","text":["When mouse leaves (ca)",{"value":"ca","t":"object"},"..."],"globalid":"e4","x":"5300","y":"5150","width":"350",
         "actions":[
          {"id":"88","text":["Tween (Background Color)",{"value":"Background Color","t":"string","l":"property"},"of (ca)",{"value":"ca","t":"object"},"to (4e9bff)",{"value":"4e9bff","t":"any"},"- (0.15)",{"value":"0.15","t":"number","l":"time"},{"value":"Sine","t":"string","l":"style"},{"value":"Out","t":"string","l":"direction"}],"globalid":"c7"}
         ]}
       ]}
     ]}
  ]
}
```

## Notes for adapting it

- **Swap the content, keep the skeleton.** Change the palette, copy, icons and section count to fit the brief. The header → scrolling body → centred column → stacked sections structure works for almost any landing page.
- **More sections:** add a `Frame` to the column with the next `order` number. Nothing else needs to move.
- **More feature cards:** add another card to `featuregrid` with the next `order`. Rows wrap automatically; change the grid's `size` to `"{0.5,-10},{0,160}"` for two per row.
- **Responsive header:** this example keeps the header simple. For a menu button that replaces the links on narrow screens, use the §6 pattern.
- **Prices are text, not purchases.** To sell something, make the button a `TextButton?transfer` with a real `product` ID (§2.4). Never invent one.
- **Every globalid is unique** across the whole file, including inside the script. If you merge this with other examples, re-check that.
