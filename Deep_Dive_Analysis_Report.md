# Deep-Dive Analysis Report — Retail Sales

**Dataset:** 992 orders · 947 unique customers · Jan 2025 – Jan 2026
**Companion file:** `Retail_Sales_Dashboard.xlsx` (interactive Excel dashboard)

## 1. Core KPIs

| KPI | Value | Why it matters |
|---|---|---|
| Total Revenue | ₹139.4M | Top-line health check |
| Average Order Value (AOV) | ₹139,399 | Value carried per transaction |
| Repeat Customer| 52 | The count or percentage of buyers who purchase more than once |
| Revenue per Customer | ₹147,201 | Average customer value acquired so far |
| Average Basket Size | 5.4 units | Cross-sell/bundling signal |

Full formulas live on the `KPI_Definitions` tab and recalculate from raw data.

## 2. Deep-Dive #1 — Cohort Analysis (Retention & LTV)

**Method:** Customers are grouped into monthly cohorts by their first purchase month. Each cohort's retention is tracked month-over-month, and cumulative revenue-per-customer is tracked as a running LTV curve.

**Finding:** Only 52 of 947 customers (5.5%) ever placed a second order — retention drops to roughly 0–1% by "Month 1" for almost every cohort. This isn't a data-quality issue; it's the headline result: **the business is acquisition-driven with almost no repeat-purchase engine.** LTV essentially equals first-order value for 94.5% of the customer base (₹147K average, driven almost entirely by order size, not repeat frequency).

**Implication:** Growth is currently capped by new-customer acquisition volume. A retention/reactivation program (even a modest post-purchase email or loyalty nudge) has outsized potential upside because the baseline is so low.

## 3. Deep-Dive #2 — Funnel Analysis (Customer Value Funnel)

**Method note:** The dataset has no clickstream/visit data, so a classic marketing funnel (visit → cart → purchase) isn't available. Instead, a **customer-value funnel** was built: every acquired customer, narrowed by spend tier and repeat behavior.

| Stage | Customers | % of Previous | % of Total |
|---|---|---|---|
| All Customers | 947 | — | 100% |
| Above-Median Spenders | 474 | 50.1% | 50.1% |
| Top-Quartile Spenders | 237 | 50.0% | 25.0% |
| Top-Quartile & Repeat Buyers | 32 | 13.5% | 3.4% |

**Finding:** The steepest drop-off (86.5%) is between "Top-Quartile Spenders" and "Top-Quartile & Repeat Buyers." Even customers who spend the most on their first order rarely return. Converting a modest share of that 237-customer top-quartile group into repeat buyers would be the single highest-leverage lever in this funnel — directly reinforcing the cohort finding above.

## 4. Deep-Dive #3 — Segmentation Analysis (RFM)

**Method:** Each customer is scored 1–4 on Recency, Frequency, and Monetary value (using the dataset's own quartile breakpoints — documented on `Customer_Summary`), summed into an RFM total, and mapped to a business-rule segment.

| Segment | Definition | Typical customer |
|---|---|---|
| Champions (RFM ≥ 11) | Recent, high-frequency, high-value | Rare — the ideal customer |
| Loyal Customers (9–10) | Strong recent spenders | Small group, close behind Champions |
| Potential Loyalist (7–8) | Often high one-time spend, not yet repeat | Largest actionable group |
| At Risk (5–6) | Below-average recency/value | Needs a win-back nudge |
| Lost / One-Time (< 5) | Low engagement, older/low-value orders | Largest overall share |

**Finding:** Because Frequency is nearly binary in this dataset (94.5% ordered exactly once), the segmentation is effectively driven by *how much* and *how recently* someone spent on their one order — not by loyalty behavior, since there's so little of it to measure yet. "Potential Loyalist" is the most actionable segment: high one-time spenders who haven't been given a reason to come back.

## 5. Recommendations

1. **Launch a post-purchase retention flow** targeted first at the 237 top-quartile spenders — this is where the funnel shows the sharpest, most fixable drop-off.
2. **Treat "Potential Loyalist" as a priority CRM segment** — they've already proven willingness to spend; a second-purchase incentive (discount, loyalty credit) directly tests the retention hypothesis.
3. **Track repeat-purchase rate as a primary KPI going forward** — at 5.5% today, even small improvements compound meaningfully given the ₹139K average order value.
4. **Re-run this analysis once click/visit-level data is available** to replace the value-tier funnel with a true conversion funnel.

## 6. How to Explore Further

Open `Retail_Sales_Dashboard.xlsx` → `Dashboard` tab → use the **City** and **Category** dropdown filters to see how revenue, orders, AOV, and the monthly trend shift by market and product line. All other analysis tabs (`Cohort_Analysis`, `Funnel_Analysis`, `Segmentation_RFM`, `Customer_Summary`) contain the full underlying formulas.
