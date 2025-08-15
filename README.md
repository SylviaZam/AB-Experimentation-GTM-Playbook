# AB-Experimentation GTM Playbook

Data-driven A/B testing playbook for Go-to-Market decisions.  
It ingests a public experiment dataset, runs statistical tests (two-proportion z-tests, confidence intervals, effect sizes), estimates **power** and **MDE**, and exports a stakeholder-ready Excel workbook plus a quick visual preview.

> **Skills showcased:** SQL-first thinking, Python for statistical rigor, experiment design, power/MDE, executive storytelling, reproducibility.

---

## What’s inside
- **Notebook:** [`notebooks/01_ingest_eda.ipynb`](notebooks/01_ingest_eda.ipynb)  
- **Sample Excel report:** [`notebooks/reports/ab_results_cookie_cats.xlsx`](notebooks/reports/ab_results_cookie_cats.xlsx)  
- **Preview chart:**  
  ![Summary chart](assets/summary_chart.png)

---

## Executive summary (from this run)
- **Day-1 retention:** Control = **44.82%**, Treatment = **44.23%** → **Δ = −0.59 pp**, **Lift = −1.32%**, **p = 0.0744**, **Significant @5%: No**  
- **Day-7 retention:** Control = **19.02%**, Treatment = **18.20%** → **Δ = −0.82 pp**, **Lift = −4.31%**, **p = 0.0016**, **Significant @5%: Yes**

**Recommendation:** Treatment underperforms on Day-7 retention with statistical significance. Keep **Control** as default, investigate the gating strategy behind Treatment, and consider a follow-up test with tighter success criteria. Day-1 shows no significant difference.

---

## Why this matters (GTM & Strategy roles)
- Turns raw experiment data into **clear investment recommendations** (lift, significance, uncertainty).
- Quantifies **tradeoffs** with **Minimum Detectable Effect** at 80% power.
- Produces **executive-ready artifacts** (Excel with formatted tables and charts) that non-technical stakeholders can use.

---

## Methods
- **Primary tests:** Two-proportion **z-tests** (two-sided), pooled SE under H0.  
- **Uncertainty:** 95% confidence intervals on absolute difference.  
- **Effect size:** **Cohen’s h** for proportions.  
- **Power & MDE:** Observed power at current sample sizes and **MDE** for 80% power (@ α = 0.05).  
- **Stratification sanity:** Optional cut by engagement deciles to check stability.

---

## Outputs
The notebook writes a formatted Excel workbook with:
- **Summary:** Control vs Treatment rates, absolute difference (pp), relative lift (%), p-value, Cohen’s h, significance flag, plus a bar chart.  
- **Power_MDE:** Observed power and MDE per metric.  
- **Variant Balance / Variant Metrics:** Sample balance and mean metrics by variant.  
- **Retention1 by Decile:** Sanity check across engagement deciles.

Open the sample: [`notebooks/reports/ab_results_cookie_cats.xlsx`](notebooks/reports/ab_results_cookie_cats.xlsx)

---

## Reproducibility
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
# open notebooks/01_ingest_eda.ipynb and Run All
