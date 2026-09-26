# Deployment guide

Two one-time steps. After the first deployment, updates happen automatically
whenever you upload a new file to GitHub — you will not need to repeat the
Vercel step again.

## Step 1 — Put the files on GitHub

Repo: https://github.com/tech4life-123/wvstu-digital-campus

1. Open the repo link above.
2. Click **Add file → Upload files** (top right of the file list).
3. Drag in `index.html` and `vercel.json` from the zip Claude gave you.
   - If files with these names already exist in the repo, GitHub will ask
     to replace them — confirm that.
4. Scroll down, click **Commit changes**.

That's it for GitHub. The repo now has everything Vercel needs.

## Step 2 — Deploy on Vercel (first time only)

1. Go to **vercel.com/new** and make sure you're logged in as `wmopolu-8632`.
2. Click **Import Git Repository**.
3. Find `tech4life-123/wvstu-digital-campus` in the list and click **Import**.
   - If it's not listed, click "Adjust GitHub App Permissions" and grant
     Vercel access to that repository, then come back and it will appear.
4. Leave every setting on its default (no framework preset needed — it's
   a static file). Click **Deploy**.
5. Wait about 20–30 seconds. Vercel will show a live URL like
   `wvstu-digital-campus.vercel.app` — that's your working site.

## After that

Every time you upload a changed `index.html` to the GitHub repo and commit,
Vercel notices automatically and redeploys the new version within about
30 seconds — no need to repeat Step 2.

## How to know it's working

Visit the live URL and try logging in as the demo student
(`jamesdoe` / `Doe@2026`). If it works — no "Failed to fetch" error — the
site is correctly talking to Supabase. If you see "Failed to fetch" again,
send Claude the exact URL and what step you're on; that error specifically
means the page can't reach the database, which normally only happens if
it's still running under Claude's own preview link rather than the real
Vercel URL.

Test `/admin` and `/faculty` as their own separate URLs
(e.g. `wvstu-digital-campus.vercel.app/admin`) — each should show only its
own login form, with no way to find the others from the homepage.
