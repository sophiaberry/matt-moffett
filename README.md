# Matt Moffett: Artist Portfolio

The website for **Matt Moffett**, a painter and mosaic artist in Tulsa, Oklahoma. It shows his original paintings (available and sold), sells prints, and tells visitors how to get in touch about commissions.

**Pages:** Home · Work · Prints · About · Services · Contact

---

## How the site works

This is a simple website: plain HTML with no framework and no build step. It's hosted for free on **GitHub Pages**, and any change saved to this repo goes live within a minute or two.

The paintings and prints aren't typed into the page itself. They're stored in two list files, and the page builds itself from those lists:

| File | What's in it |
|---|---|
| `data/artworks.json` | Original paintings: title, photo, size, medium, year, Available/Sold, price, featured |
| `data/prints.json` | Prints for sale: title, photo, print size, price, Shopify buy link, description, featured |
| `data/about.json` | The About page: headline, photo of Matt, and bio |
| `images/` | Every photo used on the site |
| `index.html` | The design, layout, and the Services and Contact text |
| `.pages.yml` | Settings for the Pages CMS editor (see below) |
| `favicon.png` | The little umbrella icon shown in the browser tab |
| `favicon.jpg` | The same icon on white, used when someone saves the site to their phone home screen |
| `CLAUDE.md` | Technical notes for Claude Code |

Each painting or print only needs to be entered once. The site places it everywhere it belongs: Featured work on the home page, the Available or Sold section of Work, and the Prints page.

---

## Editing the site

### Paintings, prints and the About page: use Pages CMS (no code)

1. Go to **[app.pagescms.org](https://app.pagescms.org)** and sign in.
2. Open **matt-site**.
3. Choose **Original paintings**, **Prints** or **About page**.
4. To change a piece, click it, edit the form, and click **Save**.
5. To add a piece, click **Add**, upload the photo, fill in the details, and click **Save**.

Useful switches:

- **Available or sold:** a sold painting moves to the Sold section and shows a SOLD tag.
- **Show in Featured work:** puts the piece on the home page.
- **Order:** drag pieces up or down in the list to change their order on the site.
- **Shopify buy link (prints):** if filled in, the button says "Buy this print" and goes to Shopify. If empty, it opens an email order to Matt.

Changes appear on the live site within a couple of minutes. Refresh the page to see them.

### Design, layout and page text: use Claude Code

For anything beyond paintings and prints, like colors, fonts, layout, new sections, or the Services text, open **[claude.ai/code](https://claude.ai/code)**, select the **matt-site** repository, and describe the change in plain English. For example:

> "Change Henry the Horrible's size to 24 × 30 in and make the About page headline bigger."

Claude Code saves its work to a branch first. Ask it to merge into **main** (or say "commit directly to main" for small edits) to make the change live.

---

## Photo tips

- Use simple file names with no spaces, such as `BlueHeron.jpg` rather than `Blue Heron.jpg`.
- JPG works best for paintings. Keep files reasonably sized (under about 2 MB) so the site loads quickly.
- Photos uploaded through Pages CMS go into the `images/` folder automatically.

---

## Contact

Site inquiries go to **tulser33@gmail.com**.
