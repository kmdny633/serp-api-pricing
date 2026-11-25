# Cheap SERP API: What $0.15 to $12 per 1,000 Searches Buys — Cached vs Queued vs Live Results, Minimum Top-Ups, Credit Expiry, and a Full Plan Table

The published floor for Google SERP data sits between $0.15 and $0.60 per 1,000 searches, and almost nobody pays that on a first order. The $0.15 rate needs a $1,000 prepayment. The $0.60 rate comes back in about five minutes instead of five seconds. A $0.30 cached rate can describe a page that no longer looks like that. Four different products are being sold with the same unit label, and the provider you pick should depend on which one you actually need.

Here is what each price tier buys, where ScraperAPI's credit multipliers land it, and the three numbers worth checking before you pay anyone.

> **The short version**
> - **Raw SERP volume only, cheapest per query:** DataForSEO at $0.60 per 1,000 queued ($50 minimum), or Serper at $1.00 per 1,000 from a $50 pack.
> - **SERP plus page fetching plus JS rendering under one key:** ScraperAPI, where a Google request costs 25 credits and an ordinary page costs 1. The $49 Hobby plan carries 100,000 credits.
> - **Chasing the lowest headline rate:** budget $799 to $3,750 upfront and expect credits that expire in 90 days to 6 months.

👉 [See ScraperAPI's plans and current credit rates](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## The four products sold as "per 1,000 searches"

**Queued.** DataForSEO's Standard queue is $0.60 per 1,000 with a 45-minute target turnaround. Priority costs $1.20 per 1,000 and averages under a minute. Live mode costs $2.00 per 1,000 and returns in about six seconds. Same keyword, same JSON shape, three prices that differ by more than 3×.

**Cached.** serp.cheap advertises $0.30 per 1,000 cached searches against $0.60 fresh. Cached means the result set comes from an earlier crawl of that query, which is fine for a weekly trend line and useless for "what does this SERP look like right now." A cheap cached rate is not a like-for-like comparison with a live one, and the "about 10× cheaper than SerpApi" line on that page is the vendor's own framing rather than a third-party finding.

**Live.** What an AI agent or an on-demand rank check needs. You pay for it: DataForSEO charges $2.00 per 1,000 for six-second results, and SerpApi's entry plan works out to $25.00 per 1,000.

**Success-only.** Some providers bill every request, including the ones that fail on a captcha or a timeout. PrismCrawl, SerpApi, Bright Data, SearchCans and OpenSERP bill only successful calls. If your provider bills failures, its effective rate climbs with its error rate, and a 10% failure rate turns $0.50 into $0.56.

## What a Google search actually costs on ScraperAPI

ScraperAPI prices by domain, not by plan. A normal page costs 1 credit. Amazon costs 5. LinkedIn costs 30. Google and Bing, including all subdomains, cost 25. That ratio decides whether the service is cheap for your workload.

| Plan | Monthly credits | Price | Billing & validity | Get started |
| --- | --- | --- | --- | --- |
| Hobby | 100,000 | $49/mo | Monthly; unused credits reset at renewal; annual billing takes 10% off | [Start on Hobby](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Startup | Larger allowance than Hobby | Shown on the pricing page | Same monthly reset; requests return a 429 once credits run out | [See Startup pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Business | Larger allowance than Startup | Shown on the pricing page | Same monthly reset; no pay-as-you-go overage | [See Business pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Scaling | 5,000,000 | Shown on the pricing page | Adds pay-as-you-go overage at a fixed per-credit rate, with a spend cap you set | [See Scaling pricing](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Enterprise | Custom volume | Quote | Custom concurrency and support terms | [Ask for a quote](https://www.scraperapi.com/pricing/?fp_ref=coupons) |

Divide the Hobby price by its credits and one credit costs about $0.00049. A Google request consumes 25 of them, so $49 buys 4,000 Google searches, or roughly **$12.25 per 1,000**. DataForSEO's live mode is $2.00 per 1,000 and Serper's entry pack is $1.00 per 1,000. If Google SERPs are the only thing you need, ScraperAPI is not the cheap answer and it is worth saying so plainly.

The ratio flips when pages enter the job. An ordinary page costs 1 credit, so the same $49 covers 100,000 pages. A rank tracker that pulls the SERP and then fetches the top ten results for each keyword spends 25 + 10 = 35 credits per keyword. That is about 2,857 keywords for $49, or $17.15 per 1,000 keywords with the page content included, from one key and one invoice. Splitting the same job across a SERP vendor and a scraping vendor means two minimum purchases and two sets of expiring credits.

The Google endpoint itself is usable. ScraperAPI runs an async structured route that accepts a single query or a batch, takes `country_code`, `tld`, `hl`, `gl` and `start` for localisation and pagination, and posts results back to a webhook. Output is JSON or CSV. The published sample response returns an `organic_results` array with `position`, `title`, `snippet`, `link` and `displayed_link`. AI Overview blocks do not appear in that sample, so if AI Overview capture is a hard requirement, ask support before you buy rather than assuming.

👉 [Open the Google SERP endpoint page to see the JSON it returns](https://www.scraperapi.com/solutions/structured-data/google-search-scraper?fp_ref=coupons)

## Why $0.30 per 1,000 is rarely $0.30 per 1,000

One request is not one billing unit. This is the single most common reason a cheap quote turns into an expensive invoice.

ScraperAPI's multipliers, from its own documentation:

- Google and Bing: **25 credits** per request
- Amazon, Walmart, eBay: 5 credits
- LinkedIn: 30 credits
- Anti-bot bypass for Cloudflare, DataDome, PerimeterX, Akamai: **+10 credits**, applied automatically when the bypass logic activates
- `render=true`: +10 credits; `premium=true`: +10; `ultra_premium=true`: +30; `premium` plus `render`: 25; `ultra_premium` plus `render`: **75**

Every response carries an `sa-credit-cost` header showing what that individual request cost, which is the fastest way to catch a parameter quietly tripling your bill.

Other providers use the same trick with different numbers. Scrapingdog's Google SERP Light endpoint burns 5 credits per request and its Advance endpoint 10, so the headline rate applies to a fraction of a page. Its Google AI Mode endpoint costs 10 credits. Searlo's 1-credit rate covers the web search endpoint only: a full results page costs 3 credits, and 8 when an AI Overview has to be rendered in a browser. On DataForSEO, each additional 100 results multiplies the task price, up to 700 results. AI Overviews there come back inside the normal response with markdown and cited references, but they double the task price.

A provider quoting $0.30 per 1,000 for "a search" and a provider quoting $0.30 per 1,000 for "a page of ten organic results with no rendering and no AI Overview" are not quoting the same thing.

## Will you use the credits before they expire?

Prepaid credits that expire are a discount you never collect. ScraperAPI resets credits at each monthly renewal and unused credits are lost rather than carried forward, so the plan size should match your steady monthly volume, not your peak week. Annual billing is exactly 10% cheaper than monthly, which helps only if you are confident about the next twelve months.

The rest of the field is uneven. DataForSEO funds do not expire. Serper's credits last 6 months, SearchCans' 6 months, PrismCrawl's 90 days. An OpenSERP balance expires after 12 months without paid usage. If you run seasonal keyword sets, a 90-day clock and a 12-month clock are very different products at the same headline price.

Minimum purchases gate the cheap rates. Reaching $0.20 per 1,000 on Searlo requires $799. PrismCrawl's $0.15 rate requires $1,000. SearchCans' $0.56 rate requires $1,680, and Serper's $0.30 rate requires a $3,750 pack. DataForSEO asks for $50. A $0.15 rate you cannot reach is marketing; a $0.60 rate with a $50 entry is a price you can actually pay.

ScraperAPI advertises a 7-day trial with 5,000 credits on its Google Search product page, which is enough to run a few hundred real queries against your own keyword list before committing to a plan. Trial terms change, so confirm the current offer at signup.

👉 [Start on the $49 Hobby plan and check the trial terms](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## How the specialists compare

Prices below are the vendors' published rates, checked against their own pricing pages and two independent round-ups published in October 2026.

| Provider | Entry price / 1K | Lowest published / 1K | Minimum purchase | Credit validity | Note |
| --- | --- | --- | --- | --- | --- |
| DataForSEO | $0.60 queued | $0.60 | $50 | No expiry | Priority $1.20, live $2.00 |
| Serper | $1.00 | $0.30 at $3,750 | $50 | 6 months | 2,500 free queries |
| serp.cheap | $0.60 fresh | $0.30 cached | None stated | Not published | Vendor's own "cheapest" claim |
| PrismCrawl | $0.30 | $0.15 at $1,000 | $5 | 90 days | Figures from its own comparison post |
| Scrapingdog | $1.00 (Light) | ~$0.21 at $5,000/mo | $40/mo | Monthly plans | Light 5 credits, Advance 10 |
| SerpApi | $25.00 | $3.75 at $3,750/mo | $25/mo | Monthly plans | 250 free searches |
| OpenSERP | $0.50 | $0.50 at any volume | Not listed | 12 months idle | Success-only billing |

Two caveats on reading this table. Vendor-published comparisons, including PrismCrawl's own round-up, price their own product favourably and should be treated as claims rather than audits. And a "no published AI Overview support" note against a provider means exactly that: nothing was documented on the date checked. Serper's public pages, for instance, list `knowledgeGraph`, `peopleAlsoAsk` and `relatedSearches` in its sample response but no AI Overview endpoint. That is not proof the feature is absent, only that the public page does not describe it.

## Which one to buy

**Only SERP JSON, high volume, no page fetching.** DataForSEO's queued tier at $0.60 per 1,000, funded with $50 that never expires, is the lowest-risk cheap option. Move to live at $2.00 per 1,000 only for the queries that genuinely need current rankings.

**SERP results plus the page content behind them, or JS-heavy targets.** ScraperAPI earns its place here. Budget 25 credits per Google call, 1 credit per ordinary page, and 10 more whenever rendering is on. Run your own keyword list through the trial and read the `sa-credit-cost` header before choosing a tier.

**A small monthly volume with no tolerance for a large prepayment.** Serper's $50 pack with a 6-month clock, or SerpApi's $25/month entry plan if 250 free searches a month covers your testing.

**Agent workloads that need an answer in seconds.** Anything queued is the wrong purchase no matter how cheap it looks. Pay for live.

Three things to confirm before checkout, whichever provider you choose:

1. **Does the SERP endpoint bill at the same rate as the plan's headline?** Ask what one Google query costs in credits, not what one credit costs in dollars.
2. **Do unused credits survive the billing period?** Monthly resets and 90-day prepaid clocks both quietly raise your effective rate.
3. **Are failed requests billed?** On a 10% failure rate, success-only billing is worth about 11% of the headline price.

👉 [Compare ScraperAPI's current tiers and per-request credit costs](https://www.scraperapi.com/pricing/?fp_ref=coupons)
