# Data Dictionary

## Basic Response Fields

| Fields | Contents |
|---|---|
| `question_id` | Question ID for recording each question |
| `question_text` | Full text of the question |
| `question_type` | Subject category: Statistics / Mathematics / Python & Introductory Computer Science |
| `difficulty_level` | Easy / Medium / Hard |
| `model_name` | ChatGPT / Claude / Grok / Qwen |
| `model_version` | The name displayed on the actual interface |
| `raw_response` | The answer provided by AI |
| `date_collected` | Date of response collection |
| `open_ended_flag` | Whether the question allows multiple valid solution paths, explanations, or code implementations |
| `public_release_status` | Indicates the current public-release status of the question material. "pending_source_review" indicates that source/licensing review is required before public release |

## Main Score Fields

| Fields | Contents |
|---|---|
| `accuracy_score` | Score for accuracy on each AI (0–3) |
| `reasoning_completeness_score` | Score for completeness on each AI (0–3) |
| `explanation_clarity_score` | Score for clarity on each AI (0–3) |
| `tutoring_effectiveness_score` | Score for how effectively the response supports freshman-level learning as a study assistant (0-3) |
| `overall_score` | Average numeric value of the four main scoring criteria. Error analysis fields and learning behavior tags are not directly included |

## Error Analysis Fields

| Fields | Contents |
|---|---|
| `error_type` | Type of error that the model makes |
| `subject_specific_error` | Type of more specific course error |
| `severity_level` | Minor / Moderate / Severe / None |
| `overconfident_wrong_flag` | Yes / No; whether the model gives an incorrect or unsupported answer with strong confidence |
| `error_notes` | Optional notes describing the identified error or relevant scoring context |

## Learning Behavior Observation Tags

| Fields | Contents |
|---|---|
| `learning_transfer_support` | Yes / Partial / No; whether the response helps students apply the method to similar future problems |
| `misconception_awareness` | Yes / Partial / No; whether the response points out common mistakes or misconceptions |
| `self_check_support` | Yes / Partial / No; whether the response provides checking, verification, or debugging methods |
| `confidence_calibration` | Good / Partial / Poor; whether the response handles assumptions, uncertainty, or ambiguity appropriately |
| `cognitive_load_level` | Low / Medium / High; how mentally demanding the explanation is for a first-year student |
| `learning_behavior_notes` | Optional notes for important, ambiguous, or case-study-worthy learning behavior observations |

## Second-Rater Evaluation

| Item | Description |
|---|---|
| `second_rater_file` | Ratings from the independent second-rater evaluation are stored in `data/second_rater_question_bank.xlsx` |
| `sample` | 32 responses covering eight complete question blocks (26.7% of the full response dataset), selected purposively for inter-rater reliability analysis |
| `matching_fields` | Second-rater responses are matched with the primary dataset using `question_id` and `model_name` |
| `scoring_fields` | Reuses `accuracy_score`, `reasoning_completeness_score`, `explanation_clarity_score`, and `tutoring_effectiveness_score` as defined above, using the same 0–3 rubric |
| `learning_behavior_fields` | Reuses the learning-behavior observation fields defined above |
| `overall_score` | Not independently assigned by the second rater; it can be derived from the four primary criterion scores |
| `error_analysis_fields` | Not included in the inter-rater reliability analysis |

## Private Reference Answer Fields

| Fields | Contents |
|---|---|
| `question_id` | Question ID used to link the reference answer to `questions.csv` |
| `reference_answer` | Full professor-provided or course-derived answer used internally for scoring |
| `expected_key_points` | Key concepts, steps, formulas, or outputs expected in a full-credit response; stored privately because it may reveal the answer |
| `grading_notes` | Additional internal notes for scoring decisions, such as partial-credit rules or acceptable variations |