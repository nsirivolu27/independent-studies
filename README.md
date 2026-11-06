# Independent studies in machine learning

Independent studies covering medical imaging, abstract reasoning, fraud detection, molecular identification, and language-model attribution.

## Completed research papers

| Study | Research paper | Status |
|---|---|---|
| [RSNA Knee Abnormality Detection](https://www.kaggle.com/competitions/rsna-knee-abnormality-detection) | [CNN Processing in Radiology: Data Preparation and Supervision in Knee MRI](papers/rsna-knee-data-audit.pdf) | **Complete** |
| [ARC Prize 2026 - ARC-AGI-2](https://www.kaggle.com/competitions/arc-prize-2026-arc-agi-2) | [Learning Rules from Examples: Reasoning and Evaluation in ARC-AGI-2](papers/arc-agi-2-research.pdf) | **Complete** |

Complete indicates the research paper is finished and published here. Kaggle submission status and leaderboard results require a separate submission record.

## Ongoing independent studies

The three ongoing studies use Kaggle datasets and evaluation protocols. Enrollment is complete, and the study targets follow the source competitions' written final submission timelines. Deadlines are at 6:59 p.m. New York time (23:59 UTC).

| Study and data source | Prediction task | Entry deadline | Target completion |
|---|---|---|---|
| [Predicting Credit Card Fraud](https://www.kaggle.com/competitions/playground-series-s6e11/overview) | Estimate the probability of fraud for each transaction | Nov 30, 2026 | **Nov 30, 2026** |
| [Enveda CASMI 2026](https://www.kaggle.com/competitions/enveda-casmi26-molecule-id-mass-spectra/overview) | Rank candidate molecular structures from tandem mass spectra | Dec 7, 2026 | **Dec 14, 2026** |
| [Name That LLM](https://www.kaggle.com/competitions/name-that-llm/overview) | Identify which of 18 language models wrote a passage | Jan 6, 2027 | **Jan 13, 2027** |

Kaggle's Name That LLM overview also displays a January 14 close date in its header. This tracker uses January 13, the earlier date specified under Timeline.

## Prediction scores

| Study | Metric | Local validation | Kaggle score |
|---|---|---|---|
| Predicting Credit Card Fraud | ROC-AUC | 0.9442151782771007 (CatBoost; Nov 6, 2026) | Not submitted; score unavailable |
| Enveda CASMI 2026 | Mean reciprocal rank at 25 | Pending | Pending |
| Name That LLM | Balanced accuracy | Pending | Pending |

## Research review — November 4, 2026

The linked Kaggle timelines still list November 30, December 14, and January 13 as the final submission deadlines. Training data and a reproducible baseline are needed for each project before the first local score can be recorded.

| Study | Proposed first experiment | Evaluation design |
|---|---|---|
| Predicting Credit Card Fraud | Compare logistic regression with categorical gradient boosting | Freeze a validation split after inspecting time and customer identifiers, fit preprocessing on training rows, and measure ROC-AUC on predicted probabilities. |
| Enveda CASMI 2026 | Establish a spectral-library retrieval baseline before attempting neural generation | Hold out molecular identities together, rank up to 25 unique structures, and use the organizer's structure matching and MRR@25. |
| Name That LLM | Start with character n-grams and a linear classifier | Group shared prompts and duplicate passages across the split where identifiers permit, fit the vocabulary on training text, and measure balanced accuracy. |

CatBoost's ordered boosting and categorical processing motivate the fraud comparison. DiffMS provides a later neural direction for molecular generation using a spectrum transformer and graph diffusion, conditional on suitable chemical formula information. Character n-gram authorship research motivates a lightweight text baseline. These are proposed experiments awaiting competition training data. [CatBoost](https://arxiv.org/abs/1706.09516v5), [DiffMS](https://arxiv.org/abs/2502.09571v2), [Character n-grams for authorship attribution](https://aclanthology.org/N15-1010/).

**Current access.** Fraud training data was downloaded on November 6 and the first local experiment is complete (see below). Enveda and Name That LLM still need training data. Kaggle API authentication was unsuccessful; the fraud submission CSV is ready locally, but submission and leaderboard score remain unverified.

### November 6 early review

Enveda's published rules specify CC BY-NC 4.0 for competition data, a maximum of five submissions per day, and selection of up to two final submissions. Its code competition runs offline with a nine-hour CPU or GPU notebook limit. Any molecular model comparison must fit that runtime, and data access remains subject to the competition rules. [Rules](https://www.kaggle.com/competitions/enveda-CASMI26-molecule-id-mass-spectra/rules), [code requirements](https://www.kaggle.com/competitions/enveda-CASMI26-molecule-id-mass-spectra).

For the proposed molecular retrieval baseline, record whether the correct structure exists in the candidate library for each held-out molecule. Retrieval cannot recover a structure absent from that library, so report candidate coverage alongside MRR@25. This is a planned diagnostic; execution awaits training data. At that early review, the fraud and language-attribution baselines also awaited data. The later fraud experiment is recorded below; no scored Kaggle submissions were verified.


## Fraud baseline — November 6, 2026

The downloaded data contains 699,960 labeled training transactions (11,689 fraud cases), 299,984 test transactions, and 24 predictors. There are no missing values or exact duplicate training feature rows; no train/test feature-hash overlaps were found. Transaction IDs are excluded from model inputs.

| Model | Local validation ROC-AUC |
|---|---|
| Logistic regression | 0.9410061337880624 |
| CatBoost | 0.9442151782771007 |

Both models use the same 139,992-row stratified development holdout with 2,338 positive cases (seed 20261106). The other 559,968 rows fit each comparison model. Logistic regression uses training-fitted standardization and one-hot encoding (C=1, maximum 500 optimizer iterations). CatBoost uses depth 6, learning rate 0.08, and at most 200 boosting rounds; early stopping uses a separate 55,997-row inner holdout and patience 80. The selected count is 197 rounds. Neither model uses class weights.

The higher validation AUC selects **CatBoost**, which is then refitted on all labeled rows. Validation is used for this model choice, so it is a development result, not an independent final estimate. No customer identifiers or full timestamps are supplied, preventing customer-grouped or chronological validation. These synthetic-data results do not establish real-world fraud-detection performance.

A local `submission.csv` contains 299,984 rows with the required `id,is_fraud` columns. File checks confirm exact test ID order, unique IDs, finite probabilities in [0,1], and no missing values. It has **not been submitted to Kaggle**; there is no verified public or final leaderboard score.

[Run evidence](results/fraud/2026-11-06-baseline.json) records unrounded scores, source-file hashes, split sizes and hash, package versions, parameters, and submission hash. The local script, saved split, predictions, and model are in ignored `artifacts/fraud-baseline/`; competition data is in ignored `data/`. Training code is retained locally pending publication through the competition's Kaggle sharing channel.

Re-run locally from this checkout: `.\.venv\Scripts\python.exe artifacts/fraud-baseline/train_baseline.py`. This path is local and is not included in the public repository. Source competition: [data](https://www.kaggle.com/competitions/playground-series-s6e11/data), [evaluation](https://www.kaggle.com/competitions/playground-series-s6e11/overview), [rules](https://www.kaggle.com/competitions/playground-series-s6e11/rules).
