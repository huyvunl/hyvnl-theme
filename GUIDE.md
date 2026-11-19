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
5. **Nothing needs a script.** Menus and the lock use what browsers already do.
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
| `--size-arrow` | `18px` | the `←` |
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

The site's or page's name, top left, semi-bold. One per page, as the page's `h1`.

```html
<h1 class="name">sidenavn</h1>
```

- Do: keep it short, one or two words.
- Don't: make it bigger or add a logo. The empty space carries it.

It sits inside `<main class="center">` but is placed in the corner by the style.

### Menu with dots and "…"

Top right. Up to three links inline with `·` between them, and the rest behind `…`. On a phone (narrower than 600px) only `…` shows, and its list also holds the inline links (`class="phone-only"`). Mark the current page with `aria-current="page"` in both places.

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
  <h1 class="name">sidenavn</h1>
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
  <h1 class="name">en tekst</h1>
  <p class="text">Første afsnit.</p>
  <p class="text">Andet afsnit.</p>
  <a class="back" href="/" aria-label="Tilbage til forsiden">←</a>
</main>
```

- Do: plain paragraphs and the `←` at the end.
- Don't: use it for a one-line page. Short pages stay centred.

### Back arrow

A bare `←` back to the front page, under the text.

```html
<a class="back" href="/" aria-label="Tilbage til forsiden">←</a>
```

- Do: keep the `aria-label`, because screen readers can't say "←" usefully.
- Don't: add the word "tilbage" next to it.

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

- Do: put the site's name in the corner (`.name`) and the page's title here.
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

### Stamp

A small faded blue dot with a see-through lime dot resting low inside it, in the bottom-right corner, like a name stamp on a print. It is the theme's only colour. Put it as the last thing inside `<main class="center">`. On a long page it sits at the very end.

```html
<span class="stamp" aria-hidden="true"></span>
```

- Do: one stamp per page, always with `aria-hidden="true"` (it's decoration).
- Don't: use its colours for text, links or anything that carries meaning.

### Site icon

The stamp is also the icon in the browser tab, in bookmarks and on a phone's home screen. Three files in `site/`:

- `favicon.svg`: the stamp as two plain circles on a clear background, filling the whole icon so it reads at 16px. Same colours and shape as `.stamp`.
- `favicon-32.png`: the same drawing as a 32×32 picture on a clear background, for browsers that can't show an SVG tab icon (some Safari versions, older browsers).
- `apple-touch-icon.png`: 180×180 for phones. A home-screen icon can't be see-through, so the stamp sits on the paper colour `#f6f4ef`.

Put these three lines in every page's `<head>`, right after the theme, in this order:

```html
<link rel="icon" href="/favicon-32.png" sizes="32x32" type="image/png">
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
<link rel="apple-touch-icon" href="/apple-touch-icon.png">
```

- Order: the PNG line first, the SVG line after it. Browsers that can show SVG take the SVG (some take the last icon they can read, and the PNG's `sizes="32x32"` stops others from preferring it); the rest skip the SVG and use the PNG.

- Do: serve all three files from the site's own address (the CSP's `img-src 'self'` allows them), with the headers from section 8.
- Do: send browsers asking for the old `/favicon.ico` to `/favicon-32.png` (a redirect, or answer it with the PNG), so they don't get a 404. Not to the SVG: browsers that ask for `.ico` can't read SVG.
- Don't: change their colours per site, or redraw one file without the others. Browsers keep icons a long time, so after a change a hard refresh may be needed to see it.

### Paper by season

Four slightly different papers. A site picks one by hand with a class on `<html>`; nothing switches by date, because that would need a script.

```html
<html lang="da" class="paper-autumn">
```

Classes: `paper-spring`, `paper-summer`, `paper-autumn`, `paper-winter`. Leave the class out for the normal paper.

- Do: change it when the season changes, if you like.
- Don't: mix papers on one site.

### Not found page

`site/404.html`: the site name, `her er intet`, and the `←`. The site's host must be set up to send it for wrong addresses (Python's preview server doesn't).

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
- **Print:** a printed page shows only the title and the words, in black on white. Menu, lock, arrow and stamp are left out.

## 5. Words

- Pages are Danish: `<html lang="da">`.
- Lowercase, short, calm. No exclamation marks.
- Screen-reader labels in Danish: `Menu`, `Flere links`, `Tilbage til forsiden`, `lås op`.
- Page titles: `<page> · <site>`, for example `link et · sidenavn`. The front page is just the site name.
- The not-found line is `her er intet`.

## 6. Accessibility checklist

Check before publishing:

- [ ] Grey on paper is about 4.8:1, just above the 4.5:1 readability bar. Never use a lighter grey for text.
- [ ] On a seasonal paper, grey stays above the bar too: spring 4.83, summer 4.83, autumn 4.65, winter 4.75.
- [ ] Everything you tap is at least 44×44px (`--tap`).
- [ ] Links and `…` show an ink outline when reached with Tab.
- [ ] The current page is marked with `aria-current="page"`.
- [ ] Text fields are 16px (`--size-input`).
- [ ] The stamp has `aria-hidden="true"`.
- [ ] Nothing scrolls sideways at 320px wide.
- [ ] Movement stops when the device asks for less motion (already in `theme.css`).
- [ ] **Click check:** the menu links, `…` and the lock take clicks at 1280, 375 and 320px wide (see below).

**Click check.** Something invisible drawn on top of the menu can swallow its clicks while the page still looks right (that was the 1.1.0 bug). In the browser, set the width (developer tools → device toolbar), open the console and paste:

```js
[...document.querySelectorAll('.menu a, .menu summary, .lock-icon, .button')]
  .filter(e => e.getClientRects().length)
  .map(e => { const r = e.getBoundingClientRect();
    const hit = document.elementFromPoint(r.x + r.width / 2, r.y + r.height / 2);
    return (e.textContent.trim() || 'lock') + (e.contains(hit) ? ': ok' : ': BLOCKED by ' + hit.tagName); })
```

Every line must end in `ok`. Open `…` and paste it again for the fold-out's links. Then really click: the lock must open its field, and `…` must open its list. On a page with a side link beside the lock, really click the side link: it must open its page, not the field. Do it on every starter page and the specimen.

## 7. Starter pages

`site/` holds eight pages to copy. All of them carry the stamp and link the site icon (`favicon-32.png`, `favicon.svg`, `apple-touch-icon.png`, see Site icon).

| File | What it is |
|---|---|
| `index.html` | front page: the site name and one quiet line |
| `page.html` | short page: a few sentences and `←` |
| `list.html` | list page: a column of links and `←` |
| `reading.html` | reading page: longer text, starting high |
| `404.html` | not found: `her er intet` and `←` |
| `log.html` | dated list |
| `post.html` | a longer text with marks |
| `form.html` | a form |

## 8. Security baseline

Every site keeps all of this.

- No scripts. No files from other websites (fonts, styles, images, scripts). No `style="…"` or `on…=` attributes. No `<style>` blocks: all styling is in `theme.css` and `site.css`.
- Every response carries these headers:

```
Strict-Transport-Security: max-age=86400
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
Content-Security-Policy: default-src 'self'; style-src 'self'; img-src 'self' data:; base-uri 'self'; form-action 'self'; frame-ancestors 'none'; object-src 'none'
```

Pages behind a password also get `Cache-Control: no-store`.

In plain words: browsers only use https, don't guess file types, don't let other sites frame the page, send less to other sites, don't offer camera, microphone or location, and only load anything from the site's own address. The styles come from its own `/theme.css`, so `style-src 'self'` is enough.

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

6. Hosting: anything that serves the pages, `/theme.css`, `/favicon-32.png`, `/favicon.svg` and `/apple-touch-icon.png`, and adds the headers from section 8. If the host supports clean addresses, links can be `/side` instead of `/page.html`. Set the host to send `404.html` for wrong addresses.
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

- **1.3.0** (2026-11-19): new: side link, column, title, meta, log, prose and form pieces, the token --column, and three starter pages (log.html, post.html, form.html). .lock now lays itself out, so it can sit inside a <div class="menu">. Pages made for 1.2 look the same.
- **1.2.1** (2026-11-18): fix: a PNG backup for the tab icon, `site/favicon-32.png`, for browsers that can't show the SVG (some Safari versions). Linked before the SVG on every starter page and the specimen; `/favicon.ico` should now go to the PNG, not the SVG (see Site icon). Nothing looks different. To get it in a site, copy the file and add the PNG `<link>` line above the SVG one.
- **1.2.0** (2026-11-18): new: the site icon. The stamp as `site/favicon.svg` and `site/apple-touch-icon.png`, linked from every starter page and the specimen (see Site icon). Pages look the same; to get the icon in a site, copy the two files and add the two `<link>` lines.
- **1.1.1** (2026-11-18): fix: the menu links, `…` and the lock could not be clicked, because the centre (made positioned in 1.1.0 for the stamp) was drawn over the menu. The menu now sits above it (`z-index: 2`). Nothing looks different. New: the click check in section 6.
- **1.1.0** (2026-11-18): the concept, the stamp, slow ink, quiet selection, paper by season, print, the list and reading pieces, three new starter pages (`list.html`, `reading.html`, `404.html`), and the specimen page. Pages made for 1.0.0 look the same.
- **1.0.0** (2026-11-18): first version, taken from hyvnl.com as it looked on 2026-11-18.
