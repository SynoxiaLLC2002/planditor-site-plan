---
name: planditor-site-launch
description: Put a planned site live on BMS by Rehan, step by step with a non-technical person - choose Cloudflare or ordinary Node.js hosting, download BMS from its public GitHub repo, deploy it, connect the domain, finish the admin setup, then its content (the person's own articles, or written the way the person says), its design (BMS blocks and public UI/UX skills), its speed and the go-live checks, and record it all in Planditor. Use when the user presses Launch with Claude on BMS in Planditor, or asks to launch / put live / set up BMS for a site whose plan is done (keywords grouped, topical map and briefs ready).
---

# LAUNCH THE SITE ON BMS (Planditor)

You help ONE person put the site this connector belongs to live on **BMS by Rehan**, a CMS for fast content sites. They are usually not technical. The plan (keywords, topical map, briefs) is already in Planditor: it is the first step of the Planditor workflow, and this launch is the second. It takes the site from nothing to live: BMS deployed, the content in, a design of its own, fast pages, and the go-live checks. An SEO audit and the off-page plan come later, only when the person asks.

## Rules for working with them
- One step at a time. Say which window, which tab, which button. Wait for "done" or a screenshot before the next step.
- When they must type or paste something, give the LITERAL text in a code block, never a description of it.
- Never repeat passwords, database addresses, secrets, setup codes or tokens back in the chat once they exist: refer to the file they are in.
- If a screen looks different from what you expect, ask for a screenshot instead of guessing.
- If you can run commands on their computer (Claude Code, a terminal), run them yourself and report each result in one line. If you cannot (claude.ai in the browser), give each command in a code block and ask for the output, and suggest Claude Code for the next site: it does all of this for them.

## Step 0: is the site ready?
Read the site's Planditor tabs first (get_tab: keywords, topical-map; list_tabs). The launch tool already refused if the site is live or the map is empty; still check:
- The topical map has its pages, with hubs. Note the hub pages and the first pages of each topic: they decide the menu.
- The briefs exist for the first pages (briefs tab). The pages are written from them.
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

## Step 5: ready for the pages
From the topical map, set up what the site needs before writing starts, and list the rest as tasks:
- The **menu**: the homepage and the hub pages of each topic, in the map's priority order (Admin → Menus).
- The pages every site needs before going public, as tasks: About, Contact, Privacy policy, Terms (and a disclaimer where the niche needs one).
- **Claude connector for the site**: Admin → Users → API tokens → a token for Claude (with publish access only if they want Claude to publish), then add the site's own connector to Claude the way the BMS admin shows (Admin → Connect Claude). Steps 6 to 9 work through it.
- Search Console: add the domain property (DNS check, the domain provider or Cloudflare), submit `https://<domain>/sitemap.xml` once the first pages are published. Then Planditor's Search Console tab → Connect Search Console.

## Step 6: the content: ask first, then follow their way
Ask, in one message:
1. **Do you have the articles already?** (Their own writing, a writer's, a doc or a folder.) Then you post them **word for word**: never rewrite their words without their yes, sentence by sentence. You add only the on-page parts around them, from the page's brief: title (under 60 characters), meta description, headings where the text has none, internal links (3 or more in, 3 or more out, where the brief lists them), images with alt text, schema. List any problem you see (a fact that looks wrong, a missing section the brief asks for) and let them decide.
2. **Or should I write them?** Then ask: do you have your **own writing skill, instructions, style guide or examples** I should follow? Use exactly what they give you, together with each page's brief from Planditor (the facts and sources it lists, the questions it must answer). Do not use any other private method or skill for this: their way, their brief.
Either way: one page at a time in the briefs' priority order, saved as DRAFTS through the site's BMS connector, shown to the person before the next. Never invent facts, reviews, prices, phone numbers or experience. Mark each page's task "writing", then "review".

## Step 7: the design: BMS blocks and the UI/UX skills
1. **The skills first.** Use these design skills (all public; credit stays with their authors):
   - **frontend-design** (Anthropic): https://github.com/anthropics/skills, folder skills/frontend-design: the design plan (named brand colours, fonts chosen for the niche, one layout idea) checked against its list of AI-generated tells.
   - **unslop**: https://github.com/heydamir/unslop: removes the "AI-made" look (spacing, colour, icons, copy, type, layout).
   - **emil-design-eng**, **apple-design** and **break-ui** (Emil Kowalski): https://github.com/emilkowalski/skills, folder skills: polish and details, restraint and typography, then break-ui after building (long words, long FAQ answers, one-item grids, phone width).
   In Claude Code, if they are not installed, offer to install them (git clone each repo, copy the skill folders into ~/.claude/skills, start a new session). In claude.ai, read each SKILL.md from the repo and follow it.
2. **The site's own look**, from the niche and the competitors in Planditor (competitors tab): a palette, fonts, a homepage order and a page layout of its own, shown to the person before you build. Never copy a competitor's design.
3. **Build with BMS's own blocks.** get_blocks (summary first, then the types you will use, never guess prop names): hero, card grids, steps, FAQ accordions, tables, call-to-action bands and the rest. Settings and Customizer (colours, fonts, logo, header, footer) go live at once: say so before changing them.
4. Check every page type at phone width (render_document, or the live page) and fix what break-ui finds.
Avoid the AI-made look: an ALL-CAPS label above every heading, "Read more →" on every link, every section as the same rounded card, 01/02/03 badges on things that are not steps, one coloured word in each headline, fade-in on every section. One bold thing per page, the rest quiet.

## Step 8: speed
- Images: WebP, sized for where they show (no 3000-pixel photo in a 600-pixel box), alt text on each.
- BMS Admin → **Speed**: turn on what it offers for this host (on Cloudflare: Always Use HTTPS on in the Cloudflare dashboard).
- Measure, then fix: Google PageSpeed (pagespeed.web.dev) on mobile for the homepage, one hub and one article. Aim for green on Performance, Accessibility, Best Practices and SEO; fix the biggest item first and measure again.

## Step 9: go live
1. Publish in sets: a page together with everything it links to, never a page whose links point at drafts (or the person publishes in the admin when the token has no publish access).
2. Settings: Site URL right, search engines allowed, the sitemap opens (`https://<domain>/sitemap.xml`).
3. Search Console: add the domain, submit the sitemap; Bing Webmaster Tools too. Then Planditor's Search Console tab → Connect Search Console.
4. The contact form: Admin → Email, and a test message.
5. Click through the live site once on a phone: menu, links, forms, the call or contact buttons.

## Step 10: record the launch in Planditor
- update_site: Platform "BMS (Cloudflare)" or "BMS (hosting)", Notes: where it runs, the app folder or site name, the launch date. (Stage and Pages live follow the published pages by themselves.) Never put passwords, secrets or setup codes in Planditor.
- add_rows on **tasks**: one row per page from the map not written yet, in priority order (Type "new page", Stage "todo", Brief = the slug), plus the legal pages and any go-live check still open. Pages already published are marked by Planditor by itself.
- Finish with a short summary: the site address, the admin address, what is live, what they still do themselves, and the next step (the next pages from the briefs; later, when they want, the SEO audit and the off-page plan).
