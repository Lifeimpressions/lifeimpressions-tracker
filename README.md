# Studio Tracker app: put it online (GitHub Pages)

This folder is the staff app: `index.html` (the whole app) and `config.js` (your Supabase address and public key).

## Before you start
Supabase must be ready: `01_schema.sql`, `02_staff.sql` run, and the access tests all PASS (see the Launch Guide).

## Step 1: Add your Supabase details
1. Supabase > Project Settings > API
2. Copy the **Project URL** and the **anon public** key into `config.js`
3. **Never** paste the `service_role` key or the database password anywhere in these files. The anon key is meant to be visible; the database rules protect the data

## Step 2: Publish on GitHub Pages
1. In your GitHub repository (public), upload `index.html` and `config.js` at the top level
2. Repository Settings > Pages > Source: **Deploy from a branch**, Branch: **main**, folder **/ (root)**
3. After a minute, the site is live at `https://<your-github-name>.github.io/<repository-name>/`

## Step 3: Tell Supabase the address
Supabase > Authentication > URL Configuration: set the Site URL to your GitHub Pages address.

## Step 4: First sign-in
1. Open the address and sign in as Keerthi
2. Check: the location filter shows all three locations; Settings lists all three staff
3. Sign out, sign in as Prabha: only Salem appears, and the location selector is missing
4. On each phone, open the address and choose **Add to Home Screen**

## What the app does with the database
| Action in the app | What the database does |
|---|---|
| New booking | Creates the customer, order and job; assigns the location's person; needs consent |
| Move a stage | Checks the rules (photo before layout, approval before fixing, QC before ready) and records who moved it |
| Upload a photo, layout or QC photo | Compresses to about 1 MB, stores it privately under the location's folder |
| Approve QC | Allowed for head office only (default) |
| Approve or request changes | Not possible from the app. Only the customer's WhatsApp reply can record it (needs the WhatsApp step) |

If a rule blocks an action, the app shows the database's message in plain words.

## Known limits of this version
- Messages appear in each job's phone panel only after the WhatsApp connection is built
- Prices, staff and stage targets are edited in Supabase's Table Editor for now
- The app loads all jobs on each refresh. That is fine at 15-20 orders a month; add paging if volume grows a lot
- The Supabase library loads from a public content network. For a locked-down version, host a copy of it in the repository
- Tested against a simulated Supabase (all screens, rules and errors). It has not yet run against your real project, so do the Step 4 checks and report anything odd
