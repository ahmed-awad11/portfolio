# Ahmed Awad: Portfolio Website

A single-page developer portfolio built with plain HTML, CSS and JavaScript.
There is no framework, no build step and no dependencies, so there is nothing to install.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole site: markup, styles, and a `CONFIG` object holding all content |
| `vercel.json` | Optional hosting settings (clean URLs and basic security headers) |
| `.gitignore` | Keeps secrets and editor files out of Git |

## Run locally

Opening `index.html` by double-clicking works. A local server is closer to production:

```bash
cd portfolio
python3 -m http.server 8000
# open http://localhost:8000
```

## Edit your content

Everything is in the `CONFIG` object near the bottom of `index.html`.

- **Contact details and links:** `CONFIG.person` (`email`, `phone`, `linkedin`, `github`, `cvUrl`).
- **Hero and About text:** `CONFIG.hero` and `CONFIG.about`.
- **Skills:** `CONFIG.skills`. The level keys are `work`, `fund`, `basic`, `begin`, `learn`, `dev`, `plan`, `cert` and `supp`.
- **Certifications:** move an entry between `certs.completed`, `certs.learning` and `certs.planned`. Add a real credential link as the third value of a completed entry; leave it `null` to hide the link.
- **Education:** `CONFIG.education`. Set `showCgpa: true` only once your CGPA is confirmed. Add real courses to `areas`.
- **Add a project:** copy an object in `CONFIG.projects` and set `status` to `Planned`, `In Progress` or `Completed`. Fill in `repo` and `demo` only with real URLs, because buttons appear only when a URL is set. Add `image` (for example `"images/my-project.png"`) once you have a screenshot, and save the file in an `images/` folder next to `index.html`.
- **Filters** are generated from the categories your projects use, so they update automatically.

## Before publishing: checklist

- [ ] Confirm your CGPA, then set `showCgpa: true` (or leave it hidden).
- [ ] Review the skill levels in `CONFIG.skills` for accuracy.
- [ ] Add credential links for completed certifications when you have them.
- [ ] Confirm you are happy for your phone number to be public.
- [ ] Only add a CV button (`cvUrl`) when a real CV file is hosted; the site does not currently render one.
- [ ] Never put API keys, tokens or passwords in `index.html`. Everything in this file is public.

## Deploy to Vercel

### Option A: GitHub, then Vercel (recommended, auto-redeploys on every push)

1. Create a new repository on GitHub (for example `portfolio`).
2. In this folder run:
   ```bash
   git init
   git add .
   git commit -m "Initial portfolio"
   git branch -M main
   git remote add origin https://github.com/<your-username>/portfolio.git
   git push -u origin main
   ```
3. Go to https://vercel.com, sign in with GitHub, click **Add New... > Project**, and import the repository.
4. Leave **Framework Preset** as **Other**. Leave Build Command and Output Directory empty. Click **Deploy**.
5. Vercel gives you a `*.vercel.app` URL. Add a custom domain later under **Settings > Domains**.

### Option B: Vercel CLI

```bash
npm i -g vercel
cd portfolio
vercel          # first run: log in and accept the defaults (preview deploy)
vercel --prod   # publish to production
```

## Optional integrations

The site has no backend, analytics or forms, so no environment variables are needed.
If you later add a service that needs a secret (for example an AI API), keep the key
in a `.env` file (already git-ignored) and call it only from a server-side function,
never from `index.html`. Add the variable in Vercel under **Settings > Environment Variables**.
