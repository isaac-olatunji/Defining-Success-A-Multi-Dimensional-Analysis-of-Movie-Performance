# Defining Success: A Multi-Dimensional Analysis of Movie Performance

**Analyst:** Isaac | isaactheanalyst
**Tools:** Power BI · Power Query · DAX
**Dataset:** TMDB — 1.4M+ movie records
**Competition:** Power BI DataViz World Championships — Final Round

---

## Executive Summary

How do filmmakers, directors, writers, studios, and investors actually know whether a movie has been successful?

This project challenges that question directly. The instinctive answers — high ratings, high revenue, popularity — each capture something real but individually incomplete. A film can be critically loved and financially invisible. A blockbuster can generate billions while receiving average audience scores. A micro-budget production can achieve an extraordinary return on investment that a studio blockbuster never could. True success requires measuring across all three dimensions simultaneously: audience reception, audience engagement, and financial performance.

Using a TMDB dataset of 1.4M+ records, the analysis is structured across four dashboard pages — each building toward a final synthesis in **The Verdict**, where financial and audience performance are plotted together in the Success Matrix to define what overall movie success actually looks like.

**Core finding:** A successful movie is not simply popular, highly rated, or profitable. It performs strongly across both audience and financial dimensions. These two axes are related but distinct — and neither alone is sufficient.

---

## Business Questions

1. What does the global movie landscape look like at scale?
2. How has movie production volume changed over time?
3. How are audience ratings distributed across the dataset?
4. Does audience engagement (vote count) correlate with rating quality?
5. How does the industry perform financially?
6. Does higher revenue automatically mean higher profit?
7. Does greater investment guarantee stronger returns?
8. What proportion of movies are financially profitable?
9. Does higher audience rating translate to higher financial profit?
10. How should movie success be defined when all dimensions are combined?

---

## Methodology

The analysis followed a structured Power BI workflow:

- **Data Connection** — TMDB dataset loaded into Power BI as `TMDB_Raw`
- **Data Cleaning (Power Query)** — duplicate removed, irrelevant columns dropped, data types standardised, invalid dates constrained, missing financial values handled, extreme values identified
- **Analytical Populations Defined** — full dataset, rated movies, financially observable (18K), financially reliable (~10K), and 25+ vote subset (44K) each defined separately before any metric was calculated
- **Feature Engineering (DAX)** — calculated columns and measures including financial profit, ROI, rating bands, vote bands, profitability status, reliable ROI, success quadrant classifications, and median-based KPIs
- **Dashboard Design** — four-page narrative: scale → commercial → audience → synthesis

### Key Methodological Decisions

**Valid financial records only:** Financial calculations were restricted to movies where both budget and revenue contained usable values. Division by zero and misleading ROI values were prevented by returning blank when inputs were invalid.

**Financially reliable subset:** A stricter population (~10K) was used for ROI analysis to reduce distortion from extreme outliers — distinguishing between financially observable (has data) and financially reliable (data is credible for ROI analysis).

**Median over average:** Where distributions were heavily right-skewed — particularly ROI — the median was used as the headline KPI. The mean ROI is heavily influenced by extreme micro-budget outliers; the median (77%) describes the typical movie more honestly.

**25+ vote threshold:** Raw ratings are noisy at low vote counts. A 25+ vote filter was applied for audience quality analysis to create a more meaningful and representative population.

**Logarithmic scaling:** Financial visualisations with extreme value ranges used logarithmic scaling to make the full distribution interpretable without distortion from outliers.

**Date constraint:** The original release date range extended from 1800 to 2099 — technically valid but analytically inappropriate. The release trend visual was constrained to 1900–2020 for a meaningful historical view.

---

## Page 1: Defining Success — Scale and Rating Overview

![Defining Success Dashboard](../Assets/screenshots/defining-success/defining-success-overview.png)

### KPI Overview

| Metric | Value |
| --- | ---: |
| Total Movies | 1M |
| Released Movies | 1M |
| Rated Movies | 360K |
| Financially Observable Movies | 18K |

**Insight:** The dataset contains 1M+ movies, but the further you move toward financial observability the smaller the pool becomes. Of 1M released movies, only 360K have been rated, and just 18K have sufficient financial data for profit analysis. This data availability gap is itself a finding — the vast majority of film production is financially invisible. All financial conclusions in this report apply to the financially observable subset, not the industry as a whole. The banner on this page makes this explicit: *"The Movie Universe is vast, but only a fraction provides sufficient audience or financial evidence to evaluate success."*

---

### Movie Production Has Expanded Dramatically Over Time

[!Movie Production Expanded Over Time](../Assets/screenshots/defining-success/movie-production-expanded-over-time.png)

**Insight:** The release trend chart — constrained to 1900–2020 to remove meaningless historical and future date noise — tells a clear story. Production remained near-zero through the early 20th century, began rising from the 1960s, and accelerated sharply from 2000 onward, reaching approximately 40K+ releases per year by 2020. The original dataset contained dates ranging from 1800 to 2099; constraining to 1900–2020 was a deliberate analytical decision, not just a visual preference. A technically valid date can still be analytically inappropriate.

---

### Most Rated Movies Sit in the Mid-to-High Rating Range

[!Rated Movies by Rating Band](../Assets/screenshots/defining-success/rated-movies-by-rating-band.png)

| Rating Band | Rated Movies |
| --- | ---: |
| Below 5 | 73K |
| 5 – 5.9 | 80K |
| 6 – 6.9 | 86K |
| 7 – 7.9 | 52K |
| 8+ | 69K |

**Insight:** The 6–6.9 band is the largest (86K), but the more analytically interesting observation is that the 7–7.9 band (52K) is smaller than the 8+ band (69K). Ratings appear to polarise rather than distribute normally — films tend to land in the average-to-good range or in genuinely acclaimed territory, with fewer in the moderately-good middle. This pattern likely reflects that films reaching a meaningful vote count are already a selected population of culturally visible titles.

---

### Higher Audience Participation Is Associated With Stronger Ratings

[!Rated Movies and Average Rating by Vote Band](../Assets/screenshots/defining-success/rated-movies-and-average-rating-by-vote-band.png)

| Vote Band | Rated Movies | Avg Rating |
| --- | ---: | ---: |
| 1 vote | 135K | 6.5 |
| 2–5 votes | 114K | 5.8 |
| 6–10 votes | 37K | 5.9 |
| 11–25 votes | 32K | 6.1 |
| 26–50 votes | 15K | 6.2 |
| 51–100 votes | 10K | 6.4 |
| 101–500 votes | 12K | 6.6 |
| 501–1K votes | 2K | 6.7 |
| 1K–5K votes | 3K | 7.2 |
| 5K+ votes | 1K | 7.2 |

**Insight:** The relationship between vote volume and average rating is consistent and directional — from 5.8 at 2–5 votes to 7.2 at 5K+ votes. This is a survivorship effect: films that attract large audiences tend to be higher-quality films. Crucially, this should be interpreted as an **association, not causation** — more votes does not cause higher ratings. Films that are better tend to attract more votes. The 25+ vote threshold used in the audience analysis is grounded in this finding: below that level, ratings are too noisy to carry analytical weight.

---

## Page 2: Commercial Success — Financial Performance

![Commercial Success Dashboard](../Assets/screenshots/commercial-success/commercial-success-overview.png)

### KPI Overview

| Metric | Value |
| --- | ---: |
| Total Revenue | $896.10bn |
| Total Budget | $340.75bn |
| Financial Profit | $563.55bn |
| ROI % | 207.9% |

**Insight:** The aggregate numbers appear impressive — $563.55bn in financial profit on $340.75bn in budget. But these figures are driven by extreme outliers, and the ROI of 207.9% does not represent the typical movie experience. The median film earns $148 in profit. The gap between headline aggregate performance and the typical movie's outcome is one of the most important stories on this page.

**Note on ROI display:** The redesign corrected the ROI KPI from a raw ratio (2.08) to a percentage (207.9%). Both represent the same figure but the percentage format communicates the investment return more intuitively.

---

### Higher Revenue Does Not Always Mean Higher Profit

[!Revenue vs Financial Profit](Assets/screenshots/commercial-success/revenue-vs-financial-profit.png)

**Insight:** The scatter plot reveals a heavily right-skewed distribution. Most financially observable movies cluster near $0bn in both revenue and profit — even among the 18K with financial data, most films generate modest returns. One extraordinary outlier at ~$1bn revenue and ~$25bn profit represents a film with an anomalously high profit-to-revenue ratio, likely reflecting a very low reported budget. This single observation materially inflates the aggregate metrics. Revenue and profit should never be treated as interchangeable — a movie generating significant revenue is not automatically financially successful once budget is accounted for.

---

### Profitability Can Only Be Assessed for a Small Share of Movies

[!Movies Profitability Status](../Assets/screenshots/commercial-success/movies-profitability-status.png)

| Profitability Status | Movies |
| --- | ---: |
| Insufficient Data | 1,451K |
| Profitable | 10K |
| Not Profitable | 8K |

**Insight:** Of 1M+ total movies, only 18K have enough financial data to assess profitability — and within that group, 10K are profitable vs 8K that are not. Roughly 55% of financially observable movies are profitable. The 1,451K movies with insufficient data represent the invisible majority of global film production. Financial success is both rare and hard to measure — the industry's actual profitability profile is substantially unknown.

---

### Higher Investment Does Not Guarantee Higher ROI

[!Budget vs ROI](../Assets/screenshots/commercial-success/budget-vs-ROI.png)

**Insight:** The Budget vs ROI scatter — displayed on a logarithmic x-axis to handle the extreme range of production budgets from thousands to hundreds of millions — reveals a clear inverse pattern. The highest ROI values concentrate at the lowest budget levels, sometimes reaching 10,000%+. As production budget increases toward $100M–$1bn, ROI compresses toward 0%. This is one of the most practically important findings for film investment: large budgets create the conditions for large absolute profits, but they do not produce efficient relative returns. Profit and ROI measure different things and should never be conflated.

**On the ROI population:** The chart uses the financially reliable population (~10K) rather than all financially observable movies (18K), because extreme outliers in the broader population would distort the visual even on a log scale. The distinction between financially observable and financially reliable was one of the most important modelling decisions in the project.

---

## Page 3: Audience Success — Engagement and Perceived Quality

![Audience Success Dashboard](../Assets/screenshots/audience-success/audience-success-overview.png)

### KPI Overview

| Metric | Value |
| --- | ---: |
| Movies with 25+ Votes | 44K |
| Median Rating (25+ Votes) | 6.39 |
| Median Profit | $148 |

**Insight:** Filtering to movies with 25+ votes leaves 44K films — a more meaningful audience-quality population than the full 360K rated set. The median rating of 6.39 is the genuine centre of audience perception for films with real audience participation. The median profit of $148 is the most important number on this page: even among films with meaningful audience engagement, the typical financial return is near-zero. Audience reception and financial success are not the same dimension.

---

### More Audience Participation Is Associated With Stronger Ratings

[!Audience Engagement](../Assets/screenshots/audience-success/audience-engagement.png)

**Insight:** The Audience Engagement scatter (Average Rating vs Popularity, bubble size = vote count) shows that popularity concentrates sharply in the 7–9 rating range. Below a rating of 6, almost no films achieve meaningful popularity. Above 7, a small number reach extreme popularity (2,500–3,000+), while the dense cluster of well-rated films sits below 500. Rating quality is a necessary but not sufficient condition for popularity — a film needs to be both good and culturally visible to achieve high engagement. The page title states this relationship clearly: *"Higher Audience Participation is Associated with Stronger Ratings, but Audience Reception alone doesn't guarantee Financial Success."*

---

### Higher Ratings Do Not Guarantee Higher Profit

[!Audience Rating vs Financial Performance](../Assets/screenshots/audience-success/audience-rating-vs-financial-performance.png)

**Insight:** Plotting Average Rating against Financial Profit reveals a weak relationship. The majority of movies — regardless of rating — cluster near $0bn in financial profit. The reference lines (median rating 6.39, median profit $148) confirm that most films land in the lower-left: below-median rating, near-zero profit. High-rated films (8+) do appear in profitable territory, but so do average-rated films. The upper-right quadrant — high rating, high profit — is sparsely populated. This visual makes the case for the Success Matrix that follows: audience and financial performance are distinct dimensions that must be evaluated separately before being combined.

---

## Page 4: The Verdict — Synthesising Movie Success

![The Verdict Dashboard](../Assets/screenshots/the-verdict/the-verdict-overview.png)

### KPI Overview

| Metric | Value |
| --- | ---: |
| Financially Observable Movies | 18K |
| Financial Profit | $563.55bn |
| Median Rating (25+ Votes) | 6.39 |
| Median Reliable ROI | 77% |

**Insight:** The Verdict page introduces a new metric not shown elsewhere: **Median Reliable ROI at 77%**. This replaces the aggregate ROI shown on the Commercial Success page with a more honest, representative figure. The reliable ROI distribution is heavily right-skewed:

| Percentile | Reliable ROI |
| --- | ---: |
| Median (P50) | 77% |
| P90 | 742% |
| P95 | 1,400% |
| P99 | 6,949% |

The extreme right tail explains why aggregate or average ROI is misleading — a tiny number of outliers at 6,000%+ pull the mean far above what the typical film achieves. The median of 77% is the honest figure: the typical financially reliable movie returns 77% on its investment.

---

### Success Matrix

[!Success Matrix](../Assets/screenshots/the-verdict/success-matrix.png)

The Success Matrix plots Financial Profit (x-axis) against Average Rating (y-axis) with reference lines at median profit ($148) and median rating (6.39), creating four analytical zones:

| Quadrant | Definition | Characteristics |
| --- | --- | --- |
| 🏆 Overall Success | High Rating + High Profit | Sparse — genuinely exceptional films |
| ❤️ Audience Favourite | High Rating + Low Profit | Most common — critically loved, financially modest |
| 💰 Commercial Performer | Low Rating + High Profit | Exists but rare — profitable despite average reception |
| 📉 Lower Overall Performer | Low Rating + Low Profit | Below median on both dimensions |

**Insight:** The Success Matrix makes the central finding visual. The vast majority of films — even those with financial data — cluster in the Audience Favourite quadrant: above-average ratings, near-zero financial profit. The Overall Success quadrant is sparsely populated, confirming that achieving both simultaneously is genuinely rare. The matrix is not a ranking tool — it is a classification framework that shows success is multidimensional and that the dimensions operate independently.

---

### What Defines Success?

[!What Defines Success](../Assets/screenshots/the-verdict/what-defines-success.png)

**Audience Reception Matters:** Higher-rated movies demonstrate stronger perceived audience quality, but rating alone does not guarantee financial success.

**Financial Performance Is Distinct:** Revenue and profit provide a separate dimension of success from audience reception. A film can excel on one and fail on the other.

**Success Is Multidimensional:** The strongest definition of movie success combines audience reception with financial performance rather than relying on a single metric.

---

### The Verdict

> *"A successful movie is not simply popular, highly rated, or profitable. It performs strongly across both audience and financial dimensions."*

---

### Key Learnings

**Industry Exploration:** Diving into the movies and series sector showed how data can be used to understand performance in a creative industry — a domain where success is subjective but measurable patterns still emerge.

**Data at Scale:** Cleaning and modelling 1.4M+ rows in Power Query sharpened the approach to structuring large datasets for fast, reliable analysis. The data availability gap — 1M+ movies, only 18K financially observable — was itself an analytical finding rather than just a limitation.

**A New Perspective on Success:** The project pushed beyond a single metric and asked what "success" actually means for a film — and how to measure it. The answer required building a framework, not just building charts.

**Business questions should determine the visuals.** The project evolved from asking *"what charts can I create?"* to *"what question does this visual help answer?"* That shift — from data to question — was the most important lesson from the redesign.

---

## Key Findings

| # | Finding |
| --- | --- |
| 1 | Of 1M+ movies, only 18K have sufficient financial data — the financially invisible majority cannot be assessed for profitability |
| 2 | Movie production expanded dramatically from 1900, with the sharpest acceleration from 2000 onward — reaching 40K+ releases per year by 2020 |
| 3 | Average rating rises consistently with vote count — from 5.8 (2–5 votes) to 7.2 (5K+ votes) — a survivorship effect, not a causation |
| 4 | The 7–7.9 rating band is surprisingly the smallest (52K); 8+ (69K) is larger — ratings polarise rather than cluster in the middle |
| 5 | Aggregate profit is $563.55bn but driven by extreme outliers; the median film earns $148 |
| 6 | Of financially observable movies, only ~55% are profitable — financial success is not the default |
| 7 | Budget and ROI have an inverse relationship — low-budget films achieve the highest ROI; large-budget films compress toward 0% |
| 8 | Median reliable ROI is 77%; P99 reaches 6,949% — the distribution is heavily right-skewed and the mean is a poor representative |
| 9 | High audience rating does not reliably predict high financial profit — most high-rated films still earn near-zero profit |
| 10 | The Overall Success quadrant (high rating + high profit) is sparsely populated — achieving both simultaneously is genuinely rare |

---

## Dashboard Design Philosophy

The redesigned dashboard was deliberately structured as an editorial data-storytelling narrative rather than a collection of independent charts.

**Design principles applied:**
- One dominant question per page
- Clear visual hierarchy — hero visual supported by evidence visuals
- Insight banners that state the analytical conclusion in plain language
- White rounded cards, transparent chart backgrounds, subtle shadows
- Consistent navigation (BACK / NEXT / HOME buttons)
- Reference lines that anchor scatter plots to meaningful benchmarks
- Logarithmic scaling where financial value ranges require it
- Final takeaway statement on each page

**Tooltip philosophy:** Tooltips were treated as a context layer, not a duplication layer. Each tooltip adds relevant supporting information — movie title, vote count, revenue, budget, profit — depending on what the visual is investigating. No tooltip repeats information already visible on the chart axes.

---

## What I Would Do Differently

1. Define the analytical framework and populations before building any visuals
2. Profile the dataset for invalid dates, zero values, and extreme observations before deciding which fields are usable
3. Identify the correct analytical population for each question separately
4. Separate the financially observable and financially reliable populations from the start
5. Create only the measures required by the analytical framework
6. Design the dashboard after establishing what the evidence actually shows — not before

---

## Recommendations

### 1. Use a Multi-Metric Framework for Success Evaluation
Rating, revenue, or ROI alone is incomplete. Films should be evaluated across at least two dimensions: audience reception and financial performance. The Success Matrix provides a practical classification framework.

### 2. Treat Financial Data as a Subset, Not the Industry
Only 18K of 1M+ movies have observable financial data. All financial conclusions apply to a high-visibility subset. Independent and low-budget films dominate the invisible majority and are systematically underrepresented.

### 3. Use Median Reliable ROI, Not Aggregate or Average ROI
Aggregate and average ROI are distorted by extreme micro-budget outliers. The median reliable ROI (77%) is far more representative of the typical financially reliable film's investment return.

### 4. Apply a Vote Threshold Before Analysing Ratings
Raw ratings below 25 votes are too noisy to carry analytical weight. Any audience quality analysis should apply a minimum participation threshold.

### 5. Distinguish Profit from ROI in Investment Decisions
Profit measures the absolute size of the financial outcome. ROI measures the efficiency of the investment. A large-budget film can generate substantial absolute profit while producing a modest ROI. Both metrics are needed — neither alone is sufficient.

---

## Conclusion

The question this project set out to answer — what makes a movie successful? — turns out to be genuinely complex. The data does not support a single answer.

Financial profit is real and measurable, but concentrated in a tiny fraction of productions and driven by outliers. Audience ratings are a meaningful signal of perceived quality, but do not reliably predict financial return. ROI can be extraordinary for micro-budget films but compresses toward zero as investment scale increases. Popularity is correlated with quality but not determined by it.

The Success Matrix is the clearest output of this analysis: a practical tool for classifying films not by a single number, but by their position across two independent dimensions. Films in the Overall Success quadrant — high rating, high profit — are rare precisely because they require excellence on both axes simultaneously.

The data at scale reinforces a truth the creative industry already knows intuitively: most films do not succeed commercially, most films do not achieve lasting audience recognition, and the ones that do both are genuinely exceptional.

> *"A successful movie is not simply popular, highly rated, or profitable. It performs strongly across both audience and financial dimensions."*
