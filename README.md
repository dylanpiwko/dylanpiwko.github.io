# dylanpiwko.github.io

Source for my portfolio site at https://dylanpiwko.github.io

## Editing

- About and Other work: `index.md`
- Projects: `_projects/` (one file per project, shown in file-name order)
- Name, headline, email, LinkedIn: `_config.yml`
- Colors and fonts: `assets/css/style.css`
- PDF: replace `assets/Dylan_Piwko_Portfolio.pdf`, keeping the same name

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
