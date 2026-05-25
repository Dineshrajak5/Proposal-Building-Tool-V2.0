# FACE Prep — Proposal Builder (Vercel deployment)

A self-contained internal tool for the FACE Prep team to build, preview, and export
training proposals (Semester Integrated or Skill Development Bootcamp).

## Files
- `index.html` — the entire app (HTML + CSS + JS + catalog, all in one file)
- `vercel.json` — static hosting config (clean URLs + basic security headers)

## Deploy to Vercel (2 options)

### Option A — Drag & drop (fastest)
1. Go to https://vercel.com/new
2. Drag this whole folder onto the page (or zip it and upload).
3. Vercel detects a static site automatically. Click **Deploy**.
4. You get a URL like `https://faceprep-proposals.vercel.app`.

### Option B — Git + CLI
```bash
npm i -g vercel          # one time
cd vercel_deploy
vercel                   # follow prompts (first deploy = preview)
vercel --prod            # promote to production
```

## After deploy
- Share the production URL with your team.
- Sign in with any `@faceprep.in` email + the access code.
- **Change the access code:** open `index.html`, find
  `const ACCESS_CODE='faceprep2026';` near the top of the script and set your own.
  Redeploy after editing.

## Saved proposals
"Save" stores proposals in the **browser's localStorage**, so they are per-device /
per-browser (not shared across the team or across machines). This works automatically
once hosted on Vercel. For team-shared saved proposals you'd need a backend/database —
see "Next steps" below.

## Important security note
The login is **client-side only** — the access code lives in `index.html`, so anyone
who can read the page source can find it. This is access-convenience, not real security.

For genuine `@faceprep.in`-only access, put the site behind real auth:
- **Vercel Password Protection** (Project → Settings → Deployment Protection) — simplest.
- **Vercel + Google Workspace SSO** via a middleware/edge function — restricts to your
  domain properly.
- Or move saving + auth to a small backend (e.g. Vercel KV / a database) so proposals
  are shared and access is enforced server-side.

I can help set any of these up if you want to go beyond the current single-file tool.
