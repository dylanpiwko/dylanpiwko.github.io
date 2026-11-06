# Dylan Piwko: engineering portfolio site

This is the source for my portfolio website. GitHub Pages builds it automatically, so any change committed here goes live in about a minute.

## Where things are

| To change | Edit this file |
|---|---|
| A project's text, figures or links | `_projects/<project>.md` |
| Home page intro | `index.md` |
| Name, email, LinkedIn, phone, degree line | `_config.yml` |
| Fonts, colors, spacing | `assets/css/style.css` |
| Downloadable PDF | Replace `assets/Dylan_Piwko_Portfolio.pdf` (keep the same file name) |

You can edit any of these on github.com: open the file, click the pencil icon, make the change, then click **Commit changes**.

## Editing a project page

Each project is one Markdown file in `_projects/`. The block at the top, between the `---` lines, controls the project card on the home page:

```yaml
title: Kestrel Flight Computer
dates: September 2026 – Present
role: Designer, Personal Project
skills: KiCad · PCB design · embedded C++ · RF
summary: One or two sentences shown on the home page card.
thumbnail: /assets/img/kestrel/thumb.jpg
permalink: /projects/kestrel/
```

Below that is normal Markdown:

- `## Heading` for a section, `### Heading` for a smaller one
- `- item` for a bullet; indent sub-bullets with 4 spaces
- `**bold**`, `*italic*`, `[link text](https://example.com)`
- Tables use `|` between columns (see the Kestrel page for an example)

## Adding or replacing pictures

1. Upload the image into the project's folder in `assets/img/` (**Add file → Upload files**).
2. Put it on the page with one line:

```liquid
{% include figure.html src="/assets/img/kestrel/new-photo.jpg" alt="What the picture shows" caption="Caption under the picture" %}
```

Optional: add `width="600px"` to keep a small diagram from stretching to full width. Captions can use Markdown, e.g. `caption="**Figure 3.** *Text*"`.

For photos side by side, separate the files and their descriptions with `|`:

```liquid
{% include gallery.html images="/assets/img/terrier/a.jpg | /assets/img/terrier/b.jpg" alts="First photo | Second photo" height="300px" caption="(L to R): ..." %}
```

## Adding a new project

1. Copy one of the files in `_projects/` and rename it, e.g. `05-rc-aircraft.md`.
2. Change the block at the top (including a new `permalink`) and replace the text.
3. Add a thumbnail. Any 16:10 image works best, e.g. 800 × 500 px.

Projects appear in the order of their file names (`01-…`, `02-…`), so rename files to reorder them.

## If the site doesn't update

Open the **Actions** tab. A red ✗ next to the latest "pages build and deployment" run means the build failed; click it to see which file and line caused it. The most common cause is an unclosed quote in an `{% include %}` line or in the block at the top of a project file.
