# Evaluating AI Models as Study Assistants

## Project Overview
This project evaluates four AI models -- ChatGPT, Claude, Grok, and Qwen -- as study assistants for lower-division college courses in Statistics, Mathematics, and Python / Introductory Computer Science.

The project focuses not only on whether a model gives the correct final answer, but also on whether its explanation is complete, clear, and helpful for a lower-division college student.

Research Version 1.0 extends the earlier MVP evaluation by adding inferential statistical analysis, inter-rater reliability analysis, and qualitative case studies of selected model responses.

The benchmark contains 30 questions:

- 10 Statistics questions
- 10 Mathematics questions
- 10 Python / Introductory Computer Science questions

Each model answered all 30 questions, producing 120 model responses in total.

All 30 questions were administered sequentially to each model within a single conversation, with context retained between questions. Most questions were self-contained; however, Q2 and Q19 relied on information provided in the immediately preceding questions, Q1 and Q18, respectively. These pairs are therefore treated as linked question sequences in the documented collection procedure.

## Research Question
How do mainstream LLM-based study assistants differ in accuracy, explanation quality, and tutoring behavior when answering introductory Statistics, Mathematics, and Python / Introductory Computer Science questions?

The project also examines:

- differences across evaluation criteria;
- variation across subjects;
- consistency of model performance across questions;
- learning-support behaviors beyond final-answer correctness.

## Models Evaluated
| Model | Version / Setting | Access Method |
|---|---|---|
| ChatGPT | ChatGPT 5.6 Thinking | App |
| Claude | Claude Opus 4.8 High | Web |
| Grok | SuperGrok Expert Mode | App |
| Qwen | Qwen 3.7-Max | Web |

Model names and versions reflect the interfaces used during data collection.

## Dataset
The local project dataset contains:

- `data/questions.csv`: question text and question-level metadata;
- `data/scored_responses.csv`: model responses, scores, error fields, and learning behavior tags;
- `data/second_rater_question_bank.xlsx`: independent ratings for a purposively selected subset of 32 responses used for inter-rater reliability analysis.

Two public-safe analysis files are also generated for reproducibility:

- `data/public_analysis_scores.csv`: question-level metadata and evaluation scores used for the main quantitative analysis;
- `data/public_second_rater_scores.csv`: paired primary- and second-rater scores used for the inter-rater reliability analysis.

Question materials are currently marked as `pending_source_review` and require source/licensing review before any public release.

The `reference_answers_private` file contains course-derived grading material and is designated as private evaluation material. It is not intended for public release.

The final audited dataset contains:

- 30 unique questions;
- 120 valid model responses;
- 30 responses per model;
- 4 responses per question;
- no duplicate question-model pairs;
- no missing main score values.

### Data Availability

The full evaluation dataset is not included in the public repository because the source questions are currently pending a separate review for public release. The local research dataset contains the 30 evaluation questions, 120 scored model responses, and the 32-response second-rater subset used in the reliability analysis. Public-safe score files are provided separately for reproducing the quantitative analyses without releasing the full question text or raw model responses.

The public repository therefore focuses on the evaluation methodology, analysis code, aggregate results, figures, and project documentation. The dataset may be released separately if the source materials are later cleared for public distribution.

## Evaluation Framework
Each response was evaluated on a 0–3 scale using four criteria:

1. **Accuracy / Substantive Correctness**
2. **Reasoning Completeness**
3. **Explanation Clarity**
4. **Tutoring Effectiveness**

The Overall Score was calculated as:

```text
Overall Score =
(Accuracy + Reasoning Completeness + Explanation Clarity + Tutoring Effectiveness) / 4
```

The complete scoring rubric, prompt protocol, response-collection procedure, error framework, and learning-behavior tag definitions are documented in `analysis/evaluation_protocol.md`.

The dataset also includes:

- error-analysis fields;
- learning-transfer support;
- misconception awareness;
- self-check support;
- confidence calibration;
- cognitive-load level.

## Analysis and Visualizations
The Jupyter Notebook performs:

- dataset validation;
- descriptive model-performance analysis;
- criterion-level comparison;
- score-distribution analysis;
- subject-level comparison;
- learning-behavior analysis;
- 95% confidence interval estimation;
- Friedman tests for paired model comparisons;
- Holm correction for multiple testing;
- post-hoc paired Wilcoxon signed-rank tests where appropriate;
- inter-rater reliability analysis using exact agreement, average absolute difference, and weighted Cohen's kappa;
- disagreement review and reliability interpretation.

Selected response-level failure modes and instructional differences are examined separately in `analysis/qualitative_case_studies.md`.

The five core visualizations are:

1. Average Overall Score by Model
2. Average Evaluation Scores by Model
3. Distribution of Overall Scores by Model
4. Average Overall Score by Subject and Model
5. Average Learning-Behavior Scores by Model

## Key Findings
- Overall model performance was high and closely clustered. Grok achieved the highest descriptive mean Overall Score (2.950), followed by Claude (2.942), Qwen (2.900), and ChatGPT (2.858).

- The overall Friedman test did not detect a statistically significant difference in Overall Score among the four models, χ²(3) = 5.721, p = 0.126, with a small effect size (Kendall's W = 0.064). The 95% confidence intervals for the four model means also overlapped substantially.

- Accuracy showed a strong ceiling effect: 117 of 120 responses received the maximum Accuracy score. Here, Accuracy refers to substantive correctness of the response for the task; a maximum score does not necessarily imply that every auxiliary statement in the response was error-free.

- At the criterion level, Tutoring Effectiveness was the only criterion that remained statistically significant after Holm correction, χ²(3) = 13.602, adjusted p = 0.014, Kendall's W = 0.151. Accuracy had a raw p-value below 0.05 but was not statistically significant after Holm correction (adjusted p = 0.088).

- Post-hoc paired Wilcoxon signed-rank tests showed that only the ChatGPT–Grok comparison in Tutoring Effectiveness remained statistically significant after Holm correction (adjusted p = 0.045). Grok had the higher mean Tutoring Effectiveness score (2.900 vs. 2.567). This result should be treated as limited benchmark-specific evidence rather than as a robust general ranking of the two models.

- Subject-level patterns varied across Statistics, Mathematics, and Python / Introductory Computer Science, but these comparisons were treated as descriptive because each subject contained only 10 questions.

- Qualitative case studies identified response-level differences that aggregate scores did not fully capture, including hallucinated information, incorrect explanations accompanying otherwise correct answers, and differences in instructional depth.

- Inter-rater analysis on 32 independently rated responses showed 96.9% exact agreement for Accuracy, 100% for Reasoning Completeness, 90.6% for Explanation Clarity, and 87.5% for Tutoring Effectiveness. Weighted Cohen's kappa was 0.000 for Accuracy, 0.520 for Explanation Clarity, and 0.273 for Tutoring Effectiveness. Kappa could not be estimated for Reasoning Completeness because the ratings showed no variation in the selected subset.

## Limitations
This project uses a small benchmark of 30 introductory questions, with only 10 questions per subject.

All 30 questions for each model were administered sequentially within a single conversation with conversational context retained between questions. Although most questions were designed to be self-contained, this procedure may have introduced context carryover across responses and therefore limits the independence of individual observations. Future evaluations could use separate conversations for independent question blocks to reduce this potential source of contamination.

Most of the full dataset was evaluated by one primary rater, and model identities were visible during the primary scoring process. The primary evaluation was therefore not blinded, so potential model-related expectation bias cannot be ruled out. A second rater independently evaluated a purposively selected subset of 32 responses (26.7% of the dataset). The subset was not randomly sampled, and model identities were also visible during the second-rater rating process. The reliability results should therefore be interpreted as a check within the selected subset rather than as a complete independent evaluation of all 120 responses.

The coarse 0–3 scoring scale and strong ceiling effects produced many tied scores, limiting the sensitivity and statistical power of some comparisons. Restricted score variation also affected the inter-rater reliability statistics: weighted Cohen's kappa could not be estimated for Reasoning Completeness, while Accuracy produced a kappa of 0.000 despite 96.9% exact agreement.

The dataset shows a strong Accuracy ceiling effect, with 117 of 120 responses receiving the maximum Accuracy score.

The benchmark covers a limited range of introductory topics and may not generalize to advanced courses, long-form assignments, or other academic disciplines.

The learning-behavior tags were manually assigned and converted into numerical values for descriptive visualization. These values should not be interpreted as validated educational measurements.

Model versions and consumer-facing interfaces may also change over time, which can affect reproducibility.


## Running the Analysis

The final analysis was tested with Python 3.14.2. Exact package versions used for the final reproducibility check are recorded in `requirements.txt`.

Install the required Python packages:

```bash
pip install -r requirements.txt
```

Then open `notebook/ai_tutor_analysis.ipynb` and run all cells from top to bottom.

The notebook has been validated to run successfully from a restarted kernel when executed from top to bottom with the Research Version 1.0 repository structure preserved.

The notebook uses relative file paths, so the repository structure should be preserved when running the analysis.


## Repository Structure

```text
ai-study-assistant-evaluation/
├── analysis/
│   ├── evaluation_protocol.md
│   ├── qualitative_case_studies.md
│   └── rater_protocol.md
├── audit/
│   ├── audit_log.xlsx
│   ├── audit_report.docx
│   └── version_inventory.md
├── data/
│   ├── public_analysis_scores.csv
│   └── public_second_rater_scores.csv
├── figures/
│   ├── average_overall_score_by_model.png
│   ├── criterion_scores_by_model.png
│   ├── learning_behavior_heatmap.png
│   ├── overall_score_boxplot.png
│   └── subject_model_comparison.png
├── notebook/
│   └── ai_tutor_analysis.ipynb
├── .gitignore
├── coding_log.md
├── data_dictionary.md
├── README.md
└── requirements.txt
```
