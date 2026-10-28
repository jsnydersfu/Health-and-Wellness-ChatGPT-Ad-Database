# ChatGPT Ad Database

A self-contained, static, **searchable** archive of advertisements observed in
ChatGPT's free tier. No server or database engine required — it's just an HTML
page that reads `data.json` and image files, so it hosts for free on GitHub Pages.

Each entry: **ad image · advertiser · prompt · ChatGPT response · date collected**
(plus location, run, and ad landing URL). Search by **advertiser, ad text, or
prompt**; sort by **date** (newest/oldest) or **advertiser** (A–Z / Z–A); filter
by location.

## Files
- `index.html` — the whole app (search, sort, grid, detail view). Edit the title/
  blurb at the top if you like.
- `data.json` — one record per ad (679 records). Regenerate or hand-edit as needed.
- `images/` — put your ad PNGs here (see `images/README.txt`).
- `serve.py` — optional local preview helper.

## 1) Add your images
Copy every ad screenshot into `images/` using the run-prefixed names
(`run1_London_ad_0001.png`, …) so they match the `img` field in `data.json`.
(If you haven't prefixed them yet, run the `prefix_run1_images.bat` /
`prefix_run2_images.bat` renamers in each run's folder first.)

## 2) Preview locally
Double-clicking `index.html` won't load the data (browsers block `fetch()` from
`file://`). Instead run a tiny local server:
```
python serve.py
```
and open the URL it prints.

## 3) Publish free on GitHub Pages
1. Create a new GitHub repository (e.g. `chatgpt-ad-database`) and make it Public.
2. Upload everything in this folder (`index.html`, `data.json`, `images/`,
   `README.md`) to the repo — either with the web "Add file → Upload files"
   button, or with git:
   ```
   git init
   git add .
   git commit -m "ChatGPT ad database"
   git branch -M main
   git remote add origin https://github.com/<you>/chatgpt-ad-database.git
   git push -u origin main
   ```
3. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a
   branch**, pick branch `main` and folder `/ (root)`, Save.
4. After a minute your public site is live at
   `https://<you>.github.io/chatgpt-ad-database/`.

GitHub repos handle this comfortably (the 679 ad-block PNGs are small). If the
image set ever grows past repo limits, host the `images/` folder on a static
host or object storage and change the `src="images/..."` prefix in `index.html`.

## Notes & attribution
- This is a **research/transparency archive**. Advertiser names and ad creatives
  belong to their respective owners and are reproduced for non-commercial
  content-analysis research. Consider adding your institution/affiliation and a
  contact to `index.html`.
- The `response` field contains ChatGPT output you collected. If you'd rather not
  publish full responses, you can truncate or drop that field in `data.json`
  (the page handles an empty value fine).
- No personal data is included. Do not add any.
