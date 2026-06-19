# Cross-Domain Deception Detection via Extended DeCLaRatiVE Stylometry: Theoretically Motivated Features Across Six Communicative Domains

**Author:** Buse Duygun · BSc Data Science, Eindhoven University of Technology (TU/e)  
**Year:** 2025–2026

---

## Project Overview

This repository is the GitHub page for the bachelor thesis:

> *Cross-Domain Deception Detection via Extended DeCLaRatiVE Stylometry:Theoretically Motivated Features Across Six Communicative Domains*

---

## All Materials Are on OSF

> **This GitHub repository contains only this README.**
>
> All code, datasets, outputs, and documentation are archived on OSF:
>
> ## [→ Access the Full Project on OSF](https://osf.io/2s3wm/overview?view_only=f53e7a5cfb9b47dd9d0ace2b53cc9330)
>
> OSF contains:
> - `scripts.zip` — complete source code
> - `outputs.zip` — all pipeline outputs and results
> - `data_cleaned.zip` — processed domain-level datasets
> - `data.zip` — raw source datasets
> - `quick_feature_check_results.zip` — feature selection outputs

---

## What This Research Does

Deception leaves linguistic traces — but do those traces generalise across contexts? This thesis tests that question using a theory-driven set of **48 stylometric features** built under the **DeCLaRatiVE** framework, derived from six theories of deceptive language:

**Distancing (D) · Cognitive Load (CL) · Reality Monitoring (RM) · Verifiability (VE) · Interpersonal Motivation Theory (IMT) · Interpersonal Deception Theory (IDT)**

Text samples from **30 corpora** are grouped into **six deception domains**:

| Domain | Examples |
|---|---|
| `review_opinion` | Fake product/service reviews |
| `misinformation` | Fake news, political statements |
| `spoken_interpersonal` | Spoken deceptive interactions |
| `personal_narrative` | Personal stories and confabulation |
| `social_game` | Game-context deception (Mafia, etc.) |
| `legal_courtroom` | Courtroom testimony |

Three research questions are investigated:

- **RQ1** — Which stylometric features are stable indicators of deception across domains?
- **RQ2** — Which theoretical framework produces the strongest within-domain classifier?
- **RQ3** — Does inter-domain linguistic distance predict zero-shot transfer performance drop?

Models: **Logistic Regression · LinearSVC · XGBoost · DistilBERT**  
Experiments: English-only (Run 1) and Multilingual — EN, IT, NL, DE, ES (Run 2)

---

## GitHub vs OSF

| | GitHub | OSF |
|---|---|---|
| Purpose | Project overview and navigation | Complete archival source |
| Contains | This README | Code + data + outputs + documentation |
| Use for | Finding the OSF link | Downloading and reproducing everything |

---

## Contact

buseduygun01@gmail.com
