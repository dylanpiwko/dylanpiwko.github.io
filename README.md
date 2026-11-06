# dylanpiwko.github.io

Source for my portfolio site at https://dylanpiwko.github.io

## Editing

- Projects: `_projects/` (one Markdown file per project, shown in file-name order)
- About section: `index.md`
- Name, headline, email, LinkedIn: `_config.yml`
- Colors and fonts: `assets/css/style.css`
- PDF: replace `assets/Dylan_Piwko_Portfolio.pdf`, keeping the same name

Sub-bullets are indented 4 spaces.

## Images

Add a figure:

```liquid
{% include figure.html src="/assets/img/kestrel/photo.jpg" alt="Description" caption="Caption" %}
```

`width="600px"` keeps a small diagram from stretching. For photos side by side:

```liquid
{% include gallery.html images="/assets/img/a.jpg | /assets/img/b.jpg" alts="First | Second" height="300px" caption="Caption" %}
```

Card thumbnails are 800 × 500.
