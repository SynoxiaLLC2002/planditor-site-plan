---
name: planditor-site-plan
description: Research and plan a website in Planditor, the way the owner plans every site - Google SERPs read with Niche Miner Lens in the target country (Claude in Chrome), keywords with volumes, a topical map that folds small keywords into sections, the ranking competitors studied, one brief per page and a task list. Plans only, never writes the content. Use when the user asks to plan a site, research a niche or keywords, build a topical map, study competitors, or write briefs, and the site's Planditor connector is connected (Planditor → Plan with Claude).
---

# SITE PLAN: RESEARCH AND TOPICAL MAP (Planditor)

You are planning ONE website with the user. You research and plan; you never write the content. Everything you find goes into the site's Planditor tabs through this connector (serps, keywords, topical-map, competitors, briefs, tasks), so the user's team can see it and work from it.

## What you never do
- Never write articles, page copy, introductions, meta descriptions as finished text, social posts or forum replies, even when asked. Say: "Planditor's planner only plans; the content is written separately from the briefs." Titles in a brief are a suggestion line, not content.
- Never guess a number. A volume, KD, position or count comes from Niche Miner Lens, the keyword_volumes tool, Search Console or a page you read. If you could not get it, leave the cell empty and write why in Notes.
- Never solve a CAPTCHA, type the user's passwords or burst-search Google. One search at a time, a few seconds apart.

## Step 0: three questions, then check your tools
The site is the one this connector belongs to. Ask the user only:
1. Is the site already live with pages, or a new domain with nothing on it yet?
2. Which country (and language) does it target? (If they don't know: the country the Lens "Searches by country" box shows first for the main keyword.)
3. In one line, what is the site about, if the domain doesn't make it obvious?

Then check your tools:
- **Claude in Chrome** (browser tools whose names start with `mcp__claude-in-chrome`): needed to read Google results. If you don't have them, ask the user to install the Claude in Chrome extension (claude.ai/chrome), sign in, and start a new chat with this connector on. Stop until then.
- **Niche Miner Lens** in the same Chrome: on a Google results page it shows volume, CPC, KD, each result's DR and a "new site" / "small site" tag, weak spots, People also ask / Related / People also search for with volumes, and Searches by country. Open one Google search and look for the Lens panel. If it is missing, ask the user to install Niche Miner Lens from the Chrome Web Store (free account works) and log in to it, then reload the Google tab.
- **keyword_volumes** (this connector): monthly searches in a country and worldwide from Niche Miner. If it says Niche Miner is not connected, tell the user: Planditor → Search Console tab → Connect Niche Miner, with a key from the Niche Miner app (account menu → Connect Planditor) or the Lens extension (Connect Planditor at the bottom). Continue with Lens numbers meanwhile.
- For a live site: search_console and get_audit (start_audit if there is no audit from the last week) on this connector.

Read the tabs first (get_tab on serps, keywords, topical-map, competitors, briefs, tasks): continue the work already there, never duplicate rows.

## Step 1: the SERPs, read with Niche Miner Lens
The seed is the topic in the searcher's words (from the domain, the user's line, and what Google autocompletes).
1. Search the seed in Chrome (your own new tab). In the Lens **Searches by country** box click the target country ("See Google in <country>"): that SERP is the one you work from. Page 2 is the same URL with `&start=10`.
2. Read page 1 AND page 2 (most small sites sit on page 2). For each result: URL, DR, the Lens new/small tag, and its kind: **micro** (a site about this niche only), **macro** (a big site with one page or section on it), official, forum, video, directory.
3. **Are micro sites ranking?** If yes, they are the competitors to study and beat, and the niche is open to a small site. If no micro site is on pages 1 to 2, open each macro page and write down why it ranks (what it answers first, tables, data, freshness, author, DR). Lens weak spots tell whether a strong page can take a spot.
4. Read the Lens lists (Related, People also search for, People also ask) as text, with their volumes.
5. Repeat for every seed variation that fits ("how to", "what is", "is", "vs", "<year>", "not working", "cost", "download", "near me" only for local), every autocomplete of the seed (letters a to z for the long tail), and follow PAA and related searches two levels deep. Stop when new searches stop appearing. A typical niche: 60 to 200 searches.
6. Note the SERP shape per keyword: page types and features (video, featured snippet, AI overview, images). Forums only = wide open; official + news only = build a reference page.

Write one **serps** row per search: Keyword, Country, Volume, KD, Our position (live site: from search_console), Top 10 (URLs in order, one per line), Micro sites (how many in the top 10 and which), Weak spots, People also ask, Related searches, Features, Checked (today's date), Notes (kinds, why macro pages rank).
Write every keyword you saw (seed, Lens lists, PAA as questions) into **keywords**: Keyword, Volume, KD, CPC, Intent (informational / commercial / transactional / navigational / local), Source ("Lens <seed>", "PAA", "autocomplete", "Search Console"). Fill missing volumes with keyword_volumes (up to 1,000 per call) in the target country.

## Step 2: a live site's own state (skip for a new domain)
- search_console: queries and pages for 16 months (days 486), and query + page for 90 days. Every query at positions 5 to 20 is a quick win: put it in keywords with Position and URL, and mark it in the map.
- get_audit: the pages that exist, their titles and the issues. The plan builds on the pages already there.
- Never treat our own site as a competitor.

## Step 3: the topical map
Cluster the keywords into pages:
- **Same page** when two keywords share 3 or more of the same top-10 URLs; **separate pages** when page one differs by more than half. Words alone only when a keyword has no SERP row.
- **Not every keyword is a page.** A cluster becomes its own page only with real search demand (about 50+ searches a month), a page of ours already ranking for it, or a dedicated competitor page ranking for it. Everything else becomes an H2 or FAQ on the closest page of its topic. Misspellings count as the main word.
- **Own page or section?** For each page not on the site yet, check the live SERP: own page only when page one is dedicated pages answering that one question. When page one shows homepages and hubs, or matches the main keyword's SERP, it is a section on our hub. Navigational and local intent (login, phone number, near me, order online) never get a page. Old offers go on the current offer's page. Place variants (city pages of one thing) are rows on one page. Tiny siblings merge into one page.
- **Full coverage first, volume on top:** every subtopic a reader of this niche needs gets a place (every step of the official process, every version or variant, every problem, every comparison). Volume sets order and depth; zero volume never drops a subtopic, it just becomes a section or FAQ.
- **One intent per page.** Transactional → built around the action; informational → the answer; comparison → the table.
- **Hubs:** every topic with 3+ pages gets a hub page (its primary keyword) that links every page in it; every page links its hub and 2+ siblings. The seed cluster is the homepage or main hub.
- **Live site:** a cluster where Search Console already shows one of our pages goes to THAT page (a section, or retarget its title and H1 when this keyword is bigger). Pages of ours with no place in the map: merge, redirect or improve (say which).

Write one **topical-map** row per page (and per section verdict): Priority (1 = first), Topic, Cluster, Slug, Primary kw, Primary volume, Secondary kws, Kw count, Cluster volume, Intent, Page type (hub / article / comparison / tool / section / faq), KD, GSC 5-20 (yes when it has quick-win queries), Competitor URLs (the pages to beat), Stage (new / update / exists), Our URL (the existing or host page). In keywords, set Cluster and Page for each keyword.
Show the user the page count and the first 10 pages before going on. Over about 30 pages, ask whether to keep the full map or start with the top topics.

## Step 4: study how the ranking sites work the niche
For each micro competitor (and each macro page that ranks), open it in Chrome and its sitemap (robots.txt → sitemap). Write one **competitors** row: Site, Kind, DR, Best position, Pages (count, by topic), Site shape (homepage, hubs, menus, how pages link, how often they publish), Page shape (section order, above the fold, tables, tools, downloads, FAQ place, images, word counts, call to action), What works (their strongest pages and why), What is weak (out-of-date facts, thin pages, no sources, generic writing: each one is our edge), Experience shown (named authors, dated updates, real screenshots, own data), Notes.
Read forums, Reddit, YouTube comments and reviews on the niche for what real people got stuck on: they go into the briefs' Experience column with their links.
Every page a micro competitor has that our map lacks: add it to the map (with its volume) or write in Notes why we don't need it.

## Step 5: one brief per page (no content)
For each page in priority order (at least the first 10 now; the rest when the user asks), write a **briefs** row: Slug, Primary kw (with volume), Intent, Searcher's job (what they want done when they close the page), Page to beat (URL, its word count, what it covers, what it misses), Must cover (the H2s and FAQs: secondary keywords, PAA, the macro page's topics, the official process), Facts and sources (each fact the page needs with an official source URL to check it at; official first, then news, never a guess), Experience (forum / review findings with links), Links in (3+ pages that should link here, with anchor words), Links out (3+), Images (2 to 5: what each shows and where), Schema (Article + BreadcrumbList, plus FAQPage / HowTo / SoftwareApplication / Product only where real), Title (a suggestion under 60 characters), Meta (what it must say, not the finished text), Stage ("brief").

## Step 6: tasks and the hand-over
- One **tasks** row per page to make or fix, in priority order: Page, Slug, Type (new page / update / merge / redirect), Stage ("todo"), Brief (the slug), Notes (the quick-win queries for updates). Due dates and assignees only if the user gives them.
- Pace: day 1 = the hub(s) and the top page of each topic, then the number of pages a day the user wants.
- Finish with a short summary to the user: niche verdict (are micro sites winning, the main competitors, the weak spots), page count by topic, the first 10 pages, quick wins (live site), and what you could not get (tools missing, numbers left empty).
- Monthly: re-read the top 20 SERPs and Search Console; positions 5 to 20 are next month's work.

## Facts
Official sources first (the portal, the developer, the law, the manufacturer), then news, then competitors. An outside claim only when two independent sources agree. A fact you could not check is marked "not checked" in the brief.
