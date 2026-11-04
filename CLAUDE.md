# Fiduciam Capital website: notes for Claude

This repo is the public website for Fiduciam Capital (https://fiduciamcapital.com).
It is a plain static site: HTML, CSS, JavaScript and images. There is no framework,
no build step, no database and no package install. Vercel serves the files as they are.
Every push to `main` deploys to the live site automatically.

## Where things are

| Page | File |
| --- | --- |
| Home | `index.html` |
| What We Invest In | `what-we-invest-in/index.html` |
| Partial Liquidity | `partial-liquidity/index.html` |
| Full Exit | `full-exit/index.html` |
| About | `about/index.html` |
| Contact | `contact/index.html` |

- Styles: `css/custom.css` (the theme). The other CSS files are libraries; leave them alone.
- Scripts: `js/function.js` (theme behavior). The rest are libraries.
- Images: `images/`. Reference them with `../images/<file>` from a page folder, or
  `images/<file>` from the home page.
- The contact form is a Tally embed (`contact/index.html`, form id `mY12VW`). Submissions
  go wherever the Tally account sends them. The hidden `<form id="contactForm">` and the
  PHP handler references in `js/function.js` are unused leftovers from the old host.
- Each page repeats the header, nav and footer. A nav change has to be made in all six files.

## The partner placeholder on About

`about/index.html` has a second partner section (between `<!-- Partner Start` and
`<!-- Partner End -->`) waiting for real content. Every placeholder value is written as
`[PARTNER ...]`, so searching for `[PARTNER` finds all of them:

- `[PARTNER NAME]` (heading and image alt text)
- `[PARTNER HIGHLIGHT 1..4 TITLE]` and their one-to-two sentence descriptions
- the photo: `images/partner-placeholder.jpg`. Add the real photo to `images/`
  (a square-ish photo around 600x600 works best; crop it if needed), point the `<img>`
  at it, and delete the placeholder file.

Match the style of Keegan's section just above it: four short highlights, each a title
plus one or two sentences. If the partner's title is something other than "Partner",
change the heading (`Our Partner:`) too.

## Adding a page

1. Copy an existing page folder (for example `full-exit/`) to a new folder with a
   lowercase, hyphenated name (for example `our-team/`).
2. Edit the title, the page header (`page-header` section) and the content.
3. Add the nav link in the header menu AND the footer menu of all six existing pages
   plus the new one. Keep the order the owner asks for (for example between About and Contact).
4. Links between pages use folder paths with a trailing slash: `../our-team/`.

## Making changes safely

- Keep the look identical to the rest of the site: reuse existing classes and sections
  rather than writing new CSS.
- Check the change in a browser (desktop and phone width) before merging.
- Prefer a branch + pull request: Vercel posts a preview link on the PR, and merging to
  `main` publishes it.
- `vercel.json` adds a `noindex` header only on `*.vercel.app` addresses so preview
  copies don't compete with the real domain in search results. Leave it in place.
