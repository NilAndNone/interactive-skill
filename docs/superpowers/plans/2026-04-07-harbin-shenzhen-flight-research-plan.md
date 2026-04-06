# Harbin To Shenzhen Flight Research Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Execute the approved research spec and produce a source-backed report for `2026-05-05` flights from `哈尔滨 / 长春 / 牡丹江` to the `深圳坪山站` direction, including Top 3 itineraries and a purchase-timing recommendation.

**Architecture:** Use a docs-first workflow. Capture OTA search results in a normalized CSV, validate shortlisted itineraries against official airline channels, add non-Shenzhen ground-transfer data to `深圳坪山站`, then write a final report that separates verified facts from trend-based inference.

**Tech Stack:** Markdown, CSV, Git, browser-based OTA and airline searches, shell validation utilities (`rg`, `head`, `wc`, `awk`)

---

## Planned Files

- Create: `data/flight-research/2026-05-05/candidates.csv`
- Create: `data/flight-research/2026-05-05/evidence-log.md`
- Create: `data/flight-research/2026-05-05/ground-transfer-notes.md`
- Create: `data/flight-research/2026-05-05/trend-analysis.md`
- Create: `data/flight-research/2026-05-05/shortlist.md`
- Create: `docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`

## Route Matrix

All searches must stay inside this matrix:

- Origins: `哈尔滨 (HRB)`, `长春 (CGQ)`, `牡丹江 (MDG)`
- Destinations: `深圳 (SZX)`, `香港 (HKG)`, `澳门 (MFM)`, `广州 (CAN)`, `珠海 (ZUH)`, `惠州 (HUZ)`
- Date: `2026-05-05`
- Same-day arrival only
- Allow nonstop and connecting itineraries
- Minimum layover: `60` minutes
- Target arrival anchor: `深圳坪山站`
- Fare basis: adult, tax-inclusive, bare fare only
- Sources: airline official sites, 携程, 飞猪, 同程, 去哪儿, 航旅纵横

### Task 1: Scaffold The Research Workspace

**Files:**
- Create: `data/flight-research/2026-05-05/candidates.csv`
- Create: `data/flight-research/2026-05-05/evidence-log.md`
- Create: `data/flight-research/2026-05-05/ground-transfer-notes.md`
- Create: `data/flight-research/2026-05-05/trend-analysis.md`
- Create: `docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`

- [ ] **Step 1: Create the research directories**

Run: `mkdir -p data/flight-research/2026-05-05 docs/superpowers/research`
Expected: command exits with no output

- [ ] **Step 2: Seed the candidate table with the exact header**

```csv
captured_at,channel,origin_city,origin_airport,destination_city,destination_airport,airline,flight_numbers,depart_at,arrive_at,arrive_same_day,stops,stop_city,layover_minutes,listed_price_cny,price_basis,bookable,official_price_cny,official_checked_at,official_status,ground_mode_to_pingshan,ground_cost_cny,ground_minutes,total_minutes,risk_level,risk_notes,score,link_or_path
```

- [ ] **Step 3: Verify the CSV header is correct**

Run: `head -n 1 data/flight-research/2026-05-05/candidates.csv`
Expected:

```text
captured_at,channel,origin_city,origin_airport,destination_city,destination_airport,airline,flight_numbers,depart_at,arrive_at,arrive_same_day,stops,stop_city,layover_minutes,listed_price_cny,price_basis,bookable,official_price_cny,official_checked_at,official_status,ground_mode_to_pingshan,ground_cost_cny,ground_minutes,total_minutes,risk_level,risk_notes,score,link_or_path
```

- [ ] **Step 4: Seed the evidence log**

```md
# Evidence Log

## Search Parameters

- Captured on: 2026-04-07
- Travel date: 2026-05-05
- Origins: 哈尔滨 / 长春 / 牡丹江
- Destinations: 深圳 / 香港 / 澳门 / 广州 / 珠海 / 惠州
- Final comparison anchor: 深圳坪山站
- Fare basis: 成人含税裸票
- Constraints: same-day departure and same-day arrival, layover >= 60 minutes and preferably <= 6 hours

## OTA Capture

### 携程

### 飞猪

### 同程

### 去哪儿

### 航旅纵横

## Official Validation

## Notes On Price Conflicts
```

- [ ] **Step 5: Seed the ground-transfer notes**

```md
# Ground Transfer Notes To 深圳坪山站

## 深圳

## 香港

## 澳门

## 广州

## 珠海

## 惠州
```

- [ ] **Step 6: Seed the trend-analysis notes**

```md
# Trend Analysis Notes

## Verified Facts

## Neighbor-Date Comparisons

## 7 Day Window

## 14 Day Window

## 21 Day Window

## Inferences
```

- [ ] **Step 7: Seed the final report skeleton**

```md
# 2026-05-05 哈尔滨方向回深圳机票深度调研

## 1. 任务参数确认

## 2. 候选方案总表

## 3. Top 3 性价比方案

## 4. 最低价方案

## 5. 最省时间方案

## 6. 高风险备选方案

## 7. 购买时机判断

## 8. 重点监控路线

## 9. 简短结论摘要
```

- [ ] **Step 8: Commit the scaffolding**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/evidence-log.md data/flight-research/2026-05-05/ground-transfer-notes.md data/flight-research/2026-05-05/trend-analysis.md docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md
git commit -m "docs: scaffold flight research workspace"
```

### Task 2: Capture OTA Inventory Across The Full Matrix

**Files:**
- Modify: `data/flight-research/2026-05-05/candidates.csv`
- Modify: `data/flight-research/2026-05-05/evidence-log.md`

- [ ] **Step 1: Record the exact route matrix in the evidence log**

Add this checklist under `## OTA Capture`:

```md
Route matrix:
- HRB -> SZX / HKG / MFM / CAN / ZUH / HUZ
- CGQ -> SZX / HKG / MFM / CAN / ZUH / HUZ
- MDG -> SZX / HKG / MFM / CAN / ZUH / HUZ
```

- [ ] **Step 2: Search 携程 for all 18 origin and destination pairs and append every sellable same-day itinerary to the CSV**

For each CSV row:
- `captured_at` uses ISO-like local time, for example `2026-04-07T10:35+08:00`
- `channel` is `携程`
- `arrive_same_day` is `yes`
- `stops` is `0` for nonstop and `1` for a single connection
- `stop_city` and `layover_minutes` are empty only for nonstop rows
- `price_basis` is exactly `adult_tax_included_bare_fare`
- `bookable` is `yes` only if the source shows an actual purchase path
- `link_or_path` is a URL or a reproducible navigation note

- [ ] **Step 3: Search 飞猪 for the same 18 pairs and append every sellable same-day itinerary to the CSV**

Use the same capture rules as Step 2 and append `channel = 飞猪`.

- [ ] **Step 4: Search 同程 for the same 18 pairs and append every sellable same-day itinerary to the CSV**

Use the same capture rules as Step 2 and append `channel = 同程`.

- [ ] **Step 5: Search 去哪儿 for the same 18 pairs and append every sellable same-day itinerary to the CSV**

Use the same capture rules as Step 2 and append `channel = 去哪儿`.

- [ ] **Step 6: Search 航旅纵横 for the same 18 pairs and append every sellable same-day itinerary to the CSV**

Use the same capture rules as Step 2 and append `channel = 航旅纵横`.

- [ ] **Step 7: Add timestamped subsections for each OTA channel in the evidence log**

Each channel subsection must record:
- query start time
- query end time
- the date searched
- the route matrix covered
- notable gaps, for example “no results for MDG -> HUZ”
- pricing anomalies, if any

- [ ] **Step 8: Verify the raw inventory is not empty**

Run: `wc -l data/flight-research/2026-05-05/candidates.csv`
Expected: total line count is greater than `1`

- [ ] **Step 9: Verify every OTA channel has a subsection**

Run: `rg '^### ' data/flight-research/2026-05-05/evidence-log.md`
Expected:

```text
### 携程
### 飞猪
### 同程
### 去哪儿
### 航旅纵横
```

- [ ] **Step 10: Commit the OTA inventory**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/evidence-log.md
git commit -m "docs: capture ota flight inventory"
```

### Task 3: Validate Distinct Itineraries On Official Airline Channels

**Files:**
- Modify: `data/flight-research/2026-05-05/candidates.csv`
- Modify: `data/flight-research/2026-05-05/evidence-log.md`

- [ ] **Step 1: Dedupe the OTA inventory by `airline + flight_numbers + depart_at + arrive_at` and build a shortlist of distinct itineraries**

Use the deduped list to avoid searching official channels repeatedly for the same flight combination across multiple OTAs.

- [ ] **Step 2: For each distinct itinerary, search the relevant airline official site and record the official result**

Update these CSV columns for every row that belongs to the same itinerary:
- `official_price_cny`
- `official_checked_at`
- `official_status`

Allowed `official_status` values:
- `matched`
- `not_found`
- `site_unavailable`
- `not_directly_bookable`

- [ ] **Step 3: Record every official validation outcome in the evidence log**

Under `## Official Validation`, record:
- airline
- flight numbers
- validation time
- official result
- official price if found
- link or navigation path

- [ ] **Step 4: Record price conflicts in the dedicated section**

For any itinerary where an OTA price differs from the official price, add one bullet in `## Notes On Price Conflicts` with:
- itinerary identifier
- cheapest OTA price
- official price
- likely cause if visible

- [ ] **Step 5: Verify every captured row has an official status**

Run: `awk -F, 'NR>1 && $20=="" {print NR}' data/flight-research/2026-05-05/candidates.csv`
Expected: no output

- [ ] **Step 6: Commit the official validation pass**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/evidence-log.md
git commit -m "docs: validate flights against official channels"
```

### Task 4: Capture Ground Transfers To 深圳坪山站

**Files:**
- Modify: `data/flight-research/2026-05-05/candidates.csv`
- Modify: `data/flight-research/2026-05-05/ground-transfer-notes.md`

- [ ] **Step 1: For each non-Shenzhen destination city, find the fastest realistic same-day path to 深圳坪山站**

Cover these city buckets:
- 香港
- 澳门
- 广州
- 珠海
- 惠州

Each bucket must include:
- starting airport or arrival area
- primary transfer mode
- estimated fare in CNY
- total transfer minutes
- key operational risk

- [ ] **Step 2: Record the transfer notes under the correct city heading**

Every city section must end with a one-line recommendation such as:
- “default transfer path for scoring”
- “backup path if the default route misses the last train”

- [ ] **Step 3: Populate the ground-transfer columns in the candidate table**

Update for every row:
- `ground_mode_to_pingshan`
- `ground_cost_cny`
- `ground_minutes`

For direct Shenzhen arrivals:
- `ground_mode_to_pingshan` may be `metro_or_taxi_from_szx`
- `ground_cost_cny` and `ground_minutes` must still be filled with the best realistic same-day estimate

- [ ] **Step 4: Compute `total_minutes` for every candidate**

`total_minutes` must include:
- air travel time
- layover time
- ground-transfer time to 深圳坪山站

- [ ] **Step 5: Verify non-Shenzhen rows do not have missing ground-transfer data**

Run: `awk -F, 'NR>1 && $5!="深圳" && ($21=="" || $22=="" || $23=="") {print NR}' data/flight-research/2026-05-05/candidates.csv`
Expected: no output

- [ ] **Step 6: Commit the ground-transfer data**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/ground-transfer-notes.md
git commit -m "docs: add ground transfer scoring inputs"
```

### Task 5: Apply Hard Filters And Produce The Shortlist

**Files:**
- Create: `data/flight-research/2026-05-05/shortlist.md`
- Modify: `data/flight-research/2026-05-05/candidates.csv`

- [ ] **Step 1: Remove or mark any row that violates the approved hard constraints**

Disqualify rows that violate any of these:
- not same-day arrival
- layover under `60` minutes
- layover far beyond the preferred `6` hour ceiling
- wrong origin or destination city
- non-bare-fare price basis
- source outside the approved set

Use `risk_notes` to explain borderline cases instead of silently deleting them.

- [ ] **Step 2: Assign a risk level to every remaining row**

Allowed `risk_level` values:
- `low`
- `medium`
- `high`

Use the spec rules:
- low for nonstop or protected same-airport connections with comfortable timing
- medium for tighter same-airport or more tedious transfers
- high for self-built, cross-border-fragile, or near-minimum-connection paths

- [ ] **Step 3: Score the remaining candidates**

Use the approved weight model:
- `40%` listed price
- `20%` ground-transfer cost
- `25%` total minutes
- `15%` risk

Write the final normalized result into the `score` column. Lower is better.

- [ ] **Step 4: Write the shortlist summary**

Create `data/flight-research/2026-05-05/shortlist.md` with these sections:

```md
# Shortlist

## Top 3 By Score

## Lowest Fare

## Fastest Arrival To 深圳坪山站

## High-Risk Bargain Backup
```

- [ ] **Step 5: Verify every retained row has a score**

Run: `awk -F, 'NR>1 && $27=="" {print NR}' data/flight-research/2026-05-05/candidates.csv`
Expected: no output

- [ ] **Step 6: Commit the shortlist**

```bash
git add data/flight-research/2026-05-05/candidates.csv data/flight-research/2026-05-05/shortlist.md
git commit -m "docs: rank flight candidates and shortlist options"
```

### Task 6: Analyze Price Trend And Buying Window

**Files:**
- Modify: `data/flight-research/2026-05-05/trend-analysis.md`
- Modify: `data/flight-research/2026-05-05/evidence-log.md`

- [ ] **Step 1: Capture price-calendar or adjacent-date evidence for the top candidate routes**

Cover at least the neighboring dates:
- `2026-05-03`
- `2026-05-04`
- `2026-05-05`
- `2026-05-06`
- `2026-05-07`
- `2026-05-08`

- [ ] **Step 2: Record all directly observable facts under `## Verified Facts`**

Only include statements that are visible in a source at capture time, for example:
- price on a neighboring date
- official fare seen at a specific time
- visible low-price calendar pattern

- [ ] **Step 3: Fill the three time-window sections**

For `## 7 Day Window`, `## 14 Day Window`, and `## 21 Day Window`, write:
- what evidence supports waiting
- what evidence supports buying now
- what would invalidate the current view

- [ ] **Step 4: Write the inference section separately**

Under `## Inferences`, state:
- likely purchase window
- price threshold that should trigger booking
- routes that are most likely to produce a better alternative

- [ ] **Step 5: Verify the trend-analysis file contains both facts and inferences**

Run: `rg '^## ' data/flight-research/2026-05-05/trend-analysis.md`
Expected:

```text
## Verified Facts
## Neighbor-Date Comparisons
## 7 Day Window
## 14 Day Window
## 21 Day Window
## Inferences
```

- [ ] **Step 6: Commit the trend analysis**

```bash
git add data/flight-research/2026-05-05/trend-analysis.md data/flight-research/2026-05-05/evidence-log.md
git commit -m "docs: analyze price trend and buying window"
```

### Task 7: Write The Final Research Report

**Files:**
- Modify: `docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`
- Modify: `data/flight-research/2026-05-05/shortlist.md`

- [ ] **Step 1: Fill the parameter confirmation and candidate summary**

`## 1. 任务参数确认` must restate:
- travel date
- allowed origins
- allowed destinations
- same-day arrival rule
- layover floor
- fare basis
- final anchor at 深圳坪山站

`## 2. 候选方案总表` must summarize the retained rows, not the raw rejected rows.

- [ ] **Step 2: Write the Top 3, lowest fare, fastest, and high-risk backup sections**

Every recommended itinerary must answer:
- why it was selected
- who it fits
- main risk
- the price at which it stops being attractive

- [ ] **Step 3: Write the buying recommendation**

`## 7. 购买时机判断` must explicitly answer:
- buy now or wait
- latest date to keep watching
- booking trigger price
- which routes to monitor

- [ ] **Step 4: Write the final summary block**

`## 9. 简短结论摘要` must include these labels exactly:

```md
- 综合最优：
- 最低价：
- 最省时间：
- 建议购买时间：
- 重点监控路线：
```

- [ ] **Step 5: Verify the report headings**

Run: `rg '^## ' docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`
Expected:

```text
## 1. 任务参数确认
## 2. 候选方案总表
## 3. Top 3 性价比方案
## 4. 最低价方案
## 5. 最省时间方案
## 6. 高风险备选方案
## 7. 购买时机判断
## 8. 重点监控路线
## 9. 简短结论摘要
```

- [ ] **Step 6: Commit the final report**

```bash
git add docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md data/flight-research/2026-05-05/shortlist.md
git commit -m "docs: add harbin to shenzhen flight research report"
```

### Task 8: Final QA And Publish

**Files:**
- Modify: `data/flight-research/2026-05-05/candidates.csv`
- Modify: `data/flight-research/2026-05-05/evidence-log.md`
- Modify: `data/flight-research/2026-05-05/ground-transfer-notes.md`
- Modify: `data/flight-research/2026-05-05/trend-analysis.md`
- Modify: `data/flight-research/2026-05-05/shortlist.md`
- Modify: `docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`

- [ ] **Step 1: Run completeness checks on the candidate table**

Run: `awk -F, 'NR>1 && ($15=="" || $17=="" || $20=="" || $22=="" || $23=="" || $24=="" || $25=="" || $27=="") {print NR}' data/flight-research/2026-05-05/candidates.csv`
Expected: no output

- [ ] **Step 2: Run the placeholder scan on every deliverable**

Run: `rg -n 'TBD|TODO|todo|待补|占位' data/flight-research/2026-05-05 docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md`
Expected: no output

- [ ] **Step 3: Stage only the publishable research files and inspect the staged file list**

Run: `git add data/flight-research/2026-05-05 docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md && git diff --cached --name-only`
Expected:

```text
data/flight-research/2026-05-05/candidates.csv
data/flight-research/2026-05-05/evidence-log.md
data/flight-research/2026-05-05/ground-transfer-notes.md
data/flight-research/2026-05-05/shortlist.md
data/flight-research/2026-05-05/trend-analysis.md
docs/superpowers/research/2026-04-07-harbin-shenzhen-flight-report.md
```

- [ ] **Step 4: Create the publish commit**

```bash
git commit -m "docs: publish harbin to shenzhen flight research"
```

- [ ] **Step 5: Push the branch**

```bash
git push origin HEAD
```

- [ ] **Step 6: Capture the pushed commit hash in the report handoff**

First run:

```bash
git rev-parse --short HEAD
```

Expected: one short commit hash on stdout

Then append one final line to the report using that actual hash:

```md
> Published to Git at commit: abc1234
```
