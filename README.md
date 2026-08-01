# Vincent Larouche — Portfolio Site

Single-file portfolio site (`index.html`, no build step, no dependencies
besides Google Fonts). See `CLAUDE.md` for the design system and content
guardrails before editing copy.

## Preview locally

From this folder:

```bash
python3 -m http.server
```

Then open http://localhost:8000 in a browser. Stop the server with `Ctrl+C`.

## Deploy to GitHub Pages

1. Push this repo to GitHub (create the repo first if it doesn't exist yet):
   ```bash
   git add .
   git commit -m "Initial portfolio site"
   git branch -M main
   git remote add origin <your-repo-url>
   git push -u origin main
   ```
2. In the GitHub repo, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Set branch to **main**, folder to **/ (root)**, then **Save**.
5. GitHub will publish the site at `https://<username>.github.io/<repo>/`
   (usually ready within a minute or two — check the Pages settings page for
   the live URL and deployment status).

## After deploying

Add the published URL to LinkedIn — Profile → **Edit intro → Website(s)**, or
the featured/contact-info section — so it's reachable from your profile.
