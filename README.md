
# Cross-Domain Deception Detection via Extended DeCLaRatiVE Stylometric Features

**Author:** Buse Duygun · BSc Data Science, Eindhoven University of Technology (TU/e)  
**Year:** 2025–2026  
**Contact:** buseduygun01@gmail.com

> **All materials (code, data, outputs, documentation) are on OSF.**  
> **[→ Access the Full Project Archive on OSF](https://osf.io/2s3wm/overview?view_only=f53e7a5cfb9b47dd9d0ace2b53cc9330)**

---

## Research Objective

Deception leaves linguistic traces — but do those traces generalise across contexts? A classifier trained on fake product reviews may fail entirely when applied to courtroom testimony or social game chat, even though both involve deliberate deception. This thesis investigates the **cross-domain generalisability** of theory-driven stylometric deception cues.

### What This Thesis Does

1. **Constructs a 48-feature stylometric framework** extending the DeCLaRatiVE framework (Loconte et al., 2023). Starting from 26 theory-grounded features, 29 additional features were coded, yielding a 55-candidate pool. A composite importance screening (mutual information + XGBoost gain + Spearman correlation) and theoratical information reduced this to **48 final features** grouped across six deception theories:

   | Theory | Code | # Features | Core Claim |
   |---|---|---|---|
   | Distancing | D | 10 | Deceivers use fewer first-person pronouns and more negative affect |
   | Cognitive Load | CL | 13 | Fabrication is cognitively harder → lower lexical diversity and syntactic complexity |
   | Reality Monitoring | RM | 8 | Fabricated accounts contain fewer sensory, spatial, and temporal details |
   | Verifiability | VE | 7 | Truthful statements reference specific, verifiable entities (names, dates, places) |
   | Information Manipulation | IMT | 5 | Deceivers violate conversational maxims in predictable ways |
   | Interpersonal Deception | IDT | 5 | In interactive settings, deceivers engage in strategic impression management |

2. **Assembles a cross-domain benchmark** from 30 corpora across 8 languages. After cleaning and deduplication, 145,854 rows are organised into 6 communicative domains. The pipeline then applies a language filter before model training: Run 1 uses English rows only (~137,995); Run 2 uses EN + IT + NL + DE + ES (Arabic, Russian, and Romanian are excluded).

   | Domain | Examples | Rows (after preprocessing) |
   |---|---|---|
   | `review_opinion` | Fake hotel/product/doctor reviews | 31,537 |
   | `misinformation` | Fake news, political statements | 84,435 |
   | `spoken_interpersonal` | Spoken deceptive interviews | 1,073 |
   | `personal_narrative` | Confabulated autobiographical accounts | 17,433 |
   | `social_game` | Mafia/Werewolf game deception | 9,716 |
   | `legal_courtroom` | Courtroom testimony | 1,660 |

3. **Trains and evaluates four models** — Logistic Regression, LinearSVC, XGBoost (primary), and DistilBERT (neural benchmark) — under three evaluation protocols:
   - **Within-domain 5-fold CV** (upper bound, in-domain performance)
   - **Zero-shot cross-domain transfer** (train on one domain, test on all others — 30 directed pairs)
   - **Leave-One-Domain-Out (LODO)** (multi-source generalisation)

4. **Answers three research questions**:
   - **RQ1**: Which features and theories produce *stable* deception signals across all six domains? (XGBoost SHAP coefficient of variation across domains — CL features are most stable)
   - **RQ2**: Which theory *dominates* within each domain? (Theory subset classifiers + SHAP dominance in joint model — domain-specific winners emerge)
   - **RQ3**: Does inter-domain *linguistic distance* predict zero-shot transfer failure? (Composite distance metric correlated with Macro F1 drop — H3 confirmed for all 4 models)

5. **Runs two experimental configurations**: English-only (Run 1) and Multilingual — EN, IT, NL, DE, ES (Run 2).

---

## Key Findings

- **Cognitive Load (CL) features** are the most domain-stable: `CL_type_token_ratio` (MATTR, CV=0.360) and `CL_hedge_density` (CV=0.517) maintain their importance regardless of domain.
- **Distancing (D) features** are the least stable: `D_positive_affect_rate` (CV=1.799) varies enormously by domain.
- **XGBoost** consistently outperforms LR and LinearSVC on within-domain CV; DistilBERT is best on large text-rich domains (misinformation) but worst on small or short-text domains.
- **Social game deception** is the hardest to transfer: LODO Macro F1 ≈ 0.19–0.25 across all models.
- **H3 confirmed**: Pearson r ≈ 0.66, Spearman ρ ≈ 0.64 (XGBoost, Run 1) — linguistically distant domains transfer worst.

---

## What Is on OSF

All materials are archived on OSF as ZIP files:

| ZIP File | What It Contains |
|---|---|
| **`scripts.zip`** | All pipeline scripts including `run_pipeline.py` (master runner) and `requirements.txt` and and `README.md` (full reproduction instructions) — all inside `scripts/`. One command reproduces everything: `python scripts/run_pipeline.py --skip-data-prep --skip-feature-check --skip-distilbert` |
| **`outputs.zip`** | Complete pipeline outputs for both experimental runs. Includes: within-CV results, LODO results, zero-shot transfer matrices, RQ1 SHAP stability tables, RQ2 theory subset F1 + SHAP heatmaps, RQ3 distance matrices + H3 JSON, and DistilBERT benchmark results (CV/LODO/transfer). Feature caches and Optuna JSONs included as checkpoints. |
| **`data_cleaned.zip`** | Six processed, deduplicated domain-level CSV files (145,854 rows total, label: 1=truthful / 0=deceptive) ready for the pipeline. |
| **`quick_feature_check_results.zip`** | Feature screening outputs: all 55 candidates ranked by composite importance, confirming the 7 dropped features and the final 48-feature set. |
| **`data.zip`** | Raw source datasets (30 corpora). Note: Russian Deception Bank is excluded (cannot be redistributed — see OSF readme for details). All other corpora included as received. |


---

## Dataset Access Requirements

> **Two datasets require a formal access request. Obtain them before reproducing the pipeline from raw data.**

| Dataset | Impact if absent |
|---|---|
| **MU3D** — Miami University Deception Detection Dataset (Lloyd et al., 2019) | `spoken_interpersonal` domain reduced from 1,073 to 753 rows. CV and LODO results for that domain will differ from reported values. **Must be obtained via signed user agreement before reproducing the pipeline.** |
| **Russian Deception Bank** (Litvinova et al., 2017) | 226 RU-language rows in `personal_narrative`. **Zero impact on any reported result** (Russian excluded from both pipeline runs). Obtainable directly from the original authors (Perm State University). |

Both datasets are commented out in `clean_all_datasets.py` with step-by-step re-enable instructions. All other corpora are in `data.zip` on OSF.

---

## GitHub vs OSF

| | GitHub | OSF |
|---|---|---|
| Purpose | Project overview and navigation | Complete, citable archival source |
| Contains | This README | Code + data + all outputs + documentation |
| Use for | Finding the OSF link and understanding scope | Downloading, reproducing, citing |

---

*Bachelor Thesis — Eindhoven University of Technology (TU/e), Data Science, 2026*
