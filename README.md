# AnyVisa — prototype deploy

Two self-contained files, zero build step, ready for GitHub Pages.

- `index.html` — the public site (home, requirements, dashboard, AI document check — all in one file, switched via JS)
- `admin.html` — internal tool (pricing table, AI review queue). Not linked from the public site. **Do not treat this as secure** — it has no login. Don't put real customer data behind it until it has real authentication.

## Deploy manually via GitHub Pages (5 minutes)

1. Go to [github.com/new](https://github.com/new) and create a new repository.
   - Name it anything, e.g. `anyvisa-site`
   - Set it to **Public** (GitHub Pages on a free account needs a public repo)
   - Don't add a README/gitignore — leave it empty
2. On the new repo's page, click **"uploading an existing file"** (the link in the empty-repo message).
3. Drag in `index.html`, `admin.html`, and `.nojekyll` from this folder. Commit directly to the `main` branch.
4. Go to **Settings → Pages** (left sidebar).
5. Under "Build and deployment" → Source, choose **Deploy from a branch**.
6. Branch: `main`, folder: `/ (root)`. Click **Save**.
7. Wait ~1 minute, then refresh — GitHub shows the live URL at the top, something like:
   `https://<your-username>.github.io/<repo-name>/`

That's it — `index.html` is served automatically at that root URL, `admin.html` at `.../admin.html`.

## Updating the site later

Same repo page → click into a file → pencil (edit) icon → paste new content → commit.
For bigger changes, easiest is to re-upload the changed file via "Add file → Upload files" — it overwrites on commit.

## What still needs a real backend before this is production-ready

Everything below is demo-only right now — it works in the browser but doesn't persist or send anywhere:

- **Get Visa wizard submission** — currently just shows the dashboard checklist locally. Needs an API endpoint to actually create a lead/application record.
- **Document upload buttons** — flip to "Uploaded" visually but don't upload a real file anywhere.
- **AI document check** (`ai-check.html` demo, and the admin review queue) — needs a backend service that stores the file and calls a vision-capable AI model; the API key must live server-side, never in this HTML.
- **admin.html pricing table "Save changes"** — shows an alert, doesn't write anywhere. Needs a database + authenticated API.
- **admin.html itself** — no login. Needs real staff authentication before it touches real prices or real customer documents.

Happy to help design/build that backend next — it needs a small server (e.g. Cloudflare Workers, or a simple Node/Python API) plus a database, which GitHub Pages alone can't provide since it only serves static files.
