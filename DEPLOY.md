# Deploying to GitHub Pages

This is a [Docsify](https://docsify.js.org/) site — pure static files, no build step. GitHub Pages serves it as-is.

## Files in this repo

```
.
├── index.html                 # Docsify config + CDN scripts
├── .nojekyll                   # tells GitHub Pages not to run Jekyll (keeps _files)
├── README.md                   # homepage content
├── _coverpage.md               # the landing cover
├── _sidebar.md                 # left navigation
├── checklist.md                # full checklist on one page
└── guide/
    ├── 01-react-basics.md
    ├── 02-props.md
    ├── 03-state-usestate.md
    ├── 04-event-handling.md
    ├── 05-conditional-rendering.md
    ├── 06-rendering-lists.md
    ├── 07-side-effects-useeffect.md
    ├── 08-component-composition.md
    └── 09-next-steps.md
```

## Preview locally

Any static server works. With Node installed:

```bash
npx serve .
# or
npx docsify-cli serve .
```

Then open the printed URL (usually http://localhost:3000).

## Publish

1. Create a GitHub repo (e.g. `ReactSyllabus`) and push:

   ```bash
   git init
   git add .
   git commit -m "Add React Syllabus Docsify site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/ReactSyllabus.git
   git push -u origin main
   ```

2. On GitHub: **Settings → Pages**.
   - **Source:** Deploy from a branch
   - **Branch:** `main`, folder `/ (root)`
   - Save.

3. Wait ~1 minute. Your site is live at:

   ```
   https://<your-username>.github.io/ReactSyllabus/#/
   ```

## After publishing

Open `index.html` and set your repo so the "Edit on GitHub" corner ribbon works:

```js
window.$docsify = {
  name: 'React Syllabus Checklist',
  repo: 'https://github.com/<your-username>/ReactSyllabus',
  // ...
}
```

Also update the `[View on GitHub]` link in `_coverpage.md`.

## Notes

- The `.nojekyll` file is **required** — without it GitHub Pages ignores files/folders starting with `_` (like `_sidebar.md`).
- All Docsify and Prism scripts load from jsDelivr CDN, so an internet connection is needed to view the site.
- To add a page: create the `.md` file and add a link to it in `_sidebar.md`.
