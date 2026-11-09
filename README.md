# dylanpiwko.github.io

Source for my portfolio site at https://dylanpiwko.github.io

## Quick edits on GitHub

1. Open the file on github.com (see the list below) and click the pencil icon (Edit this file).
2. Make the change, then click **Commit changes…**, type a short message, and commit straight to `main`.
3. Wait about a minute. The **Actions** tab shows a green check when the site has rebuilt.
4. Open the site and hard refresh (Ctrl+Shift+R, or Cmd+Shift+R on a Mac) to see the change.

To replace a picture, open its folder, click **Add file → Upload files**, and upload a file with the exact same name. To undo a bad edit, open the file's **History**, pick the last good version, and copy its text back in.

If the Actions tab shows a red X, the site keeps showing the last good version. Open the failed run to see which line broke. It's usually a missing quote or a bad indent in the block at the top of a project file.

## Where things are

| To change | Edit |
| --- | --- |
| About, Other work | `index.md` |
| A project's card, pictures, What? / How? / Results | the block at the top of its file in `_projects/` |
| A project's longer write-up | the text below the second `---` in that file |
| Name, headline, degree, graduation, email, LinkedIn | `_config.yml` |
| Publications page | `publications.md` |
| Home page header photo | `assets/img/home/north_campus.jpg` (keep the credit line in `_layouts/home.html`) |
| Colors and fonts | `assets/css/style.css` |
| Portfolio PDF | `assets/Dylan_Piwko_Portfolio.pdf` |

Projects show on the home page in file-name order (`01-`, `02-`, …).

The PDF doesn't update when the site text changes. To update it, edit the Word portfolio, delete the phone number, use **File → Save As → PDF**, and upload it to `assets/` with the same name.

## Project files

The block between the `---` lines at the top of each project file sets the card on the home page, the pictures at the top of the page and the What? / How? / Results lists:

```yaml
title: Kestrel Flight Computer
role: Designer, Personal Project
dates: October 2026 – Present
skills: KiCad, PCB design, RF
summary: One sentence for the home page card.
thumbnail: /assets/img/kestrel/thumb.jpg
images:
- src: /assets/img/kestrel/kestrel_block.png
  alt: What the picture shows
  caption: Kestrel block diagram
  w: 1.5        # optional: relative width when there are several pictures
what:
- First bullet
how:
- Use **double asterisks** for bold
results:
- ...
```

Put quotes around a line if it contains a colon followed by a space. Everything below the second `---` is normal Markdown (`## Heading`, paragraphs, `- bullets`, tables).

## Figures in the page text

```liquid
{% include figure.html src="/assets/img/kestrel/photo.jpg" alt="Description" caption="Caption" %}
```

Add `width="600px"` to keep a small diagram from stretching. Card thumbnails are 800 × 500.
