# SETUP.md — Getting lowlighter/metrics running on your profile

## What this gives you

Eight auto-generated SVG panels committed to your profile repo daily:

| File | What it shows |
|---|---|
| `metrics.header.svg` | Profile overview — repos, commits, PRs, stars |
| `metrics.isocalendar.svg` | 3D isometric contribution calendar (full year) |
| `metrics.languages.svg` | Language breakdown across all repos |
| `metrics.habits.svg` | Commit time heatmap + day distribution |
| `metrics.repositories.svg` | Featured repo cards with live stats |
| `metrics.activity.svg` | Recent commits, PRs, releases feed |
| `metrics.topics.svg` | Your starred GitHub topic badges |
| `metrics.achievements.svg` | GitHub achievement badges |

---

## Step 1 — Create your profile repository (if not done)

Your profile README lives in a repo named exactly the same as your username:

```
github.com/SiphiweRadebe/SiphiweRadebe
```

If it doesn't exist, create it at https://github.com/new
- Name: `SiphiweRadebe`
- Make it public
- Tick "Add a README file"

---

## Step 2 — Generate a Personal Access Token (classic)

> ⚠️ Fine-grained tokens are NOT supported — you must use a classic token.

1. Go to: https://github.com/settings/tokens/new
2. Note (name): `METRICS_TOKEN`
3. Expiration: No expiration (or 1 year)
4. Scopes to tick:
   - ✅ `repo` — full repo access (needed for private repo stats)
   - ✅ `read:user` — read user profile
   - ✅ `read:org` — read org membership
5. Click **Generate token** and copy it immediately

---

## Step 3 — Add the token as a repository secret

1. Go to your profile repo: `github.com/SiphiweRadebe/SiphiweRadebe`
2. Settings → Secrets and variables → Actions → **New repository secret**
3. Name: `METRICS_TOKEN`
4. Secret: paste the token you copied
5. Click **Add secret**

---

## Step 4 — Add the workflow file

Create this file in your profile repo:

```
.github/workflows/metrics.yml
```

Paste the contents of the `metrics.yml` file provided.

---

## Step 5 — Add the README

Replace your profile repo's `README.md` with the provided one.

---

## Step 6 — Run it for the first time

1. Go to your profile repo on GitHub
2. Click the **Actions** tab
3. Click **Metrics** in the left sidebar
4. Click **Run workflow** → **Run workflow**

The workflow will take ~5–10 minutes on first run. When it finishes,
you'll see the `.svg` files committed to your repo root, and the README
will display them automatically.

After that it runs automatically every day at midnight UTC.

---

## Optional: Enable private contribution counting

In your GitHub profile settings:
Settings → Contributions → tick **"Include private contributions on my profile"**

This makes the isometric calendar and stats count commits to private repos too.

---

## Troubleshooting

**SVG shows "not found"** — the workflow hasn't run yet, or failed. Check the Actions tab.

**Token error in logs** — make sure you used a *classic* PAT, not fine-grained.

**Workflow never commits** — check repo Actions permissions:
Settings → Actions → General → Workflow permissions → set to **Read and write permissions**

**Want to add more panels?** — browse plugins at:
https://github.com/lowlighter/metrics#-plugins
