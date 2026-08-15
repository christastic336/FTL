# FTL Lesson Repository — website

A single-page, filterable index of the Foundations of Teaching & Learning lesson
library. It reads its data from a Google Sheet (published as CSV) and falls back
to a bundled `data.json` copy if no sheet is connected.

## Files
- `index.html` — the whole site (filters, search, cards). Nothing to build.
- `data.json` — offline copy of the lessons, so the site works before you connect a sheet.
- `README.md` — this file.

## One-time setup

### 1. Push these files with GitHub Desktop
1. Put `index.html`, `data.json`, and `README.md` in the top level of a repository.
2. In GitHub Desktop: **Commit to main**, then **Push origin**.

### 2. Turn on GitHub Pages
1. On github.com, open the repo ▸ **Settings** ▸ **Pages**.
2. Under **Build and deployment**, Source = **Deploy from a branch**;
   Branch = **main**, folder = **/ (root)**. Save.
3. Wait ~1 minute. Your site is at `https://<your-username>.github.io/<repo-name>/`.

At this point the site is live, running from `data.json`.

### 3. Connect the live Google Sheet (optional but recommended)
1. Upload `FTL_Lesson_Repository_v2.xlsx` to Google Drive and open it as a Google Sheet.
2. In the Sheet: **File ▸ Share ▸ Publish to web**.
3. Under **Link**, choose the **Lessons** tab (not "Entire document") and format
   **Comma-separated values (.csv)**. Click **Publish**. Copy the link.
4. Open `index.html`, find this line near the bottom, and paste your link between the quotes:
   ```js
   const SHEET_CSV_URL = "";
   ```
5. Commit + push again. Now the site loads live from the sheet.

## Day-to-day
- **Editing lessons:** edit the Google Sheet. The site reflects changes on its own
  (Google refreshes the published CSV every few minutes). No push needed.
- **Changing the site** (design, filters): edit `index.html`, then commit + push.

## Good to know
- Publishing the Lessons tab makes **that tab's data publicly readable**. The lesson
  *files* in Drive stay private — the "Open in Drive" links only work for people who
  already have Drive access. The site is a public index over private content.
- Keep the **column headers unchanged** (ID, Title, Content_Area, SEP, CCC, FTL_Day,
  View_URL, …). The filters match on those exact names; renaming a column silently
  drops its filter.
- Published-CSV updates lag by roughly five minutes and depend on the sheet staying
  published. If the feed ever fails, the site automatically falls back to `data.json`.
- To refresh the offline fallback after big edits, re-export the sheet and replace
  `data.json` (or ask Claude to regenerate it).
