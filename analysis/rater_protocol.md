# Second-Rater Evaluation Protocol

## Purpose

A second-rater evaluation was conducted to assess the consistency of the primary scoring process. The second-rater ratings were used for inter-rater reliability analysis and did not replace the primary ratings used in the main analysis.

## Sample Selection

The second-rater subset consisted of 32 model responses from eight complete question blocks: Q4, Q6, Q10, Q14, Q17, Q21, Q27, and Q29.

Each selected question included responses from all four evaluated models, resulting in 8 questions × 4 models = 32 responses, representing 26.7% of the full 120-response dataset.

The subset was purposively selected rather than randomly sampled. Complete question blocks were retained so that all four model responses to each selected question were included.

## Materials Provided to the Second Rater

For each selected response, the second rater was provided with:

- the question ID and question text;
- the reference answer and expected answer information;
- the original model response;
- the scoring rubric and criterion definitions; and
- a worksheet for recording ratings and observations.

Model names were visible in the rating materials. Therefore, the second-rater evaluation was not model-blind.

The primary rater's scores were not provided to the second rater during the independent rating process.

## Rating Procedure

The second rater independently evaluated each response using the same 0–3 scoring rubric used in the primary evaluation.

Four criteria were scored:

- `accuracy_score`
- `reasoning_completeness_score`
- `explanation_clarity_score`
- `tutoring_effectiveness_score`

The second rater also recorded the learning-behavior observations included in the evaluation framework.

`overall_score` was not independently assigned by the second rater and was instead derived from the four criterion scores.

Error-analysis fields were not used in the inter-rater reliability analysis.

## Inter-Rater Reliability Analysis

Second-rater records were matched with the primary evaluation using `question_id` and `model_name`.

Agreement was evaluated using:

- exact agreement rates;
- absolute score differences;
- agreement in derived overall scores; and
- quadratic-weighted Cohen's kappa where score variation permitted its calculation.

For criteria with no rating variance, weighted kappa was undefined and was not interpreted as evidence of poor reliability.

## Limitations

The second-rater subset was purposively selected rather than randomly sampled. Therefore, the reliability results describe agreement within the selected subset and should not be interpreted as a population-level estimate of agreement across all 120 responses.

In addition, model identities were visible during the rating process, so potential model-related expectation bias cannot be ruled out.

Q24 and Q28 were not included because they had already been identified as failure cases during the earlier audit and were reviewed separately before the second-rater subset was finalized. Q29 was included in the subset and rated by the second rater before the later final audit identified an additional issue in the Qwen response. Q29 was retained in the reliability analysis rather than removing a question after the second-rater ratings had already been collected. This is another reason why the reliability results should be interpreted only as a check within the purposively selected subset.

## Rater Background and Preparation

The second rater was an incoming undergraduate student at University College London (UCL) intending to major in media.

Before the independent rating process, the second rater received an oral explanation of the evaluation procedure and reviewed the scoring criteria and annotation guidelines. These materials included the 0–3 scoring rubric for the four main evaluation criteria as well as the definitions of the learning-behavior tags used in the project.

This preparation gave the second rater a chance to understand the scoring criteria and annotation fields before starting the ratings.