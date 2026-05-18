# SkyGeni Sequential Recommender

> A hybrid Markov + Association Rules engine that predicts the next product a B2B account will buy — built as a Practicum project at Santa Clara University in partnership with SkyGeni.

<p align="center">
  <a href="https://doriswang-me.github.io/-skygeni-recommender/">
    <img src="https://img.shields.io/badge/Live_Site-View_Demo-1a73e8?style=for-the-badge" alt="Live Site" />
  </a>
  <a href="SkyGeni_Project_Summary_Report.pdf">
    <img src="https://img.shields.io/badge/Report-Download_PDF-ea4335?style=for-the-badge" alt="PDF Report" />
  </a>
  <img src="https://img.shields.io/badge/Hit@1-68.29%25-34a853?style=for-the-badge" alt="Hit@1" />
  <img src="https://img.shields.io/badge/Hit@10-98.26%25-34a853?style=for-the-badge" alt="Hit@10" />
</p>

🔗 **Live site:** [doriswang-me.github.io/-skygeni-recommender](https://doriswang-me.github.io/-skygeni-recommender/)

---

## 📊 Headline Results

For each B2B account, given everything they've already purchased, the model predicts what they should be offered next:

| Metric | Value | What it means |
|---|---|---|
| **Hit@1** | **68.29%** | The model's #1 pick is exactly the next product purchased |
| **Hit@3** | 85.70% | Top-3 recommendations contain the correct product |
| **Hit@5** | 93.70% | Top-5 contains it |
| **Hit@10** | **98.26%** | Top-10 nearly always contains it |
| **MRR@10** | 0.78 | Mean reciprocal rank |
| **NDCG@10** | 0.83 | Ranked-quality score |

Evaluated on **3,510 accounts** with leave-last-out protocol on **33,589 purchase events** spanning **Mar 2020 → Mar 2026**.

---

## 🧠 Approach

The hybrid recommender combines **seven complementary signals** into a single ranked recommendation:

### Sequence signals
- **Markov-1** — "Buyers of *D* next purchase…?" (27% Hit@1 standalone)
- **Markov-2** — "Buyers of *C→D* next purchase…?" (27%)
- **Markov-3** — "Buyers of *B→C→D* next…?" (12%)
- **Markov-4** — "Buyers of *A→B→C→D* next…?" (2%)

### Co-occurrence signals
- **Association Rules — Confidence** — "% of D-buyers who also bought X" (21%)
- **Association Rules — Lift** — "How much more likely than random?" (6%)

### Lifecycle signal
- **Stage-aware Popularity** — "What do most accounts buy at their 5th purchase?" (10%)

### Cascading fallback
When a higher-order Markov state isn't found in training, its weight cascades to lower orders rather than being wasted — so the model gracefully degrades for accounts with short histories.

**Result:** combining all seven signals beats every single signal by 2.5× or more.

---

## 📁 What's in this repo

| File | Description |
|---|---|
| **`index.html`** | Project landing page with interactive demo and downloads |
| **`SkyGeni_Project_Summary_Report.pdf`** | 4-page report: scope, methodology, findings, benefits, next steps |
| **`sequential_recommender_results_V3.xlsx`** | Six sheets: Cover, Evaluation, Ablation, Coverage, Recommendations (35,100 rows), Methodology |
| **`SkyGeni26-v3.ipynb`** | Full Python pipeline: data loading, MarkovChain class, association rules, hybrid scorer, evaluation |

---

## 🎮 Try the Interactive Demo

The landing page includes a working demo: select any of 12 "most recent purchase" scenarios and instantly see the actual top-5 recommendations from real account data — with full per-signal score breakdown.

**[→ Try it now](https://doriswang-me.github.io/-skygeni-recommender/#demo)**

---

## 🚀 Proposed Next Steps

From the official report, prioritized by effort vs. impact:

| Extension | Effort | Expected gain |
|---|---|---|
| **Weight tuning** — 3-fold validation grid over the WEIGHTS dictionary | ~1–2 days | +1 to +3 points on Hit@5 |
| **Time decay in Markov fit** — exponential decay on transition counts | ~4–5 days | +2 to +5 points if catalog has churn |
| **Cohort ensembling** — cluster accounts by industry × size, blend per-cohort models | 2+ weeks | +3 to +8 points on cold-start accounts |

Longer-horizon: a neural sequential model (**GRU4Rec, SASRec**) that blends account- and product-level features with the sequence signal already captured here.

---

## 👥 Team

- **Doris Wang**
- **Liwen Chen**
- **Zenning He**
- **Faculty Advisor:** Sami Najafi

Santa Clara University · MSBA Practicum · May 2026

---

## 🛠 Tech Stack

- **Python** — pandas, numpy, openpyxl
- **Methods** — Higher-order Markov chains, association rule mining, leave-last-out evaluation
- **Frontend** — Vanilla HTML/CSS/JS (no framework)
- **Hosting** — GitHub Pages

---

<p align="center">
  <sub>© 2026 · A SkyGeni × Santa Clara University Practicum Project</sub>
</p>
