# Planditor site plan: a Claude skill

Research and plan a website the way we plan every site: read the real Google results in the country you target, collect the keywords with their volumes, build a topical map, study the sites that rank, write one brief per page and a task list. **It plans only: it never writes the content.**

Everything Claude finds goes into the site's tabs in **Planditor** (SERPs, Keywords, Topical map, Competitors, Briefs, Tasks), so your team works from one plan.

## What you need
- **Planditor** with your site added. In the site, press **Plan with Claude** to get the site's connector and the start prompt.
- **Claude** (claude.ai, the desktop app or Claude Code) with that connector added.
- **Claude in Chrome** (claude.ai/chrome), so Claude can read Google results.
- **Niche Miner Lens** (Chrome Web Store, a free account works) in the same Chrome: it shows volumes, KD, each result's DR, People also ask and related searches on every Google results page.
- Optional: connect Niche Miner in Planditor's Search Console tab, so Claude can look up volumes for any list of keywords.

## How it runs
1. Paste the start prompt from Planditor ("Start the Planditor site plan for yoursite.com").
2. Claude asks three things: is the site live or a new domain, which country, and the topic in one line.
3. It reads the SERPs with Lens (pages 1 and 2, People also ask and related searches two levels deep), adds a live site's Search Console and audit, builds the map (a keyword becomes its own page only with real demand; the rest are sections and FAQs), studies the ranking micro and macro sites, then writes the briefs and the tasks.

The Planditor connector already gives Claude this same procedure (its `start_site_plan` tool), so the skill is optional there. Install it when you work in Claude Code or want Claude to know the steps before it connects.

## Install
- **Claude Code:** copy the `planditor-site-plan` folder into `~/.claude/skills/`.
- **claude.ai / desktop app:** Settings → Capabilities → Skills → upload the `planditor-site-plan` folder as a zip.

## Also here: planditor-site-launch
`planditor-site-launch/` puts a planned site live on **BMS by Rehan** (Cloudflare or your own Node.js hosting): it asks for the domain and where the site should run, downloads BMS from its public GitHub repo, walks you through the deploy, the domain and the admin, and records the launch in Planditor. In Planditor it is the **Launch with Claude on BMS** button, which works once the site's keywords are grouped and its topical map is ready, and only for a site that is not live yet. It writes no content. Best in Claude Code, which can run the download and the deploy for you.
