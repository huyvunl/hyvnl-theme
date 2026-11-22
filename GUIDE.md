# The hyvnl look: a guide

This is how all my websites look and behave: hyvnl.com, and every site after it. Each site is its own repo and keeps its own copy of `site/theme.css` from here.

Version: see the first line of `site/theme.css`. Changes are listed at the end. To see everything at a glance, open the specimen page (section 10).

## 1. The concept

**Ink on paper.** A warm off-white page, soft black and grey text, one small title in the corner, a quiet menu in the other corner, and a lot of room in between. Four Japanese ideas carry it:

| Idea | In one line | Carried out by |
|---|---|---|
| **ma** | the empty space is the design | two small corners, an empty middle, one line |
| **kanso** | leave out what the page can do without | no scripts, nothing downloaded, three links at most |
| **seijaku** | nothing moves until you touch it | nothing animates at rest; links only fade slowly when touched |
| **shibui** | quiet, never loud | grey on paper, lowercase, one small accent |

## 2. Principles

1. **Empty space is the design.** Add something only when the page can't work without it.
2. **Ink on paper.** Paper, ink, grey and one hairline. One accent, the stamp, never used for text. No dark mode.
3. **Nothing moves until you touch it.** No animation at rest. Movement stops when the device asks for less.
4. **Fonts already on the device.** Japanese-style serifs, nothing downloaded.
5. **Nothing needs a script.** Menus and the lock use what browsers already do. The one exception a site may make is its own small script for the editor (section 4), on the pages that hold one.
6. **Danish, lowercase, short.** On the pages, words are few and quiet.
7. **Every site keeps the security baseline** (section 8).

## 3. Tokens

Tokens are the named values in `theme.css`. Use the name, never the raw value, so every site stays in step.

| Token | Value | Job |
|---|---|---|
| `--paper` | `#f6f4ef` | page background, fold-out background |
| `--ink` | `#2b2b2b` | main text, corner title, `…`, hover, focus outline |
| `--grey` | `#6b6b6b` | links, centred line, body text, lock |
| `--hairline` | `#d6d3cb` | thin border of the fold-out, selected text |
| `--stamp-blue` | `#8fa7bf` | the stamp's faded blue dot |
| `--stamp-lime` | `rgba(200, 230, 90, 0.55)` | the see-through lime dot inside the stamp |
| `--paper-spring` | `#f7f3f0` | spring paper (section 4) |
| `--paper-summer` | `#f3f4f1` | summer paper |
| `--paper-autumn` | `#f4efe4` | autumn paper |
| `--paper-winter` | `#f2f2f0` | winter paper |
| `--font` | Hiragino Mincho, Yu Mincho, Georgia, serif | all text |
| `--size-title` | `1rem` | corner title |
| `--size-menu` | `0.8rem` | menu links, lists |
| `--size-text` | `0.85rem` | centred line, body text |
| `--size-more` | `1.1rem` | the `…` |
| `--size-input` | `16px` | text fields (smaller makes iPhones zoom in) |
| `--size-arrow` | `18px` | the `←` (deprecated in 1.6.0) |
| `--size-stamp` | `12px` | the stamp |
| `--edge-top` | `12px` | gap above the corner title and the menu |
| `--edge-left` | `24px` | gap left of the corner title, right of the stamp |
| `--edge-right` | `12px` | gap right of the menu |
| `--edge-bottom` | `24px` | gap below the stamp |
| `--tap` | `44px` | smallest tap area |
| `--gutter` | `16px` | side padding of the centre |
| `--column` | `22rem` | width of a left-aligned column (log, title, meta, prose, form) |
| `--ink-fade` | `0.6s` | how slowly a link turns from grey to ink |

The phone switch at 600px is written out in `theme.css` and isn't a token, because CSS doesn't allow variables inside `@media`.

To change a value for one site only, set the token in that site's `site.css` (see section 9). Never edit the site's copy of `theme.css`.

## 4. Pieces

Copy the HTML as it is, then change the words.

### Corner title

The site's name, top left, semi-bold, on every page, as a link to the front page (the front page too, so it looks and works the same everywhere). It is how a visitor gets home, so pages need no `←`.

```html
<a class="name" href="/">sidenavn</a>
<h1 class="visually-hidden">link et</h1>
```

Every page still needs exactly one `h1`, the page's own name, for screen readers. If the page shows its title (`.title`, see Title and meta), that is the `h1`. If it doesn't (a front page, a short page, a list, a log, the not-found page), add a visually hidden `h1` right after the corner title, as above.

- Do: keep it short, one or two words.
- Don't: make it bigger or add a logo. The empty space carries it.

It sits inside `<main>` but is placed in the corner by the style. (Before 1.6.0 the corner held the page's name as a plain `<h1 class="name">`; that still works and looks the same.)

### Menu with dots and "…"

Top right. Up to three links inline with `·` between them, and the rest behind `…`. On a phone (narrower than 600px) only `…` shows, and its list also holds the inline links (`class="phone-only"`). Mark the current page with `aria-current="page"` in both places: it shows in ink with a thin underline. A side link (`.menu-side`) gets it too, on its own page and the pages under it.

```html
<nav class="menu" aria-label="Menu">
  <ul class="menu-links">
    <li><a href="/et">link et</a></li>
    <li><span class="dot" aria-hidden="true">·</span><a href="/to">link to</a></li>
    <li><span class="dot" aria-hidden="true">·</span><a href="/tre">link tre</a></li>
  </ul>
  <details class="more">
    <summary aria-label="Flere links">…</summary>
    <ul>
      <li class="phone-only"><a href="/et">link et</a></li>
      <li class="phone-only"><a href="/to">link to</a></li>
      <li class="phone-only"><a href="/tre">link tre</a></li>
      <li><a href="/fire">link fire</a></li>
      <li><a href="/fem">link fem</a></li>
    </ul>
  </details>
</nav>
```

- Do: keep three links inline at most.
- Don't: replace `<details>` with a script. It opens and closes on its own. (Clicking elsewhere doesn't close it, and that's accepted.)

### Centre and centred line

Everything that isn't in a corner goes in `<main class="center">`, centred across and down the screen. A front page usually holds just one quiet line.

```html
<main class="center">
  <a class="name" href="/">sidenavn</a>
  <h1 class="visually-hidden">sidenavn</h1>
  <p class="line">en stille linje</p>
</main>
```

- Do: one line, lowercase.
- Don't: stack several lines or headings in the middle.

### Body text

A short grey paragraph, never wider than 26em. Several paragraphs get space between them on their own.

```html
<p class="text">En kort tekst.</p>
```

- Do: a few sentences on a short page; use the reading page (below) for more.
- Don't: add headings. If it needs headings, it needs a new design decision first.

### List

A quiet column of links, for example an index of notes.

```html
<ul class="list">
  <li><a href="/noter/en">første note</a></li>
  <li><a href="/noter/to">anden note</a></li>
</ul>
```

- Do: short link texts, lowercase.
- Don't: add dates next to the links (use the log).

### Reading page

For text longer than a few sentences: add `reading` to the centre, and the text starts high on the page instead of in the middle.

```html
<main class="center reading">
  <a class="name" href="/">sidenavn</a>
  <h1 class="visually-hidden">en tekst</h1>
  <p class="text">Første afsnit.</p>
  <p class="text">Andet afsnit.</p>
</main>
```

- Do: plain paragraphs.
- Don't: use it for a one-line page. Short pages stay centred.

### Back arrow (deprecated in 1.6.0)

Don't use it on new pages: the corner title links home and the menu shows where you are. The style stays until 2.0.0 so older pages look the same; when a site updates, it can delete its `<a class="back" …>←</a>` lines.

### Side link

One link at the start of the top-right corner, visible on phones too (`.menu-side`). Next to a menu it is the first child of the `<nav class="menu">`. Beside a lock, wrap both in `<div class="menu">` and write the link **after** the `<form class="lock">` (it is shown before it): a link inside the form would open the field when pressed and lose its click. It steps aside while the field is open.

```html
<div class="menu">
  <form class="lock" method="post" action="/unlock">…</form>
  <a class="menu-side" href="/log.html">noter</a>
</div>
```

- Do: one short word, lowercase.
- Don't: more than one side link.

### Title and meta

A page's own title in the column (`.title`), with a small grey line of facts under it (`.meta`), `·` between.

```html
<h1 class="title">en morgen</h1>
<p class="meta"><time datetime="2026-11-19">19 11 2026</time> · <a href="/log.html">rejser</a></p>
```

- Do: put the site's name in the corner (`.name`) and the page's title here, as the page's `h1`.
- Don't: more than one line of facts.

### Log

Grey dates next to ink titles (`.log`, `.log-date`). Copy the HTML from `site/log.html`.

```html
<ol class="log">
  <li><time class="log-date" datetime="2026-11-19">19 11 2026</time><a href="/post.html">en morgen</a></li>
</ol>
```

- Do: one line per entry, newest first.
- Don't: add descriptions under the titles.

### Add link

A small, quiet `+ word` just above a list, for those who may add to it, for example `+ skriv` above a log (`.add`). Like the pop-out `+` beside a title, but a plain link to its own page. Show it only to visitors who may use it; the server decides who that is.

```html
<a class="add" href="/ny">+ skriv</a>
<ol class="log">…</ol>
```

- Do: one short word after the `+`, lowercase.
- Don't: put it in the top-right corner; it belongs with the list it adds to.

### Prose

Longer text with headings (`h2`, `h3`), lists, emphasis and links (`.prose`). This is the design decision that "Body text" asks for before headings. Copy the HTML from `site/post.html`.

```html
<div class="prose">
  <p>Første afsnit.</p>
  <h2>en overskrift</h2>
  <p>Tekst med <em>kursiv</em>, <strong>fed</strong> og <a href="#">et link</a>.</p>
</div>
```

- Do: use it for a real text with parts.
- Don't: use it for a few sentences (use Body text).

### Form

Labels above fields, one quiet button and a `fortryd` link (`.form`, `.field-label`, `.field`, `.area`, `.hint`, `.notice`, `.actions`, `.button`). A wrong field gets `aria-invalid="true"`, `aria-describedby` and a `.notice` right under it. The site's own server code decides what happens with the form; the theme only gives the look. Copy the HTML from `site/form.html`.

```html
<form class="form" method="post" action="/gem">
  <label class="field-label" for="titel">titel</label>
  <input class="field" id="titel" name="titel" type="text" required>
  <div class="actions"><button class="button" type="submit">gem</button><a href="/log.html">fortryd</a></div>
</form>
```

- Do: a label for every field.
- Don't: placeholders instead of labels.

### Choices

Checkboxes in a group, with a small ink heading (`.choices`, `.choice`). Each box sits inside its own label, so the whole line takes the tap. It can sit inside a Form, before its `.actions`. Two forms in a row get room between them. Copy the HTML from `site/form.html`.

```html
<fieldset class="choices"><legend>vis på</legend>
  <label class="choice"><input type="checkbox" name="vis" value="forside" checked>forsiden</label>
  <label class="choice"><input type="checkbox" name="vis" value="noter">noter</label>
</fieldset>
```

- Do: short labels, lowercase; the legend says what the boxes are about.
- Don't: use it for one single yes/no (write one choice without a fieldset instead).

### Editor (look only)

A writing window for longer text: a quiet row of tools above an area that shows **bold**, *italic*, a heading, lists and links as they will look (`.editor`, `.editor-bar`, `.editor-tool`, `.editor-gap`, `.editor-link`, `.editor-area`). The theme only gives the look. **The site brings its own small script**, which builds the window in place of a `.area` and keeps the `.area` (hidden) for the form to send. With scripts off, the page is the plain `.area`, so a form with an editor always works without one.

The HTML the script builds:

```html
<div class="editor">
  <div class="editor-bar" role="toolbar" aria-label="formatering" aria-controls="tekst-vist">
    <button type="button" class="editor-tool tool-b" aria-label="fed" aria-pressed="false">F</button>
    <button type="button" class="editor-tool tool-i" aria-label="kursiv" aria-pressed="false">K</button>
    <span class="editor-gap" aria-hidden="true"></span>
    <button type="button" class="editor-tool" aria-label="overskrift" aria-pressed="false">Aa</button>
    <button type="button" class="editor-tool" aria-label="punktliste" aria-pressed="false">•</button>
    <button type="button" class="editor-tool" aria-label="nummereret liste" aria-pressed="false">1.</button>
    <span class="editor-gap" aria-hidden="true"></span>
    <button type="button" class="editor-tool is-word" aria-label="link" aria-pressed="false">link</button>
  </div>
  <div class="editor-link" hidden>
    <label for="adresse">adresse</label><input class="field" id="adresse" type="text" inputmode="url">
    <button type="button">ok</button><button type="button">fjern</button><button type="button" aria-label="luk">×</button>
  </div>
  <div class="editor-area" id="tekst-vist" contenteditable="true" role="textbox" aria-multiline="true" aria-labelledby="tekst-label"></div>
</div>
```

- A tool that is on gets `aria-pressed="true"`: ink, underlined.
- The tools are letters, like a Danish word processor (**F** fed, *K* kursiv), so the row fits one line even 320px wide. Every tool has a Danish `aria-label` and is at least 44×44px.
- The row stays at the top of the window while you scroll a long text (`position: sticky`).
- `[hidden]` now always hides, even on pieces that set their own `display` (for example the `.area` the script hides).
- Do: keep the tools to what the site can really store, and paste as plain text.
- Don't: add colours, fonts or sizes. Ink on paper.

### Wide page and head

A full-width page that starts top left, for an overview or a dashboard (`.wide` on `<main>` instead of `.center`). The corner title, menu and stamp work as on every page. `.head` puts something small beside the title, for example a pop-out `+`. Copy the HTML from `site/cards.html`.

```html
<main class="wide">
  <div class="head"><h1 class="title">oversigt</h1> … </div>
  <p class="meta">tre noter</p>
  …
</main>
```

- Do: keep it for pages that show many things side by side.
- Don't: use it for reading; text pages stay in the centre.

### Cards

A grid of equal boxes with a hairline frame (`.cards`, `.card`, `.card-name`, `.card-line`, `.card-label`, `.card-actions`). As many fit per row as there is room for (one on a phone), and every card is as tall as the tallest one, so the grid stays even. A card's own links or pop-outs sit on one line at the bottom. Copy the HTML from `site/cards.html`.

```html
<ul class="cards">
  <li class="card">
    <h2 class="card-name">en-morgen</h2>
    <p class="card-line"><span class="card-label">emner</span>rejser · te</p>
    <div class="card-actions"><a href="/post.html">åbn</a></div>
  </li>
</ul>
```

- Do: short lines; a semi-bold label, then grey values with ` · ` between.
- Don't: put long text in a card; it makes every card that tall.

### Toggles

Words that switch on and off (`.toggles`, `.toggle`), a quieter choice than checkboxes. Each word holds a real checkbox, hidden but still there, so it works without scripts, with the keyboard and with screen readers. On: ink with a line under it. Off: grey. Browsers older than 2023 show no difference between on and off, so use Choices where that matters. Copy the HTML from `site/cards.html`.

```html
<fieldset class="toggles"><legend>vises på</legend>
  <label class="toggle"><input type="checkbox" name="vis" value="forside" checked>forsiden</label>
  <label class="toggle"><input type="checkbox" name="vis" value="noter">noter</label>
</fieldset>
```

- Do: short words, lowercase; the legend says what they are about.
- Don't: mix toggles and checkboxes on one page.

### Pop-out

A word (or `+`) that opens a framed panel over the page, without scripts (`.pop`, `.pop-add` for a `+`, `.pop-panel`). Pressing the word again, or a `fortryd` link back to the page, closes it. Give every pop-out on a page the same `name`: then opening one closes the others (browsers from 2024; older ones simply leave them open). Inside `.head` the panel hangs under the title; inside `.card-actions` it is as wide as the card. An open panel covers what is under it until it is closed. Copy the HTML from `site/cards.html`.

```html
<details class="pop" name="kort"><summary aria-label="ret en-morgen">ret</summary><div class="pop-panel">
  <form class="form" method="post" action="/gem"> … </form>
</div></details>
```

- Do: a short form or one question per panel; an `aria-label` that names the thing it belongs to.
- Don't: put a pop-out inside a pop-out.

### Stamp

A small faded blue dot with a see-through lime dot resting low inside it, in the bottom-right corner, like a name stamp on a print. It is the theme's only colour. Put it as the last thing inside `<main class="center">`. On a long page it sits at the very end.

```html
<span class="stamp" aria-hidden="true"></span>
```

- Do: one stamp per page, always with `aria-hidden="true"` (it's decoration).

**Stamp as a link** (optional, 1.6.0). A site may make the stamp a quiet way in, for example to its lock. It looks exactly the same; an invisible 44×44px square around the dot takes the tap, so nothing moves, and it shows the ink outline when reached with Tab. Give it a short Danish `aria-label` that says what it does, and no `aria-hidden`:

```html
<a class="stamp" href="/laas" aria-label="lås op"></a>
```

- Don't: use its colours for text, links or anything that carries meaning.

### Site icon

The stamp is also the icon in the browser tab, in bookmarks and on a phone's home screen. Four files in `site/` (and three square twins, below):

- `favicon.ico`: a real ICO file holding two pictures, 16×16 and 32×32, each drawn on its own so the stamp stays crisp, on a clear background. Safari and older browsers look for this one first.
- `favicon-32.png`: the same drawing as a 32×32 picture on a clear background.
- `favicon.svg`: the stamp as two plain circles on a clear background, filling the whole icon. Same colours and shape as `.stamp`. Browsers that show SVG tab icons take this.
- `apple-touch-icon.png`: 180×180 for phones and for Safari's Favorites and start page. Apple expects an opaque square (iOS may fill anything see-through with a solid colour), and rounds the corners itself. So it is a full-bleed square of the stamp's blue `#8fa7bf` with the lime dot in the middle: it reads as the stamp and has no light square around it. Tabs never use it; they use the clear icons above.

Put these four lines in every page's `<head>`, right after the theme, in this order:

```html
<link rel="icon" href="/favicon.ico" sizes="16x16 32x32">
<link rel="icon" href="/favicon-32.png" sizes="32x32" type="image/png">
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

- Order: ICO first, then PNG, then SVG. Browsers that can show SVG take the SVG; Safari takes what it can read from the first lines. No `mask-icon`: Safari dropped pinned-tab icons that need it.

- Do: serve the four files from the site's own address (the CSP's `img-src 'self'` allows them), with the headers from section 8, except caching: they hold nothing private, so let them be kept for a day (`Cache-Control: public, max-age=86400`). Safari keeps its own icon store and tends to skip icons sent with `no-store`. Send `favicon.ico` as `image/x-icon`.
- Safari draws every tab and Favorites icon on its own white tile, and it takes the SVG too (Safari 26 reads SVG icons), so a round icon shows white corners there. `site/` therefore also holds square twins of the three tab icons: `favicon-square.ico`, `favicon-square-32.png` and `favicon-square.svg`. They are the same stamp colours drawn as a full-bleed blue square with the lime dot, the same picture as the touch icon. A page can't tell Safari from other browsers, so the server does: when the browser is Safari (its `User-Agent` has `Version/…` and `Safari/…` and none of `Chrome`, `Chromium`, `CriOS`, `FxiOS`, `EdgiOS`, `Edg`, `OPR`, `OPiOS`, `Firefox`), the answers to `/favicon.ico`, `/favicon-32.png` and `/favicon.svg` are the square files; everyone else gets the round ones. Send `Vary: User-Agent` on those three answers, so no shared cache hands one browser the other's file. The `<link>` lines don't change. A site that doesn't care about Safari's white corners can skip the square files.
- Do: answer `/favicon.ico` with the ICO file itself (no redirect: browsers keep a redirect for a very long time).
- Don't: change their colours per site, or redraw one file without the others. Browsers keep icons a long time, so after a change a hard refresh, or clearing Safari's icon cache, may be needed to see it.

### Paper by season

Four slightly different papers. A site picks one by hand with a class on `<html>`; nothing switches by date, because that would need a script.

```html
<html lang="da" class="paper-autumn">
```

Classes: `paper-spring`, `paper-summer`, `paper-autumn`, `paper-winter`. Leave the class out for the normal paper.

- Do: change it when the season changes, if you like.
- Don't: mix papers on one site.

### Not found page

`site/404.html`: the corner title, `her er intet`, and a visually hidden `h1` (`ikke fundet`). The site's host must be set up to send it for wrong addresses (Python's preview server doesn't).

### Lock (look only)

A small grey lock in the menu's place. Clicking it turns it into a password field with a thin underline. The theme only gives the look. **The code that checks the password lives in each site's own server code**, never in this theme.

```html
<form class="menu lock" method="post" action="/unlock">
  <input id="adgangskode" class="lock-field" type="password" name="adgangskode" placeholder="adgangskode" aria-label="adgangskode" autocomplete="current-password">
  <label class="lock-icon" for="adgangskode" aria-hidden="true"><svg width="12" height="14" viewBox="0 0 16 18" fill="none" stroke="currentColor" stroke-width="1.2" focusable="false"><rect x="2" y="8" width="12" height="9" rx="1"/><path d="M4.5 8V5.5a3.5 3.5 0 0 1 7 0V8"/></svg></label>
  <button class="visually-hidden" type="submit">lås op</button>
</form>
```

Adding `data-open` to the form keeps the field open (for example after a wrong password).

`.lock` now lays itself out, so it can sit inside a `<div class="menu">` with a side link (see Side link); the old `<form class="menu lock">` still works.

- Do: let the server decide who gets in.
- Don't: hide pages with CSS or a script. Hidden is not locked.

### Visually hidden

Text only screen readers read, like the lock's `lås op` button.

```html
<button class="visually-hidden" type="submit">lås op</button>
```

### Quiet details (no HTML needed)

- **Slow ink:** links and the lock icon fade from grey to ink over `--ink-fade` when touched, instead of jumping.
- **Quiet selection:** selected text gets a hairline wash with ink text instead of the browser's blue.
- **Print:** a printed page shows only the title and the words, in black on white. Menu, lock, arrow, add link and stamp are left out.

## 5. Words

- Pages are Danish: `<html lang="da">`.
- Lowercase, short, calm. No exclamation marks.
- Screen-reader labels in Danish: `Menu`, `Flere links`, `lås op`.
- Page titles: `<page> · <site>`, for example `link et · sidenavn`. The front page is just the site name.
- The not-found line is `her er intet`.

## 6. Accessibility checklist

Check before publishing:

- [ ] Grey on paper is about 4.8:1, just above the 4.5:1 readability bar. Never use a lighter grey for text.
- [ ] On a seasonal paper, grey stays above the bar too: spring 4.83, summer 4.83, autumn 4.65, winter 4.75.
- [ ] Everything you tap is at least 44×44px (`--tap`).
- [ ] Links and `…` show an ink outline when reached with Tab.
- [ ] The current page is marked with `aria-current="page"` (underlined in the menu).
- [ ] Every page has exactly one `h1` (visible, or visually hidden after the corner title).
- [ ] Text fields are 16px (`--size-input`).
- [ ] The stamp has `aria-hidden="true"`, or is a link with an `aria-label`.
- [ ] Nothing scrolls sideways at 320px wide.
- [ ] Movement stops when the device asks for less motion (already in `theme.css`).
- [ ] **Click check:** the corner title, the menu links, `…`, the lock, an add link and a stamp link take clicks at 1280, 375 and 320px wide (see below).

**Click check.** Something invisible drawn on top of the menu can swallow its clicks while the page still looks right (that was the 1.1.0 bug). In the browser, set the width (developer tools → device toolbar), open the console and paste:

```js
[...document.querySelectorAll('a.name, .menu a, .menu summary, .lock-icon, .add, a.stamp, .button, .pop > summary, .editor-tool')]
  .filter(e => e.getClientRects().length)
  .map(e => { const r = e.getBoundingClientRect();
    const hit = document.elementFromPoint(r.x + r.width / 2, r.y + r.height / 2);
    return (e.textContent.trim() || e.getAttribute('aria-label') || 'lock') + (e.contains(hit) ? ': ok' : ': BLOCKED by ' + hit.tagName); })
```

Every line must end in `ok`. Open `…` and paste it again for the fold-out's links. Then really click: the corner title must go to the front page, the lock must open its field, and `…` must open its list. On a page with a side link beside the lock, really click the side link: it must open its page, not the field. Do it on every starter page and the specimen.

## 7. Starter pages

`site/` holds nine pages to copy. All of them carry the stamp and link the site icon (`favicon.ico`, `favicon-32.png`, `favicon.svg`, `apple-touch-icon.png`, see Site icon).

| File | What it is |
|---|---|
| `index.html` | front page: the site name and one quiet line |
| `page.html` | short page: a few sentences |
| `list.html` | list page: a column of links |
| `reading.html` | reading page: longer text, starting high |
| `404.html` | not found: `her er intet` |
| `log.html` | dated list, with `+ skriv` above it |
| `post.html` | a longer text with marks |
| `form.html` | a form |
| `cards.html` | an overview: a wide page with cards, toggles and pop-outs |

## 8. Security baseline

Every site keeps all of this.

- No scripts. No files from other websites (fonts, styles, images, scripts). No `style="…"` or `on…=` attributes. No `<style>` blocks: all styling is in `theme.css` and `site.css`. (The one exception: a site's own script file for the editor, below.)
- Every response carries these headers:

```
Strict-Transport-Security: max-age=86400
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
Content-Security-Policy: default-src 'self'; style-src 'self'; img-src 'self' data:; base-uri 'self'; form-action 'self'; frame-ancestors 'none'; object-src 'none'; script-src 'none'
```

`script-src 'none'` (new in 1.7.0) says it out loud: `default-src 'self'` alone would let the site's own scripts run. Add it to an older site's headers when you update it.

Pages behind a password also get `Cache-Control: no-store`.

In plain words: browsers only use https, don't guess file types, don't let other sites frame the page, send less to other sites, don't offer camera, microphone or location, only load anything from the site's own address, and run no scripts at all. The styles come from its own `/theme.css`, so `style-src 'self'` is enough.

**A page with an editor** (and only such a page) may run the site's own script file. Its CSP ends in `script-src 'self'; require-trusted-types-for 'script'; trusted-types 'none'` instead of `script-src 'none'`: only script files from the site's own address, nothing written inside the page, and no script may turn text into HTML. Every other page keeps `script-src 'none'`. Never add `'unsafe-inline'`, and never a script from another address.

- **If the site's server code builds its responses itself**, it must add the headers in that code; a host's headers file may not apply to them.
- If a site ever truly needs something from another address, change its CSP on purpose, and write down why in that site's docs.

Check a site's files with:

```bash
grep -rnE '<script|https?://|@import|url\(|style="|<style| on[a-z]+=' site/ | grep -v 'xmlns="http://www.w3.org/2000/svg"' || echo "clean"
```

(The second `grep` lets through `favicon.svg`'s `xmlns="http://www.w3.org/2000/svg"`. Every SVG file needs that label; it names the format and loads nothing.)

## 9. Start, update and change

### Start a new site

1. On GitHub, create an empty repo (github.com/new; no README, no .gitignore, no licence).
2. In the folder that holds `hyvnl-theme`, make the new site's folder next to it and start git:

```bash
mkdir ny-side && cd ny-side && git init -b main
```

3. Copy the starter:

```bash
cp -R ../hyvnl-theme/site ./site
```

4. Change the words: `<title>`, the corner title, the menu links, the lines and texts. Delete the starter pages you don't need.
5. Preview:

```bash
python3 -m http.server 8000 --directory site
```

Then open http://localhost:8000. (Double-clicking a file won't load the style, because `/theme.css` needs a server.)

6. Hosting: anything that serves the pages, `/theme.css`, `/favicon.ico`, `/favicon-32.png`, `/favicon.svg` and `/apple-touch-icon.png`, and adds the headers from section 8. If the host supports clean addresses, links can be `/side` instead of `/page.html`. Set the host to send `404.html` for wrong addresses.
7. Run the check in section 8 and the checklist in section 6, then publish the way that site's README says.

### Update a site

1. Read **Changes** below for every version since the site's copy (the site's version is the first line of its `site/theme.css`).
2. From the site's folder (next to `hyvnl-theme`), copy the new file over the old one:

```bash
cp ../hyvnl-theme/site/theme.css site/theme.css
```

3. Check the first line shows the new version:

```bash
head -1 site/theme.css
```

4. If the **first** number changed, make the HTML changes that Changes lists. If the middle number changed, new pieces are available, but nothing has to change.
5. Preview, run the checks, and publish the way that site's README says.

**What the numbers mean** (for example `1.2.0`):
- first number: something was renamed or removed, so pages may need changes
- middle number: something new was added, and old pages still work and look the same
- last number: a small fix

**A site's own extras** go in `site/site.css`, linked after the theme:

```html
<link rel="stylesheet" href="/theme.css">
<link rel="stylesheet" href="/site.css">
```

It can hold that site's own pieces, or a changed token, for example `:root { --edge-left: 32px; }`.

### Change the theme itself (in this repo)

1. Edit `site/theme.css`.
2. Raise the version in its first line.
3. Add a line under Changes. Update this guide if a piece changed.
4. Update the specimen page and its screenshots (section 10).
5. Preview the starter pages and the specimen.
6. Commit, then mark the version and push:

```bash
git tag v1.2.0
```

```bash
git push origin main v1.2.0
```

Then update each site, one at a time.

## 10. Specimen

`specimen/index.html` shows the whole theme on one page: the concept, colours, papers, type, space, every piece in each state, the starter pages, do/don't pairs, and computer next to phone. It uses the real `site/theme.css`, so it always shows the current version. `specimen/specimen.css` only lays out the page; sites never copy the `specimen/` folder.

Preview it from the repo's top folder:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000/specimen/.

The pictures in the README are screenshots of this page, in `specimen/screens/`. Take them again whenever the theme changes.

## 11. Ideas for later

Not in the theme yet. Each waits until a real page needs it.

- **hairline pause:** a short centred hairline between two parts of a page
- **one picture:** an image page with a small grey caption
- **facts:** labels and values, for example a contact page
- **specimen online:** showing the specimen page as a public website

Considered and left out: text set top-to-bottom as a margin accent, and a name seal (the stamp replaced it).

## 12. Changes

- **1.7.2** (2026-11-22): new: Safari-only square tab icons, `site/favicon-square.ico`, `site/favicon-square-32.png` and `site/favicon-square.svg` (a full-bleed blue square with the lime dot), because Safari draws round icons on a white tile. The server sends them instead of the round files when the browser is Safari (see Site icon); other browsers keep the round stamp. Nothing changes in the pages or the `<link>` lines. To get it in a site, copy the three files and add the server rule.
- **1.7.1** (2026-11-22): fix: the site icon in Safari and on light backgrounds. New `site/favicon.ico` (a real ICO with 16×16 and 32×32 pictures); `favicon-32.png` is redrawn with its metadata stripped; `apple-touch-icon.png` is now a full-bleed blue square with the lime dot, not the stamp on a paper-coloured square, so no light square shows in Safari's Favorites. The head now has four icon lines, ICO first (see Site icon), and the icon files should be cached for a day instead of `no-store`. Pages look the same. To get the fix in a site, copy the three changed files, add the ICO file and its `<link>` line, and give the icon files normal caching.
- **1.7.0** (2026-11-22): new: the editor (`.editor`, `.editor-bar`, `.editor-tool`, `.editor-gap`, `.editor-link`, `.editor-area`), the look of a writing window whose script the site brings itself; `[hidden]` now always hides. The security baseline now ends the CSP in `script-src 'none'`, and says what a page with an editor sends instead. Pages made for 1.6 look the same.
- **1.6.0** (2026-11-22): new: the corner title as a link home on every page (`a.name`, in ink like the plain title), with the page's own `h1` visible or visually hidden; the current page underlined in the menu (`aria-current="page"`); the add link (`.add`, a quiet `+ word` above a list); the stamp as a link (`a.stamp`: same look, an invisible 44px tap area, a focus outline). Deprecated: the back arrow (`.back`); the starter pages and the specimen no longer use it, and its style stays until 2.0.0. Two small look changes on existing pages: a current menu link is now underlined, and a corner title that is a link is now ink instead of grey. Nothing has to change in old pages.
- **1.5.0** (2026-11-21): new: the wide page and head (`.wide`, `.head`), cards (`.cards`, `.card` and its parts; equal heights), toggles (`.toggles`, `.toggle`: words that switch on and off) and the pop-out (`.pop`, `.pop-add`, `.pop-panel`), shown in a ninth starter page, `site/cards.html`, and the specimen. Pages made for 1.4 look the same.
- **1.4.0** (2026-11-19): new: the choices piece (checkboxes in a group, `.choices`, `.choice`), shown in `site/form.html` and the specimen, and room between two forms in a row (`.form + .form`). Pages made for 1.3 look the same.
- **1.3.0** (2026-11-19): new: side link, column, title, meta, log, prose and form pieces, the token --column, and three starter pages (log.html, post.html, form.html). .lock now lays itself out, so it can sit inside a <div class="menu">. Pages made for 1.2 look the same.
- **1.2.1** (2026-11-18): fix: a PNG backup for the tab icon, `site/favicon-32.png`, for browsers that can't show the SVG (some Safari versions). Linked before the SVG on every starter page and the specimen; `/favicon.ico` should now go to the PNG, not the SVG (see Site icon). Nothing looks different. To get it in a site, copy the file and add the PNG `<link>` line above the SVG one.
- **1.2.0** (2026-11-18): new: the site icon. The stamp as `site/favicon.svg` and `site/apple-touch-icon.png`, linked from every starter page and the specimen (see Site icon). Pages look the same; to get the icon in a site, copy the two files and add the two `<link>` lines.
- **1.1.1** (2026-11-18): fix: the menu links, `…` and the lock could not be clicked, because the centre (made positioned in 1.1.0 for the stamp) was drawn over the menu. The menu now sits above it (`z-index: 2`). Nothing looks different. New: the click check in section 6.
- **1.1.0** (2026-11-18): the concept, the stamp, slow ink, quiet selection, paper by season, print, the list and reading pieces, three new starter pages (`list.html`, `reading.html`, `404.html`), and the specimen page. Pages made for 1.0.0 look the same.
- **1.0.0** (2026-11-18): first version, taken from hyvnl.com as it looked on 2026-11-18.
