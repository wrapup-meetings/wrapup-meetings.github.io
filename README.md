# wrapup-meetings.github.io

GitHub Pages site for Wrap-Up.

| URL | File | What it is |
|---|---|---|
| `https://wrapup-meetings.github.io/` | `index.html` | Home — intentionally blank for now |
| `https://wrapup-meetings.github.io/intro` | `intro/index.html` | Product one-pager for prospective customers: motivation, the live map to try (the demo's Board, copied in), features |
| `https://wrapup-meetings.github.io/demo` | `demo/index.html` | Participant familiarization page for the meeting-map interface |

Every page is a single self-contained HTML file: no build step, no dependencies,
no external requests. Edit the file, commit, push — Pages redeploys in a minute.

## First-time setup

The repository name has to match the account exactly, or the site will not be
served at `wrapup-meetings.github.io`:

1. On GitHub, as **wrapup-meetings**, create a public repository named
   **`wrapup-meetings.github.io`**. Do not add a README, license, or
   `.gitignore` — this folder already has the files.
2. From this folder:

   ```bash
   git remote add origin https://github.com/wrapup-meetings/wrapup-meetings.github.io.git
   git push -u origin main
   ```

3. **Settings → Pages → Build and deployment**: source *Deploy from a branch*,
   branch `main`, folder `/ (root)`. Save.
4. Wait ~1 minute, then open `https://wrapup-meetings.github.io/demo`.

## Updating the demo page

`demo/index.html` is a copy of `documents/user_study/design/familiarization.html`
from the `wrap-up` project repository, wrapped in a `<!doctype html>` document
(that source file is written to be embedded, so it carries no `<head>` of its
own). To publish a new version, re-copy it and keep the wrapper:

```
<!doctype html><html lang="en"><head> … meta, title, favicon … </head>
<body>  ← the familiarization.html contents go here, minus its
          <meta charset> and <title> lines
</body></html>
```

Then:

```bash
git add demo/index.html && git commit -m "Update demo" && git push
```

## Local preview

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000/demo/>.

## Notes

- `.nojekyll` turns off Jekyll processing, so files are served exactly as they
  are in the repository.
- The demo page records nothing and sends nothing anywhere — the sandbox on it
  is a local fixture, not a live meeting.
