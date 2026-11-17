---
name: planditor-site-launch
description: Put a planned site live on BMS by Rehan, step by step with a non-technical person - choose Cloudflare or ordinary Node.js hosting, download BMS from its public GitHub repo, deploy it, connect the domain, finish the admin setup, then record the launch in Planditor. Use when the user presses Launch with Claude on BMS in Planditor, or asks to launch / put live / set up BMS for a site whose keywords are grouped and whose topical map is ready. It does not write content.
---

# LAUNCH THE SITE ON BMS (Planditor)

You help ONE person put the site this connector belongs to live on **BMS by Rehan**, a CMS for fast content sites. They are usually not technical. The keyword research and the topical map are already in Planditor; this launch gets the empty site live and ready for its pages. **You do not write content here** (no articles, no page copy).

## Rules for working with them
- One step at a time. Say which window, which tab, which button. Wait for "done" or a screenshot before the next step.
- When they must type or paste something, give the LITERAL text in a code block, never a description of it.
- Never repeat passwords, database addresses, secrets, setup codes or tokens back in the chat once they exist: refer to the file they are in.
- If a screen looks different from what you expect, ask for a screenshot instead of guessing.
- If you can run commands on their computer (Claude Code, a terminal), run them yourself and report each result in one line. If you cannot (claude.ai in the browser), give each command in a code block and ask for the output, and suggest Claude Code for the next site: it does all of this for them.

## Step 0: is the site ready?
Read the site's Planditor tabs first (get_tab: keywords, topical-map; list_tabs). The launch tool already refused if the site is live or the map is empty; still check:
- The topical map has its pages, with hubs. Note the hub pages and the first pages of each topic: they decide the menu.
- The site is not live yet (the Sites dashboard: Stage not "published", Pages live empty or 0).
If something is missing, stop and tell them to finish the plan first (Plan with Claude).

## Step 1: three questions, all at once
1. The domain (no https://, no www). Is it bought already? Where (registrar)?
2. Where should it run?
   - **Cloudflare (recommended):** no hosting needed. One Cloudflare Workers Paid plan ($5 a month) covers all their sites. Needs a Windows PC with Docker Desktop. Fastest pages, nightly backups, the deploy is one command.
   - **Their own hosting:** cPanel with "Setup Node.js App" (Node.js 22), Plesk or a VPS, with a MariaDB 10.10+ or MySQL 8 database.
3. Windows or Mac? Is Node.js installed (`node -v`)? Is Git installed (`git --version`)?

## Step 2: download BMS from its public repo
Into a folder on their Desktop (Git, or the green **Code** button → **Download ZIP** on GitHub, then extract):
- Cloudflare: https://github.com/SynoxiaLLC2002/bms-by-rehan-cloudflare
  `git clone https://github.com/SynoxiaLLC2002/bms-by-rehan-cloudflare bms-cloudflare`
- Hosting: https://github.com/SynoxiaLLC2002/bms-by-rehan-mariadb
  `git clone https://github.com/SynoxiaLLC2002/bms-by-rehan-mariadb bms-<site>`
Read the repo's README.md first, then its guide (below). The repo's own guide wins over this file where they differ: it is updated with each release.

## Step 3a: Cloudflare
Follow the repo's **START-HERE.txt** exactly. In short:
1. Cloudflare account → Workers & Pages → Plans → **Workers Paid**.
2. **Docker Desktop** installed and open ("Engine running").
3. A site name: small letters, numbers and dashes, starting with a letter (from the domain: `example-site`).
4. In the folder (right-click an empty area → Open in Terminal):
   `powershell -ExecutionPolicy Bypass -File .\deploy.ps1 -Site <site-name>`
   First time: it installs packages (5 to 10 minutes) and prints a Cloudflare sign-in link: they open it in Chrome ON THE SAME PC and click Allow.
5. At "7/7 Done" it prints the site address, the admin setup link and a setup code. The file `sites/<site-name>.env` holds the site's secret keys: they keep it, never share it, never delete it.
6. The domain: add it to Cloudflare (Add a domain → Free plan → change the nameservers at the registrar → wait for "Active"), then run the same command with `-Domain <domain>`.

## Step 3b: their own hosting (MariaDB edition)
Follow the repo's **README.md**, **release/env.example** and **release/README.md** (parts of release/README.md and release/DEPLOY-PROMPT.txt were written for the older Postgres version: where they say Postgres or Neon, use MariaDB / MySQL; the rest of their hosting steps still apply). In short:
1. The domain in cPanel (Domains → Domains, UNTICK "Share document root"), DNS pointing at the host (Cloudflare in front recommended: A records, proxied, SSL Full (strict)), HTTPS valid.
2. cPanel → **MySQL Databases**: create a database and a user, Add User To Database with ALL PRIVILEGES. The address is `mysql://<cpaneluser_user>:<password>@localhost:3306/<cpaneluser_db>` (a password with @ : / ? # % must be percent-encoded). Check the server version is MariaDB 10.10+ or MySQL 8.
3. A folder for the app in the home directory, named after the site WITHOUT a dot (the folder with the dot belongs to the domain). Upload the files there, the way release/README.md says (built upload, never a Windows "Compressed folder" zip: it loses the Linux permissions and the host answers 503).
4. **Setup Node.js App** → Create Application: Node.js 22, Production, the app folder, the domain, startup file `server.js`. Environment variables from release/env.example: `DATABASE_URL`, `AUTH_SECRET` (generate a fresh one: `node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"`), `NEXTAUTH_URL=https://<domain>` (required: without it the admin login loops), `AUTH_TRUST_HOST=true`, `NEXT_PUBLIC_SITE_URL=https://<domain>`, plus what the file marks as recommended. On this kind of host the app reads these from that screen, not from a file.
5. **Run NPM Install**, then **Restart**. Open the domain: the first visit after a start can take 3 to 10 seconds.
If anything fails, read startup.log in the app folder before guessing.

## Step 4: the admin
1. Open `https://<domain>/admin/setup` (Cloudflare: the setup link from step 3a, with the setup code). Their name, email and a strong password; scan the QR code with an authenticator app (Google Authenticator, Microsoft Authenticator); the 6-digit code. Two-factor sign-in is required.
2. Admin → **Settings** → **Site URL** → `https://<domain>` → Save. Do this before any page: Google reads this address in every canonical tag and the sitemap.
3. Site name, language, logo (if they have one), the default share image.

## Step 5: ready for the pages (structure only, no content)
From the topical map, set up what the site needs before writing starts, and list the rest as tasks:
- The **menu**: the homepage and the hub pages of each topic, in the map's priority order (Admin → Menus). Create pages only if the person asks; never write their content.
- The pages every site needs before going public, as tasks: About, Contact, Privacy policy, Terms (and a disclaimer where the niche needs one).
- **Claude connector for the site**: Admin → Users → API tokens → a token for Claude, so the writing work later can use the site's own connector.
- Search Console: add the domain property (DNS check, the domain provider or Cloudflare), submit `https://<domain>/sitemap.xml` once the first pages are published. Then Planditor's Search Console tab → Connect Search Console.

## Step 6: record the launch in Planditor
- update_site: Platform "BMS (Cloudflare)" or "BMS (hosting)", Stage "brief" (pages not written yet), Notes: where it runs, the app folder or site name, the date. Never put passwords, secrets or setup codes in Planditor.
- add_rows on **tasks**: one row per page from the map in priority order (Type "new page", Stage "todo", Brief = the slug), plus the legal pages and the go-live checks (Site URL set, sitemap submitted, Search Console connected).
- Finish with a short summary: the site address, the admin address, what they still do themselves, and the next step (write the pages from the briefs).
