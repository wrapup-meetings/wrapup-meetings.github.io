# wrapup-meetings.github.io

GitHub Pages site for Wrap-Up.

| URL | File | What it is |
|---|---|---|
| `https://wrapup-meetings.github.io/` | `index.html` | Home — landing page: challenges, how WrapUp helps, our approach, comparison, demo request |
| `https://wrapup-meetings.github.io/info` | `info/index.html` | Previous home: product one-pager with the live map to try (the demo's Board, copied in) |
| `https://wrapup-meetings.github.io/demo` | `demo/index.html` | Participant familiarization page for the meeting-map interface |

Every page is a single HTML file: no build step, no dependencies, no external
requests. The home page also loads its fonts (Newsreader, IBM Plex Sans, IBM Plex Mono — all
SIL OFL, self-hosted) and product screenshots from `assets/`. Edit, commit,
push — Pages redeploys in a minute.

## Home page

- **Demo requests.** Every "Request a Demo" button opens an email to
  wrapup.iui@gmail.com with the subject and a short request template filled in.
  The link is `window.WRAPUP_DEMO_HREF`, set once near the top of `index.html`'s
  `<head>`; swap it for a form or scheduling URL if you get one. If no email app
  takes over within about a second, a small panel shows the address with a
  button to copy it.
- **Scrolling.** On desktop, from Challenges to the end of the page, one
  scroll gesture moves exactly one step (the `stops` list in the script):
  each challenge, each solution, Our Approach, the comparison, the closing.
- **Hero art.** Drawn in the browser, not an image (the "Hero art" block in
  `index.html`'s script): scattered ideas gather into topic groups sized and
  packed by the map's own rules, the last topic live. It loops on a 6-second
  timer (about 2s of idea cloud, 3s of map); clicking a topic makes it live,
  and clicking the cloud forms the map. A still frame with reduced motion.
- **Product images.** In `assets/product/`: `call` (WrapUp beside a video
  call, from `info/`), and `clarity` and `ai-1`–`ai-3` (plus `-m` portrait
  versions for phones), drawn
  with the demo's own renderer (`nodeSVG`, `packItems`, `cardBlock` in
  `demo/index.html`) on a transparent background. `og.png` is the social preview.
- **Motion.** The Challenges and With WrapUp sections pin while you scroll
  through their states; other sections snap into place on desktop. With
  reduced motion everything is static and stacked.

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
