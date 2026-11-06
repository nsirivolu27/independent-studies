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
| Predicting Credit Card Fraud | ROC-AUC | Pending | Pending |
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

**Access needed.** Open a signed-in Kaggle competition tab to enable the next data download and submission-history check. The November 6 review still found no competition training data in this project or competition-named downloads in the checked download directory. Authenticated submission history remains inaccessible. All three scores remain pending verification.

### November 6 follow-up

Enveda's published rules specify CC BY-NC 4.0 for competition data, a maximum of five submissions per day, and selection of up to two final submissions. Its code competition runs offline with a nine-hour CPU or GPU notebook limit. Any molecular model comparison must fit that runtime, and data access remains subject to the competition rules. [Rules](https://www.kaggle.com/competitions/enveda-CASMI26-molecule-id-mass-spectra/rules), [code requirements](https://www.kaggle.com/competitions/enveda-CASMI26-molecule-id-mass-spectra).

For the proposed molecular retrieval baseline, record whether the correct structure exists in the candidate library for each held-out molecule. Retrieval cannot recover a structure absent from that library, so report candidate coverage alongside MRR@25. This is a planned diagnostic; execution awaits training data. The fraud and language-attribution baselines also await their training data. No new experiments or scored submissions were verified in this review.

