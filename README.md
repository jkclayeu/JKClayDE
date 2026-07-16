# JK & Clay — website template

This is the JK & Clay shop website. **You never need to edit the HTML to run the shop.** Everything you change day to day — products, prices, photos, blog articles, lab notes — lives in plain folders and small text files. You edit those files (here on GitHub), commit, and the site updates itself.

---

## What's in the repo

```
index.html                 the website itself (do not edit for content)
image-slot.js              helper the site uses
support.js                 helper the site uses
ProductCard.dc.html        the shop product card (do not edit for content)

products/                  ← your shop
  index.json                 the ordered list of products shown
  <product-slug>/
    product.json             one product's details
    photo1.jpg               its photos
    photo2.jpg

blog/                      ← your Journal (Blog)
  index.json                 the ordered list of articles shown
  <article-slug>/
    post.json                the article's title, date, tag, excerpt
    article.md               the full text of the article
    cover.jpg                the article's photo

lab/                       ← your Lab Journal
  notes.json                 all glaze-test notes, in one file

images/                    ← site-wide photos
  site.json                  which files to use for the hero & about photo
  <your photos>
```

A **slug** is just the folder name — lowercase words joined by hyphens, e.g. `green-breakfast-bowl`. Use only letters, numbers and hyphens (no spaces, no accents).

---

## 1. Products

### Add a product
1. Create a folder inside `products/`, named with a slug, e.g. `products/green-breakfast-bowl/`.
2. Put the photos in that folder (JPG or PNG; square photos look best).
3. Create `product.json` inside it:

```json
{
  "name": "Green Breakfast Bowl",
  "category": "bowls",
  "price": 32.00,
  "colorName": "Sage green",
  "swatch": "#dce3d3",
  "glaze": "#aec19c",
  "description": "A short, warm description of the piece.",
  "images": ["photo1.jpg", "photo2.jpg"]
}
```

4. Add the slug to `products/index.json`, in the position you want it to appear:

```json
[
  "rose-green-travel-mug",
  "green-breakfast-bowl"
]
```

Commit. The piece now appears in the shop, in the right category, in the category counts, and gets its own product page — automatically.

### Product fields
| field         | what it does                                                            |
|---------------|-------------------------------------------------------------------------|
| `name`        | the product title                                                       |
| `category`    | **must be one of:** `mugs`, `vases`, `plates`, `bowls`                  |
| `price`       | a number in euros, e.g. `32.00` — the € sign is added for you           |
| `colorName`   | the glaze name shown under the title                                    |
| `swatch`      | background colour shown behind the photo while it loads (hex, e.g. `#dce3d3`) |
| `glaze`       | the colour dot shown in the glaze picker (hex)                          |
| `description` | the paragraph on the product page                                       |
| `images`      | list of photo filenames in the same folder; **the first one is the main image** |

### Common product edits
- **Change a price / description:** open that product's `product.json`, edit the value, commit.
- **Add / replace photos:** drop the files in the folder and update the `images` list.
- **Reorder the shop:** reorder the slugs in `products/index.json`.
- **Hide / remove a product:** delete its slug from `products/index.json` (you can leave or delete the folder).

---

## 2. Blog (the "Journal")

Each article is its own folder in `blog/`.

### Write a new article
1. Create a folder, e.g. `blog/glazing-in-winter/`.
2. Inside it, create `post.json`:

```json
{
  "title": "Glazing in winter",
  "tag": "Studio notes",
  "date": "Aug 2026",
  "excerpt": "One or two sentences shown on the article card.",
  "tint": "#e7e1d4",
  "image": "cover.jpg"
}
```

3. Create `article.md` — the full text of the note. **Separate paragraphs with a blank line:**

```
This is the first paragraph of the article.

This is the second paragraph. Leave one empty line between paragraphs
and the website turns each block into its own paragraph.
```

4. Add the photo (e.g. `cover.jpg`) to the same folder — or set `"image": ""` to skip the photo.
5. Add the slug to `blog/index.json` (newest usually goes first):

```json
[
  "glazing-in-winter",
  "the-quiet-ritual-of-the-morning-cup"
]
```

Commit. The article appears in the Journal grid, and clicking it opens the full text.

### Blog fields (post.json)
| field     | what it does                                                        |
|-----------|---------------------------------------------------------------------|
| `title`   | the article title                                                   |
| `tag`     | small label on the card, e.g. `Slow living`, `Care`, `Gifting`      |
| `date`    | shown next to the tag, e.g. `Aug 2026` (free text)                  |
| `excerpt` | the preview sentence on the card                                    |
| `tint`    | background colour behind the photo (hex)                            |
| `image`   | the photo filename in the same folder; `""` for no photo           |

The article text itself lives in **`article.md`**, not in `post.json`.

---

## 3. Lab Journal (glaze notes)

All lab notes live in a single file: **`lab/notes.json`**. It is a list; each entry is one glaze test. Add a note by adding a block to the top of the list:

```json
[
  {
    "id": "L-048",
    "hex": "#c9d3c0",
    "title": "Matte sage, high feldspar",
    "status": "Testing",
    "result": "First tile is promising — even surface, no pinholing. Firing a mug next to confirm on a curve."
  },
  {
    "id": "L-047",
    "hex": "#d8b7a6",
    "title": "Rose-ash over speckled buff",
    "status": "Keeper",
    "result": "A warm blush that breaks softly on the rims."
  }
]
```

### Lab fields
| field    | what it does                                                                    |
|----------|---------------------------------------------------------------------------------|
| `id`     | the batch label shown on the card, e.g. `L-048`                                  |
| `hex`    | the glaze colour dot (hex)                                                       |
| `title`  | the name of the test                                                             |
| `status` | one of `Keeper`, `Refining`, `Testing` — this colours the status pill            |
| `result` | your notes on how the test turned out                                            |

(Keep the file valid JSON: every entry wrapped in `{ }`, separated by commas, the whole list inside `[ ]`.)

---

## 4. Site photos (hero & about)

The big homepage photo (**hero**) and the portrait in the **"Hello, I'm Julia"** section are set in `images/`.

1. Put your photos in `images/`, e.g. `images/hero.jpg` and `images/julia.jpg`.
2. List them in `images/site.json`:

```json
{
  "hero": "hero.jpg",
  "about": "julia.jpg"
}
```

Leave a value as `""` to show the drag-and-drop placeholder instead of a fixed photo.

---

## 5. A note on JSON

The `.json` files are picky about punctuation. If the site stops loading after an edit, check that file for:
- a **comma** between every entry, and **no comma after the last one**;
- straight double quotes `"` around every text value (not “curly” quotes);
- every `{` closed with a `}` and every `[` closed with a `]`.

A free online "JSON validator" will point to the exact line if something is off.

---

## 6. Putting the site online (GitHub Pages)

1. Push this repo to GitHub.
2. Repo → **Settings** → **Pages**.
3. Under **Source**, choose branch `main` and folder `/ (root)`, then **Save**.
4. After a minute the site is live at `https://<your-username>.github.io/<repo-name>/`.

Every time you commit a change to a product, article, note or photo, GitHub Pages republishes automatically.
