# Data Dictionary

This document describes the data fields used in Research Version 1.0. The project maintains a distinction between public-safe analysis files and private internal research files.

The public repository includes score and annotation data needed to reproduce the quantitative analyses, but it does not include full question text, raw model responses, private reference answers, or other source-derived materials that remain pending source and permission review.

## Public Analysis Dataset

File: `data/public_analysis_scores.csv`

This is the main public-safe dataset used by the final analysis notebook. It contains 120 rows, representing 30 questions evaluated across four models.

| Field | Description |
|---|---|
| `question_id` | Identifier for each benchmark question |
| `question_type` | Subject category: Statistics / Mathematics / Python & Introductory Computer Science |
| `difficulty_level` | Easy / Medium / Hard |
| `model_name` | ChatGPT / Claude / Grok / Qwen |
| `accuracy_score` | Accuracy score on the 0–3 evaluation rubric |
| `reasoning_completeness_score` | Reasoning Completeness score on the 0–3 evaluation rubric |
| `explanation_clarity_score` | Explanation Clarity score on the 0–3 evaluation rubric |
| `tutoring_effectiveness_score` | Tutoring Effectiveness score on the 0–3 evaluation rubric |
| `overall_score` | Equal-weight average of the four main evaluation criteria |
| `error_type` | General category of an identified response error; `none` when no error was recorded |
| `subject_specific_error` | More specific course-related error category; `none` when not applicable |
| `severity_level` | Severity of an identified error: Minor / Moderate / Severe / None |
| `overconfident_wrong_flag` | Yes / No; whether an incorrect or unsupported claim was presented with strong confidence |
| `learning_transfer_support` | Yes / Partial / No; whether the response supports transfer of the method or principle to similar future problems |
| `misconception_awareness` | Yes / Partial / No; whether the response identifies relevant common mistakes or misconceptions |
| `self_check_support` | Yes / Partial / No; whether the response provides an explicit checking, verification, debugging, or independent confirmation method |
| `confidence_calibration` | Good / Partial / Poor; whether assumptions, uncertainty, or ambiguity are handled appropriately |
| `cognitive_load_level` | Low / Medium / High; descriptive judgment of how mentally demanding the explanation is for a first-year student |

The learning-behavior fields are manually assigned descriptive annotations. Numerical values derived from these categories in the analysis notebook are used only for descriptive visualization and should not be interpreted as validated educational or psychometric measurements.

## Public Second-Rater Dataset

File: `data/public_second_rater_scores.csv`

This public-safe dataset contains the paired primary- and second-rater criterion scores used for the inter-rater reliability analysis. It contains 32 responses covering eight complete question blocks, representing 26.7% of the full response dataset.

| Field | Description |
|---|---|
| `question_id` | Question identifier used to match the rating pair |
| `model_name` | Model associated with the evaluated response |
| `accuracy_score_primary` | Accuracy score assigned by the primary rater |
| `accuracy_score_second` | Accuracy score assigned by the second rater |
| `reasoning_completeness_score_primary` | Reasoning Completeness score assigned by the primary rater |
| `reasoning_completeness_score_second` | Reasoning Completeness score assigned by the second rater |
| `explanation_clarity_score_primary` | Explanation Clarity score assigned by the primary rater |
| `explanation_clarity_score_second` | Explanation Clarity score assigned by the second rater |
| `tutoring_effectiveness_score_primary` | Tutoring Effectiveness score assigned by the primary rater |
| `tutoring_effectiveness_score_second` | Tutoring Effectiveness score assigned by the second rater |

The second rater did not independently assign an Overall Score for the reliability analysis. Inter-rater comparisons were conducted separately for the four main evaluation criteria.

The 32-response subset was purposively selected rather than randomly sampled. Model identities were visible during both primary and second-rater scoring.

## Private Internal Data

The local research workspace also contains internal files used for benchmark administration, scoring, auditing, and documentation. These files are excluded from the public repository.

### `data/questions.csv`

Internal question-level metadata may include:

| Field | Description |
|---|---|
| `question_id` | Identifier for each benchmark question |
| `question_text` | Current internal text representation of the question |
| `question_type` | Subject category |
| `difficulty_level` | Easy / Medium / Hard |
| `open_ended_flag` | Whether multiple valid solution paths, explanations, or implementations are possible |
| `public_release_status` | Release status of the question material; `pending_source_review` indicates that source and permission review is required before public release |
| `administered_question_text` | Text representation corresponding to the question as originally administered |
| `archival_normalized_question_text` | Later normalized archival representation used to improve internal reproducibility where necessary |
| `administered_context_note` | Internal note describing relevant context dependencies or differences between the administered and archival representations |

### `data/scored_responses.csv`

The complete internal response dataset additionally contains fields not released in the public analysis dataset, including:

| Field | Description |
|---|---|
| `raw_response` | Full response produced by the evaluated model |
| `model_version` | Model name or version displayed in the interface during collection |
| `date_collected` | Date of response collection |
| `error_notes` | Internal notes describing identified errors or relevant scoring context |
| `learning_behavior_notes` | Internal notes for important or ambiguous learning-behavior observations |

The internal dataset also contains the scoring, error-analysis, and learning-behavior fields represented in `public_analysis_scores.csv`.

### `data/second_rater_question_bank.xlsx`

Internal second-rater materials contain the responses and rating information used to conduct the second-rater evaluation. The public repository instead provides only the paired criterion scores required for reproducing the inter-rater reliability calculations in `public_second_rater_scores.csv`.

## Private Reference Answers

Private reference-answer materials are stored separately and are not included in the public repository.

These materials may contain:

| Field | Description |
|---|---|
| `question_id` | Question identifier used to link the reference material to the benchmark |
| `reference_answer` | Full professor-provided or course-derived answer used internally during evaluation |
| `expected_key_points` | Concepts, steps, formulas, or outputs expected in a full-credit response |
| `grading_notes` | Internal scoring guidance, including acceptable variations, assumptions, or partial-credit considerations |

Reference answers, expected key points, full question materials, and raw model responses remain private while their source and permission status is under review.