# Qualitative Case Studies

## Purpose

This qualitative analysis examines selected model responses to identify patterns that are not fully visible in the aggregate scores. The four cases cover a factual error, a correct answer with flawed reasoning, differences in how correct explanations are organized, and a case where clear presentation did not necessarily provide strong instructional support.

## Case Selection Strategy
The cases were selected purposively rather than randomly. Selection focused on responses that represented distinct patterns observed during scoring and audit: a substantive factual error, a correct final answer with flawed reasoning, differences in explanation quality among substantively correct responses, and a difference between clear presentation and instructional support. The cases are used to illustrate these patterns rather than to estimate how frequently they occur across the full dataset.
---

## Case Study 1 — Q24: Hallucinated Edge in a Directed-Graph Task

### Why This Case Was Selected
Q24 was selected as a substantive-error case because Qwen introduced a directed edge that was not present in the question. Unlike a response that was merely incomplete or overly verbose, this response changed the graph itself by adding a nonexistent B → E edge, which led to an incorrect adjacency list. The error is useful to examine because the invented edge appeared within an otherwise plausible and systematic response.

### Question Context
Q24 asked the models to construct an adjacency list for a directed graph from information supplied in the question. The task required identifying the outgoing neighbors of each vertex. Because the original question materials are pending source and permission review, the complete graph specification is not reproduced here.

### Responses Compared
Qwen and Grok were compared because both attempted to derive the adjacency list directly from the supplied edge information, but they differed on the outgoing edges from vertex B.

Qwen stated that B had two outgoing edges and produced:

`b: [c, e]`

Grok identified only the edge B → C and produced:

`B: [C]`

The remaining adjacency-list entries were consistent between the two responses.

### Key Observation
The question specified B → C but did not specify B → E. Qwen nevertheless stated that “there are two arrows originating from B” and added E as a second neighbor of B. This unsupported edge changed the graph represented by the response and made the final adjacency list incorrect.

The error was presented confidently within an otherwise systematic vertex-by-vertex explanation. The response correctly identified the outgoing edges for A, C, D, E, and F, making the invented B → E edge the specific source of the incorrect result.

### Rubric Evidence
Qwen received scores of 2 for Accuracy, Reasoning Completeness, Explanation Clarity, and Tutoring Effectiveness, resulting in an Overall Score of 2.00. The audited dataset classified the error as `hallucinated_concept`, with the subject-specific error recorded as `invented nonexistent B→E graph edge` and the severity level recorded as `Moderate`. The `overconfident_wrong_flag` was marked `yes`.

### Learning-Behavior Evidence
The response was coded as `partial` for Learning Transfer Support and Confidence Calibration, but `no` for Misconception Awareness and Self-Check Support. Although the response explained the general idea of an adjacency list and worked through the vertices individually, it did not fully verify the adjacency list against the six edges explicitly provided in the question. Such a verification step could have exposed the unsupported B → E edge.

The response was also coded as having low cognitive load. Its readability and organization therefore did not prevent the substantive factual error described above.

### Interpretation
Q24 is a useful example of how a localized factual error can be difficult to notice in an otherwise organized response. Qwen correctly handled five of the six vertices and presented its reasoning systematically, but the invented B → E edge was enough to make the final adjacency list incorrect.

For a learner, this type of error may be especially difficult to detect because the unsupported claim is embedded within reasoning that otherwise appears consistent. Evaluating the response therefore requires checking individual factual and structural claims against the information given in the problem, rather than relying on the overall plausibility of the explanation.

---

## Case Study 2 — Q28: Correct Final Answer with Incorrect Explanation

### Why This Case Was Selected
Q28 was selected because Qwen reached the correct final time complexity, Θ(n²), while making a substantive conceptual error in its explanation of the code. Unlike Q24, the error did not change the requested final result. This makes Q28 useful for examining whether final-answer correctness can hide a problem in the reasoning presented to the learner.

### Question Context
Q28 asked the models to analyze the time complexity of a Python function containing linear scans and a nested-loop operation. The key task was to determine the dominant asymptotic running time and explain the behavior of the code. Because the original question materials are pending source and permission review, the complete function is not reproduced here.

### Responses Compared
Qwen and Claude were compared because both models correctly identified the nested loop as the dominant source of the function's Θ(n²) running time, but they differed in their interpretation of what that loop does.

Qwen correctly calculated the total number of inner-loop iterations as

`0 + 1 + 2 + ... + (n - 1) = n(n - 1)/2`

and concluded that the overall time complexity is Θ(n²). However, it additionally claimed that the third loop does not perform a true reversal and instead performs an "insertion-sort-style left-shift."

Claude also derived Θ(n²), but explicitly checked the behavior of the reversal loop by tracing a small example. It showed that `[1,2,3]` becomes `[2,1,3]` and then `[3,2,1]`, correctly confirming that the loop does reverse the list.

### Key Observation
Qwen's complexity analysis was largely correct. It correctly identified both initial scans as linear, determined that the inner loop executes i times for each outer-loop index i, and derived the triangular sum that produces Θ(n²) total running time.

The error appeared in an additional interpretation of the code rather than in the calculation itself. Contrary to Qwen's claim, repeatedly moving `a[i]` to the front while shifting the preceding elements one position to the right does reverse the list.

### Rubric Evidence
Qwen received an Accuracy score of 2, a Reasoning Completeness score of 2, an Explanation Clarity score of 3, and a Tutoring Effectiveness score of 2, resulting in an Overall Score of 2.25. The audited dataset classified the error as `conceptual_error`, with the subject-specific error recorded as `incorrectly described the reversal loop`, a severity level of `Moderate`, and the `overconfident_wrong_flag` marked `yes`.

The response therefore retained credit for its correct complexity analysis and clear presentation, while the substantive misinterpretation of the program's behavior prevented full credit for accuracy, reasoning, and tutoring effectiveness.

### Learning-Behavior Evidence
Qwen was coded as `partial` for Learning Transfer Support and Confidence Calibration, `no` for Misconception Awareness and Self-Check Support, and `low` for Cognitive Load Level. The response did provide a useful transferable pattern by recognizing the triangular sum in the nested loop, but it did not detect or correct its mistaken interpretation of the reversal operation.

Claude was coded as `yes` for Learning Transfer Support, `good` for Confidence Calibration, and `low` for Cognitive Load Level. Its response additionally traced a small list example to verify that the loop actually reverses the list. Although this behavior was not classified as Self-Check Support under the project's existing annotation scheme, it provides a useful qualitative contrast in how the two responses supported their conclusions.

### Interpretation
Q28 shows a problem that would be missed if evaluation stopped at the final answer. A student asking only for the time complexity would receive the correct result, Θ(n²), but would also be told incorrectly that the loop does not reverse the list.

Claude’s response provides a useful contrast because its small-example trace checks the actual behavior of the loop rather than relying only on the asymptotic calculation. The comparison shows why the substantive claims inside an explanation need to be evaluated separately from the correctness of the final result, especially when the response is intended to help a student learn from the reasoning.

---

## Case Study 3 — Q10: Correct and Complete Answers with Different Tutoring Quality

### Why This Case Was Selected
Q10 was selected because all four models were substantively correct but received different scores for Explanation Clarity and Tutoring Effectiveness. All four received full scores for Accuracy and Reasoning Completeness, and no substantive errors were recorded. This makes Q10 useful for examining whether organization, concision, and instructional focus affect tutoring quality even when the underlying answer is correct.

### Question Context
Q10 asked the models to compare Principal Component Analysis (PCA) with Best Subset Selection, including the main goal of each method and how each procedure operates. The main distinction is that PCA creates new components through unsupervised dimensionality reduction, whereas Best Subset Selection selects among the original predictors using the response variable.

### Responses Compared
ChatGPT, Claude, and Grok were selected for detailed comparison because they represent three different score profiles despite all receiving full scores for Accuracy and Reasoning Completeness.

ChatGPT provided an extensive explanation of both methods, including their goals, procedures, interpretability, computational considerations, and appropriate use cases. However, its response was coded as less clear and less effective for tutoring because the main answer was not prioritized as directly as it could have been and the response included more detail than necessary.

Claude was similarly detailed and received the same Explanation Clarity score of 2, with some unnecessary repetition noted in the evaluation. Unlike ChatGPT, however, it retained a Tutoring Effectiveness score of 3 because the additional detail still provided useful instructional support and clearly emphasized the conceptual contrast between the two methods.

Grok gave a more direct comparison of the same core concepts. It distinguished PCA as unsupervised feature transformation from Best Subset Selection as supervised variable selection, explained the procedures in structured steps, and included relevant practical differences without the same degree of repetition. It received full scores for both Explanation Clarity and Tutoring Effectiveness.

### Key Observation
The main difference among these responses was not factual correctness or reasoning completeness, but how the correct information was organized and prioritized for the learner.

ChatGPT and Claude both provided substantial additional detail beyond the core comparison. In ChatGPT's case, this reduced the directness of the answer and made the main takeaway less immediately prominent. Claude also included some unnecessary repetition, but its explanation maintained stronger instructional framing, including explicit conceptual contrasts and a concluding takeaway.

Grok achieved a more balanced presentation: it retained the important procedural and conceptual details while keeping the central PCA-versus-subset-selection distinction prominent throughout the response. The main difference was therefore not how much information each model included, but whether the extra information helped make the comparison easier to follow. Grok kept the central distinction visible throughout the response, while ChatGPT and Claude included more material around it.

### Rubric Evidence
All four models received Accuracy = 3 and Reasoning Completeness = 3, and no substantive errors were recorded for any Q10 response.

The remaining scores differentiated the responses:

- ChatGPT: Accuracy 3, Reasoning Completeness 3, Explanation Clarity 2, Tutoring Effectiveness 2; Overall Score = 2.50.
- Claude: Accuracy 3, Reasoning Completeness 3, Explanation Clarity 2, Tutoring Effectiveness 3; Overall Score = 2.75.
- Grok: Accuracy 3, Reasoning Completeness 3, Explanation Clarity 3, Tutoring Effectiveness 3; Overall Score = 3.00.
- Qwen also received 3 across all four criteria, with an Overall Score of 3.00.

The evaluation notes identified ChatGPT as more verbose than necessary and as not presenting the final answer as clearly as it could have. Claude was noted to contain some unnecessary repetition, while Grok was characterized as simple and clear. These differences occurred despite agreement on the substantive content of the answer.

### Learning-Behavior Evidence
All four responses were coded as providing Learning Transfer Support and as showing good Confidence Calibration. The clearest learning-behavior difference was Cognitive Load Level: ChatGPT and Claude were coded as `medium`, whereas Grok and Qwen were coded as `low`.

This pattern is consistent with the qualitative differences in presentation. The lower cognitive-load responses retained the core conceptual and procedural distinctions without requiring the learner to process as much additional or repetitive material. This does not mean that shorter answers are always better. In Q10, the difference was whether the additional detail helped the learner focus on the main comparison.

### Interpretation
Q10 shows why correctness and completeness alone do not fully describe the quality of a study-assistant response. All four models covered the required statistical concepts correctly, but they differed in how easily a learner could identify the main comparison.

It also shows why Explanation Clarity and Tutoring Effectiveness were scored separately. ChatGPT and Claude both received Clarity = 2, but Claude retained Tutoring Effectiveness = 3 because its additional detail still supported the learner despite some repetition. In this case, the strongest responses were not necessarily the shortest or longest; they were the ones that kept the central distinction easy to identify while still providing enough explanation.

---

## Case Study 4 — Q29: Different Problems in Otherwise Strong Responses

### Why This Case Was Selected

Q29 was originally selected because ChatGPT answered the question correctly and clearly but gave less explanation than the other models. During the final review, I also found a small conceptual error in Qwen's response. Qwen selected the correct operations but incorrectly stated that adding a tail pointer would make deleting the last node O(1). This makes Q29 useful for comparing two different weaknesses in otherwise strong responses: too little explanation and an incorrect extra explanation.

### Question Context

Q29 asked which operations are inefficient for a singly linked list. Answering the question requires identifying operations that require traversal of the list and distinguishing them from operations that can be performed directly at the head. Beyond selecting the correct operations, an instructional response can also explain how the structure of a singly linked list produces these time-complexity differences.

### Responses Compared

ChatGPT and Grok were selected for detailed comparison because both correctly identified the relevant operations but differed in the amount of supporting explanation they provided.

ChatGPT directly identified finding the middle, accessing the last element, searching for an element, and deleting the last element as Θ(n) operations. It also distinguished operations at the head as Θ(1). The response was concise, clearly organized, and substantively correct. However, it provided limited explanation of why the listed operations require linear time in a singly linked list.

Grok provided the same core conclusions while giving additional structural explanations. For example, it explained that reaching the middle or last element requires traversal from the head and that deleting the last element requires locating the second-to-last node because a singly linked list does not provide a direct reference to the previous node. These explanations connected the complexity classifications to the underlying properties of the data structure.

### Key Observation

The central difference between the two responses was not correctness or readability, but instructional support. ChatGPT clearly communicated which operations have Θ(n) complexity, making the answer easy to follow. Grok additionally explained why those complexities arise from the structure of a singly linked list.

The difference was not simply that Grok wrote more. Its explanation linked the complexity results to specific properties of a singly linked list, including sequential traversal and the lack of backward links. This gives the learner a reason for the answer that can also be applied to similar questions.

### Rubric Evidence

ChatGPT received Accuracy = 3, Reasoning Completeness = 3, Explanation Clarity = 3, and Tutoring Effectiveness = 2. Its Overall Score was therefore 2.75. The evaluation note described the response as providing the selected answer but lacking basic supporting explanation.

Claude and Grok received full scores across all four criteria. Qwen selected the correct operations and explained the main traversal costs clearly, but its final note incorrectly stated that adding a tail pointer would make deleting the last node O(1). Because a singly linked list still has to find the predecessor of the last node, Qwen received 2 for Accuracy and Tutoring Effectiveness, 3 for Reasoning Completeness and Explanation Clarity, and an Overall Score of 2.50.

ChatGPT’s lower Tutoring Effectiveness score occurred without a reduction in Accuracy, Reasoning Completeness, or Explanation Clarity. The response was correct and clearly presented, but provided less instructional support than the comparison responses.

### Interpretation

Q29 shows two different ways a response can fall short as a study aid. ChatGPT gave a correct and clear answer but did not explain the traversal costs in much depth. Qwen gave more explanation, but its extra comment about deleting the last node with a tail pointer introduced an incorrect concept. This shows why tutoring quality depends not only on how much explanation a response gives, but also on whether that explanation remains accurate.

For a learner, that missing step matters. Knowing that an operation is Θ(n) answers the immediate question, but connecting that result to traversal and the structure of a singly linked list makes the reasoning easier to reuse on future problems. This difference explains why the response could be clear while still receiving a lower Tutoring Effectiveness score.

---

## Cross-Case Synthesis

Across the four cases, the models showed several kinds of differences that are difficult to see from Overall Score alone.

Q24 and Q28 show two different problems with correctness. In Q24, Qwen added a graph connection that was not given in the question and produced an incorrect adjacency list. In Q28, the final Θ(n²) result was correct, but part of the explanation of the code’s behavior was not. Together, these two cases show why checking only the final answer can miss problems in the reasoning given to a student.

Q10 mainly shows differences in how the models organized and prioritized correct explanations. Q29 shows two other issues: ChatGPT gave a correct answer with limited explanation, while Qwen gave more explanation but included an incorrect claim about deleting the last node with a tail pointer. Together, these cases show that a response can be less useful for learning either because it does not explain enough or because an additional explanation introduces a mistake.

Overall, the four cases help explain patterns that are compressed into the numerical scores. Accuracy captures an important part of response quality, but it does not show whether the explanation contains an unsupported claim, whether the intermediate reasoning is reliable, or whether the response gives the learner enough support to understand and reuse the idea. The case studies are therefore used alongside the aggregate results rather than as a replacement for them.
