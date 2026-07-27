# YouTube Trending Content Analytics: Ireland vs. GB, US & India

A business analytics + data analytics case study examining how YouTube's trending charts differ across four markets, and building a predictive model for how long a video stays trending.

**Business question:** Which content categories and markets should a platform like YouTube prioritize for creator investment — and is Ireland's trending market structurally different from larger English-speaking markets?

## Key findings

- **Ireland's trending chart has far lower content diversity** than GB, US, or India — only ~800 unique videos appeared over a 90-day window, versus 2,500-3,700+ elsewhere, despite similar total daily chart activity.
- Videos that do trend in Ireland **stay trending far longer** (~5.5 days on average vs. ~1.2-1.8 days elsewhere) and **reach higher peak view counts**, even outside of outlier cases.
- A **Random Forest model predicted trending duration with R² ≈ 0.68** (average error under half a day), outperforming Linear Regression and XGBoost. The single strongest predictor was **whether a video was trending in Ireland** — more influential than the video's own views or likes.
- Local Irish content can still break through despite this pattern (e.g. Kingfishr, a CMAT collaboration both reached Ireland's top-10 longest-trending videos).

## Repository structure
├── notebook/
│ └── youtube_trending_analysis.ipynb # Full analysis: EDA, modeling, exports
├── dashboard/
│ └── youtube_dashboard.pbix # Interactive Power BI dashboard (3 pages)
├── data/
│ └── (exported CSVs used by the dashboard)
├── report/
│ ├── executive_summary.docx
│ └── full_analytical_report.docx
└── README.md


## Methodology

**Data source:** [Trending YouTube Videos, 113 Countries](https://www.kaggle.com/datasets/asaniczka/trending-youtube-videos-113-countries) (Kaggle, updated daily).

**Scope:** Filtered to 4 markets (IE, GB, US, IN) over a rolling 90-day window.

**Approach:**
1. Data cleaning and exploratory analysis, including a check on unique-video counts to correct for repeat-appearance bias.
2. Content categorization via keyword pattern-matching on titles (iteratively refined; ~45% remain unclassified as "Other").
3. Three regression models (Linear Regression, Random Forest, XGBoost) trained to predict trending duration, compared on held-out test data.
4. Feature importance analysis on the winning model.
5. Results exported to a 3-page Power BI dashboard.

**Tools:** Python (pandas, scikit-learn, matplotlib, seaborn, xgboost), Google Colab, Power BI.

## Limitations

- Content categories are keyword-based, not from YouTube's own taxonomy — ~45% of videos fall into an "Other" bucket.
- `peak_views`/`peak_likes` are partly a consequence of `days_trending`, so some model accuracy reflects this relationship rather than a purely independent early-warning signal.
- Figures reflect a rolling 90-day window as of the most recent data pull and will shift slightly if re-run later, since the source dataset updates daily.

## Dashboard

The companion Power BI dashboard presents these findings across 3 pages:
1. **EDA & content findings** — market comparison charts, KPIs, interactive country filter.
2. **Predictive modeling** — model comparison and feature importance.
3. **Additional findings & methodology** — supporting evidence and honest limitations.

## Author

Built as part of a business analytics / data analytics portfolio project, targeting analyst roles at technology and consulting companies.
