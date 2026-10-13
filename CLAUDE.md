# CLAUDE.md

Portfolio site for Matt Moffett, a painter and mosaic artist in Tulsa, Oklahoma. It is a static site with no build step, no framework and no package manager. Everything is served as-is.

## Layout

```
index.html          The whole site: markup, CSS (in <style>) and JS (in <script>)
favicon.jpg         Favicon and apple-touch-icon
data/artworks.json  Original paintings, shown on the Work page
data/prints.json    Prints for sale, shown on the Prints page
images/             All images (artwork photos, headshot, home banner)
.pages.yml          Pages CMS config for editing the two JSON files and uploading images
```

## How index.html works

- **Single page, hash routing.** Each page is a `<section class="page">` with an id: `home`, `work`, `prints`, `about`, `services`, `contact`. `route()` shows the section matching `location.hash` (unknown hashes fall back to `home`) and sets `document.title`. Adding a page means adding the section, a nav link, and an entry in the `pages` and `titles` arrays.
- **Data loading.** On load, the script fetches `data/artworks.json` and `data/prints.json` (`cache: "no-cache"`) and renders tiles into these containers:
  - `#featured` (Home): every artwork and print with `featured: true`, artworks first
  - `#avail` / `#sold` (Work): artworks split by `status`, toggled by the Available/Sold filter buttons
  - `#printgrid` (Prints)
  Because the data is loaded with `fetch`, opening `index.html` from `file://` won't show artwork. Serve it locally instead, for example `python3 -m http.server`.
- **Detail dialog.** Clicking a tile opens `<dialog id="dlg">` through `openDlg()`. Artwork details come from `data-*` attributes on the tile. Print details come from the `PRINTS` array.
- **Hand-written content.** The About, Services and Contact copy, the home banner image (`images/The-Night-We-Learned-How-to-Swim.jpg`) and the About headshot (`images/Matt-Moffett-headshot.png`) are set directly in `index.html`, not in the CMS.
- **Styling.** Colors and fonts are CSS variables on `:root`. The fonts are Hanken Grotesk for body text and Gloock for headings, both loaded from Google Fonts. Tiles cycle through the palette classes `p1` to `p6`.
- **Contact.** All email links and order/purchase fallbacks go to `hello@mattmoffett.com`.
- The script escapes all values from the JSON with `esc()`, and `src()` strips leading slashes from image paths. Keep that escaping for any new fields.

## Data files

Both files are JSON objects wrapping one list: `{ "artworks": [...] }` and `{ "prints": [...] }`. Pages CMS edits them, so keep that shape and the field names in sync with `.pages.yml`.

**Artwork fields:** `title` (required, entries without one are skipped), `image`, `size`, `medium`, `year`, `status` (`"Available"` or `"Sold"`, case-insensitive), `price`, `featured`.
- Sold pieces show a SOLD tag, and the dialog links to Prints.
- Available pieces show `price`, or "Inquire" if `price` is empty, and the dialog opens a purchase email.

**Print fields:** `title`, `image`, `size`, `size_details` (overrides `size` in the dialog), `price`, `buy_link`, `description`, `featured`.
- If `buy_link` is set (a Shopify buy-button cart URL), the button says "Buy this print" and opens in a new tab.
- If it is empty, the button becomes a "Print order" email.
- In `description`, a blank line starts a new paragraph.

Optional fields can be left out or set to `""`.

## Images

- Images live in `images/` and are referenced from JSON as `images/<file>`, a path relative to the site root.
- Pages CMS uploads to the same folder, as set by `media.input`/`media.output` in `.pages.yml`.
- When renaming or deleting an image, update every JSON entry and `index.html` reference that uses it. The same image can appear in both lists. For example, `GardenParty.jpg` is used by a painting and by a print.
- Use simple filenames with no spaces or quotes.

## Editing workflow

- Matt edits content through Pages CMS, which commits straight to the repo with messages like "Update data/artworks.json (via Pages CMS)". Expect those commits and don't reformat the JSON files without a reason.
- If you add a field to the data, also add it to `.pages.yml` so it can be edited in the CMS, and render it in `index.html`.
- There are no tests or linters. To check a change, serve the folder locally, then look at Home, Work (both filters), Prints, and the detail dialog for both kinds of item.
