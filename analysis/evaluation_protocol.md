# Evaluation Protocol

This document records the evaluation procedure used in the project, including the prompt, response collection process, scoring rubric, error analysis, and learning-behavior tags.

## Prompt Protocol

I tested a more structured prompt during the pilot study:

> You are a Senior Academic Tutor at UC Davis, specializing in introductory Statistics, Mathematics, and Python programming. Your task is to help a first-year college freshman understand the following question.
>
> When I provide the question, please structure your response exactly as follows:
>
> 1. Direct Answer: Give the final correct answer or output clearly in 1-2 sentences.
> 2. Step-by-Step Solution: Provide a detailed, logical, and chronological breakdown of how to solve it. Do not skip intermediate steps.
> 3. Concept Explanation (Freshman-friendly): Explain the core logic or formulas used in plain, intuitive English. Imagine you are explaining it to someone with zero prior background. Avoid overly dense academic jargon without defining it first.
> 4. Confidence & Uncertainty (Optional): If the question is ambiguous or lacks enough information, explicitly point out any assumptions you are making or potential alternative interpretations.

During the pilot, this prompt produced very similar answers across the models, and most responses received similarly high scores. I felt that the fixed structure was guiding the models too heavily and made it harder to compare how they would naturally respond to a student.

I therefore switched to a shorter prompt for the full evaluation:

> You are a teaching assistant for lower-division college courses in Statistics, Mathematics, and Python programming. Please help me understand and solve the following question. Please explain your reasoning clearly enough for a first-year college student.
>
> Question:
> [question text]

## Response Collection

The same 30 questions were given to each of the four models, giving 120 responses in total.

I used the revised prompt for all questions in the main evaluation. The questions were submitted in the same order for each model, and I did not provide corrections or additional hints between questions.

For each model, the 30 questions were collected in one continuous conversation. This meant that earlier messages remained in the conversation history. Most questions were written to work on their own, but Q2 depended on Q1 and Q19 depended on Q18, so those pairs intentionally used the preceding question as context.

Model identities were visible to the primary rater during scoring. The primary evaluation was therefore not blinded, and potential model-related expectation bias cannot be ruled out.

## Scoring Rubric

Each response received a score from 0 to 3 for four criteria: Accuracy, Reasoning Completeness, Explanation Clarity, and Tutoring Effectiveness.

### Accuracy

Accuracy evaluates the substantive correctness of the response, with primary emphasis on whether the main answer, conclusion, and required result are correct. Errors in supporting or additional statements may lower the score when they materially affect the correctness of the response.

Accordingly, an Accuracy score of 3 indicates that the response is substantively correct for the task; it should not be interpreted as a guarantee that every auxiliary statement in the response is error-free.

**0 — Unacceptable**

The final answer, numerical value, conclusion, code output, or mathematical result is incorrect. The response shows a major misunderstanding of the problem or reaches the wrong conclusion.

**1 — Poor**

The answer contains an important error, such as an incorrect final value, sign, code behavior, or conclusion. Some parts may still be correct, but the answer is not reliable overall.

**2 — Satisfactory**

The main answer is correct or mostly correct, but there is a minor problem with the calculation, notation, wording, or interpretation that does not substantially change the result.

**3 — Excellent**

The answer and supporting work are correct and consistent with the reference answer.

### Reasoning Completeness

**0 — Unacceptable**

There is little or no useful reasoning. Important formulas, calculations, logical steps, or code-tracing steps are missing.

**1 — Poor**

Some reasoning is provided, but major steps are missing. A student would need to fill in important gaps to understand how the answer was reached.

**2 — Satisfactory**

Most important steps are included and the reasoning is generally logical, but some transitions, assumptions, formulas, or intermediate steps are not fully explained.

**3 — Excellent**

The reasoning gives a complete path from the question to the final answer, including the important formulas, assumptions, calculations, or logical steps needed for the problem.

### Explanation Clarity

**0 — Unacceptable**

The explanation is difficult to follow or poorly organized. The connection between the reasoning, formulas, code, and final answer is unclear.

**1 — Poor**

The explanation has some structure, but parts of it are confusing, inconsistent, unnecessarily long, or difficult to follow.

**2 — Satisfactory**

The explanation is generally clear and readable, although some parts may be abrupt, repetitive, or more complicated than needed.

**3 — Excellent**

The explanation is clear, organized, and easy to follow. Formatting, formulas, code, and written explanation are used effectively without adding unnecessary detail.

### Tutoring Effectiveness

**0 — Unacceptable**

The response provides little help beyond giving an answer. Important ideas may be left unexplained, or the response may not help a first-year student understand how the solution works.

**1 — Poor**

The response provides some teaching value, but the explanation is mostly mechanical or does not give enough support for a first-year student to understand the main idea.

**2 — Satisfactory**

The response is useful for a first-year student and explains most of the important ideas in accessible language, although some concepts could use more explanation or support.

**3 — Excellent**

The response works well as a study aid. It explains the main ideas clearly, helps the student understand the method, and gives enough support for the student to apply the same idea again. When relevant, it may also point out common mistakes or ways to check the answer.

## Overall Score

The Overall Score was calculated as the average of the four criterion scores:

`Overall Score = (Accuracy + Reasoning Completeness + Explanation Clarity + Tutoring Effectiveness) / 4`

The four criteria were weighted equally when calculating the Overall Score. This weighting was chosen as a simple summary of performance across the four evaluation dimensions rather than as an empirically validated weighting scheme. Criterion-level results are therefore also reported separately.

The error-analysis fields and learning-behavior tags were recorded separately and did not affect the Overall Score.

## Error Analysis

I used several additional fields to record substantive response errors and related scoring context:

- `error_type`: general category of the error
- `subject_specific_error`: a more specific description related to the subject
- `severity_level`: Minor / Moderate / Severe / None
- `overconfident_wrong_flag`: Yes / No
- `error_notes`: a short note describing the problem

The following error categories were used in the dataset:

- `calculation_error`
- `conceptual_error`
- `reasoning_gap`
- `missing_key_step`
- `unclear_explanation`
- `overconfident_wrong_answer`
- `hallucinated_concept`
- `fails_to_identify_ambiguity`
- `weak_tutoring`

### Severity Levels

**Minor**

A small problem that does not change the main answer or method. The response is still mostly reliable and is unlikely to seriously mislead a student.

**Moderate**

A more noticeable problem that affects part of the reasoning or explanation without making the entire solution invalid. Examples include an important missing step, an incomplete explanation, or a partially incorrect interpretation.

**Severe**

A major problem that could seriously mislead a student. Examples include a major conceptual error, a hallucinated formula or theorem, incorrect code logic, or a confidently stated wrong conclusion.

**None**

No meaningful error was identified. Minor stylistic or formatting issues were not counted as substantive errors if they did not affect the student's understanding.

## Learning-Behavior Tags

In addition to the main scores, I recorded five learning-behavior tags. I used these to look at tutoring-related features that were not fully represented by the four numerical criteria.

The learning-behavior tags were manually assigned as descriptive annotations based on the observed response characteristics. Numerical values derived from these tags were used only for descriptive visualization and should not be interpreted as validated educational or psychometric measurements.

### `learning_transfer_support`

Whether the response helps the student apply the same method to a similar problem.

Values: Yes / Partial / No

### `misconception_awareness`

Whether the response identifies common mistakes, traps, or possible misunderstandings.

Values: Yes / Partial / No

### `self_check_support`

Whether the response gives the student a way to check the answer, reasoning, or code.

Values: Yes / Partial / No

### `confidence_calibration`

How well the response handles assumptions, uncertainty, or ambiguity when they are relevant.

Values: Good / Partial / Poor

### `cognitive_load_level`

How difficult the explanation is for a first-year student to process.

Values: Low / Medium / High

These tags were used for descriptive analysis only and were not included in the Overall Score.