🎬 Defining Success: A Multi-Dimensional Analysis of Movie Performance

Show Image

Tools: Power BI · Power Query · DAX Dataset: TMDB — 1.4M+ movie records across ratings, revenue, budget, and audience engagement

A Power BI analysis of 1.4M+ movie records exploring what makes a film successful across audience reception, engagement, and financial performance — culminating in a Success Matrix that evaluates performance across all three dimensions.

Project Overview
This project explores what it truly means for a movie to be successful. Rather than defaulting to a single measure — ratings, revenue, or popularity — the analysis builds a multi-dimensional framework that evaluates films across both audience and financial performance.

The dashboard spans four pages, each building progressively toward a final synthesis: The Verdict, which classifies movies into four success quadrants and answers the central question the project sets out to resolve.

Business Problem
Success in the film industry is subjective by nature — but it is also measurable. The challenge is that the most common measures (ratings, box office revenue, popularity) each capture something real while missing something important.

This analysis was designed to answer: when all dimensions are measured together, what does a truly successful film look like — and how rare is it?

Dataset Overview
Attribute	Detail
- Total Records	1M+ movies
- Rated Movies	360K
- Financially Observable	18K (budget + revenue available)
- Source	TMDB (The Movie Database)
- Key Metrics	Rating, Vote Count, Revenue, Budget, Profit, ROI, Popularity

Tools & Techniques
- Power Query — data cleaning, duplicate removal, column selection, type standardisation
- DAX — calculated columns and measures including financial profit, ROI, rating bands, vote bands, profitability classification, and success quadrant logic
- Power BI Visuals — KPI cards, scatter plots, bubble charts, bar charts, line charts, and a custom Success Matrix

Dashboard Structure
Page	Title	Focus
1	Defining Success	Dataset scale, production history, rating and vote band distribution
2	Commercial Success	Revenue, budget, financial profit, ROI, profitability status
3	Audience Success	Engagement patterns, rating vs popularity, rating vs financial performance
4	The Verdict	Success Matrix synthesis, what defines success, key learnings

Key Findings
Finding	Detail
- Data Availability Gap	Only 18K of 1M+ movies have financial data — the financially invisible majority cannot be assessed
- Production Peak	Movie releases peaked at ~50K/year around 2010; post-2015 drop reflects data lag, not industry decline
- Vote-Rating Relationship	Average rating rises from 5.8 (2–5 votes) to 7.2 (5K+ votes) — survivorship effect confirmed
- Profitability Rate	Only ~55% of financially observable movies are profitable — success is not the default
- Budget vs ROI	Inverse relationship — micro-budget films can achieve extraordinary ROI; large budgets compress returns
- Median Film Profit	$148 — even among audience-engaged films, the typical financial return is near-zero
- Rating ≠ Profit	High audience ratings do not reliably predict high financial profit
- Overall Success is Rare	The high rating + high profit quadrant is sparsely populated — achieving both is genuinely exceptional
  
Dashboard Preview
Defining Success — Overview Page
Show Image
Commercial Success
Show Image
Audience Success
Show Image
The Verdict — Success Matrix
Show Image

Business Impact
This analysis reframes how movie performance should be evaluated. The core insight — that financial and audience success are related but distinct dimensions — has practical implications for how studios, analysts, and investors assess film performance.

Key takeaways:
- A multi-metric framework (audience + financial) is more meaningful than any single KPI
- Financial data covers only a small fraction of global production — conclusions must be scoped accordingly
- Budget size does not reliably predict ROI — mid-to-low budget films with strong audience engagement represent undervalued opportunities
- The Success Matrix provides a practical classification tool: Overall Success, Audience Favorite, Commercial Performer, or Lower Overall Performer

"A successful movie is not simply popular, highly rated, or profitable. It performs strongly across both audience and financial dimensions."

Repository Structure
text
defining-success-movie-analysis/
│
├── README.md
│
├── Assets/
│   ├── cover/
│   │   └── cover.svg
│   └── screenshots/
│       ├── defining-success/
│       ├── commercial-success/
│       ├── audience-success/
│       └── the-verdict/
│
└── Analysis Report/
    └── Defining_Success_Analysis_Report.md


Detailed Analysis Report
For complete methodology, page-by-page analysis, all dashboard insights, and strategic recommendations:
📖 View Full Analysis Report

Author
Isaac Olatunji Business Intelligence Analyst focused on transforming data into actionable business insights through SQL, Power BI, Excel, and data storytelling.
GitHub: isaactheanalyst
