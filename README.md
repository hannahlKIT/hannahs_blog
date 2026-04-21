# Life of Lorena — Authoring Guide

This site is built with [Hugo](https://gohugo.io/) and supports two languages: **English (default)** and **German**. English pages live at the root (`/`), German pages live under `/de/`.

---

## Running the site locally

```bash
hugo server
```

Then open http://localhost:1313/ for English or http://localhost:1313/de/ for German. The site rebuilds automatically as you edit files.

---

## How content files are named

Hugo picks the language of a file from its filename suffix:

| Filename                  | Language |
|---------------------------|----------|
| `my-post.en.md`           | English  |
| `my-post.de.md`           | German   |

Two files with the **same basename** but different language suffixes are treated as translations of each other. That's how the EN/DE switcher in the nav finds the matching page.

---

## Adding a new blog post

1. Create the English version in `content/post/`:

   ```
   content/post/2026-05-10-my-new-post.en.md
   ```

   With front matter like:

   ```yaml
   ---
   layout:   post
   title:    "My New Post"
   subtitle: "A short subtitle"
   date:     2026-05-10
   author:   "Hannah Lorena"
   image:    "img/home-bg-jeep.jpg"
   tags:
     - General
   ---

   Write your English content here.
   ```

2. Create the German version **with the same basename**:

   ```
   content/post/2026-05-10-my-new-post.de.md
   ```

   ```yaml
   ---
   layout:   post
   title:    "Mein neuer Beitrag"
   subtitle: "Ein kurzer Untertitel"
   date:     2026-05-10
   author:   "Hannah Lorena"
   image:    "img/home-bg-jeep.jpg"
   tags:
     - General
   ---

   Schreibe hier deinen deutschen Inhalt.
   ```

That's it — the language switcher will automatically link the two versions.

### If you only have one language ready

You can publish just the English version and add the German translation later. The switcher will link to the German home page as a fallback until the translated file exists.

---

## Editing existing pages (About, Archive, Notes)

Each of these has two files — edit whichever language you want to change:

| Page    | English                         | German                          |
|---------|---------------------------------|---------------------------------|
| About   | `content/about/index.en.md`     | `content/about/index.de.md`     |
| Archive | `content/archive/index.en.md`   | `content/archive/index.de.md`   |
| Notes   | `content/notes/index.en.md`     | `content/notes/index.de.md`     |

---

## Adding images

All images live in `static/img/`. Anything you put there is served from `/img/...`.

### 1. Add the image file

Drop your image into `static/img/`, e.g.:

```
static/img/my-vacation.jpg
```

### 2. Reference it in content

**As a post header image** (front matter):

```yaml
image: "img/my-vacation.jpg"
```

**Inside the body of a post** (Markdown):

```markdown
![Alt text describing the image](/img/my-vacation.jpg)
```

Note the leading `/` — this makes the path work for both `/` (English) and `/de/` (German) pages.

**With custom sizing** (raw HTML also works, since `unsafe = true` is enabled in the config):

```html
<img src="/img/my-vacation.jpg" alt="Alt text" width="600">
```

### Image tips

- Keep filenames lowercase and dash-separated (`my-vacation.jpg`, not `My Vacation.JPG`) — avoids URL-encoding headaches.
- Compress images before committing; large photos bloat the repo and slow page loads. Aim for under ~500 KB per image where possible.
- The site uses `lazysizes` for lazy-loading, so many images on one page is fine.

---

## Site-wide settings

Most site-level strings (title, description, slogan, menu labels) are defined per-language in `hugo.toml` under `[languages.en.params]` and `[languages.de.params]`. If you change the English slogan, don't forget to update the German one too.
