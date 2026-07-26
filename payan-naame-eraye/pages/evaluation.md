## Evaluation

This chapter evaluates the Tripartite RAFT pipeline and assesses whether the proposed approach addresses the research questions identified earlier. The evaluation setup, metrics, and results are presented for both the retrieval component and the response generation component.


<v-clicks>

- **Baseline Evaluation** — LLM performance without RAG
- **LLM as Judge** — Automated evaluation using a larger LLM
- **Human as Judge** — TA review of generated answers
- **Embedding Models** — Impact of embedding choice on retrieval

</v-clicks>


---
src: ./pages/baseline.md
---

## Baseline Evaluation

Before examining the results of the Tripartite RAFT pipeline, it is essential to establish a baseline by evaluating the performance of LLMs in the absence of retrieval-augmented generation. This preliminary assessment highlights the inherent limitations of LLMs when operating without external context, thereby motivating the need for the proposed approach.

---

### Illustrative Example — Zero-shot Baseline

Question: *"What is an AI Agent?"* answered by **Google Gemma 4 E4B** without any context.

<v-clicks>

- ❌ **Incorrect definition**: The AI agent definition is much simpler; the definition provided is for a goal-based agent.
- ❌ **Use of unacademic words**
- ❌ **Prerequisites are not valid**

</v-clicks>

<v-click>

> These issues collectively demonstrate that LLMs, when operating without domain-specific contextual grounding, are prone to generating responses that are inaccurate, irrelevant, or misleading. This underscores the necessity of a retrieval-augmented framework.

</v-click>

---

### Illustrative Example — Context-augmented Baseline

Same question, same model, but with **retrieved context** provided.

<v-click>

> *"Based on the provided materials, here is an explanation of what an AI Agent is: In Artificial Intelligence (AI), an agent is a thing that can perceive its environment and then act upon that environment..."*

</v-click>

<v-clicks>

- ❌ **Incorrect and incomplete definition**: Does not define what an agent is or provide the definition in mathematical notation.
- ❌ **Use of unacademic words**
- ❌ **Prerequisites are not valid**

</v-clicks>

<v-click>

Adding context helps, but the model still fails to produce accurate, academically rigorous answers.

</v-click>

---

## LLM as Judge

Using an LLM as a judge is an effective approach for evaluating generated answers and providing feedback on their quality.

<v-clicks>

- **Judge LLM**: `deepseek-ai/DeepSeek-V4-Flash` (larger parameter count model)
- Also introduces a **RAG pipeline** to compare against RAFT — isolating the effect of fine-tuning
- Raises concerns: LLMs are **not entirely trustworthy** and do not provide **explainable reasoning**

</v-clicks>

---

### Three Evaluation Metrics

<v-clicks>

**Contextual Relevancy** — Evaluates the retriever component by measuring the overall relevance of retrieved context with respect to the input query.

**Faithfulness** — Measures whether the generated output factually aligns with the contents of the retrieved context (i.e., no hallucination).

**Answer Relevancy** — Evaluates whether the generated answer directly addresses the user's question, avoiding extraneous or off-topic content.

</v-clicks>

<v-click>

> All three metrics are implemented as **self-explaining LLM-Evals** — in addition to a numerical score, the LLM judge generates a natural language explanation justifying its assessment.

</v-click>

---

### LLM-as-Judge Results

| Condition | Contextual Relevancy | Answer Relevancy | Faithfulness |
|-----------|:-------------------:|:----------------:|:------------:|
| **Zero-shot Baseline** | 7% | 38% | 29% |
| **Context-augmented Baseline** | 15% | 55% | 62% |
| **RAG** | 16% | 44% | 52% |
| **RAFT** | 10% | 45% | 52% |

<v-click>

**Key observations:**

- Context-augmented baseline shows **marked improvement** in answer relevancy (38% → 55%) and faithfulness (29% → 62%)
- RAG and RAFT scores are **comparable**, but RAFT answers are **more coherent and consistent**

</v-click>

---

### Why Answers Fail the Relevancy Check

<v-clicks>

- The model tends to **default to summarizing the input** rather than directly addressing the question
- Upon reviewing chain-of-thought reasoning: the model **initially identifies** the need to answer directly
- But as reasoning progresses deeper — particularly when listing prerequisites — the model **loses sight of the original question**

</v-clicks>



<v-click>

> Example: When asked *"What is an AI agent?"*, the model shifts focus to producing a comprehensive summary of prerequisites instead of a direct answer.

</v-click>

---

### Additional Observation

<v-click>

The same question was posed to the fine-tuned model **without any prior context or instructions** regarding academic tone.

</v-click>

<v-click>

**Result:** The answers exhibited a **markedly improved academic tone** and overall quality compared to those generated with context and prerequisite information.

</v-click>

<v-click>

> This suggests that fine-tuning helps the model produce better-structured and more coherent responses. However, this alone does not fulfill the thesis objective, as the primary goal is to enable customization through a runtime-adaptable mechanism rather than relying solely on fine-tuning.

</v-click>

---

### RAFT vs RAG: Coherence

<v-clicks>

- ✅ **RAFT**: Generated answers are **more coherent** and exhibit **less variation** during generation
- ❌ **RAG**: Sometimes produces answers that are **entirely incomplete** or **drastically different** from one attempt to another
- However, relying solely on a fine-tuned model is **not sufficient** — given the degree of customization required, a **runtime-adaptable mechanism** is necessary
- Another factor: the model is **relatively small** with a **very limited context window** — when additional content is supplied, the increased volume causes confusion

</v-clicks>

---

## Human as Judge

A teaching assistant for the subject courses reviewed a subset of generated answers, checking that:

<v-clicks>

- ✅ Answers are **valid**
- ✅ All **concepts and information** are explained
- ✅ **No hallucinations** present
- Answers were compared against actual reference answers

</v-clicks>

---

### Human as Judge — Key Findings

<v-clicks>

- Many answers merely **summarized the prerequisites** and avoided addressing the actual question
- However, when the model **did answer** the question, the response was **quite good** — free of hallucinations or off-topic explanations
- **Notable observation**: When the user demonstrated **expert-level knowledge** of prerequisites, the model tended to avoid answering the question directly — instead stating the user already understood everything or attempting to end the conversation prematurely

</v-clicks>

---

### Human as Judge — Example 1 (Good)

<v-click>

> User asked: *"How can I check if my logic formula is complete?"* (basic-level knowledge of prerequisites)

</v-click>

<v-click>

**Model response:** Correctly identified that completeness is a **property of a logical system**, not of a single formula, corrected the user's misconception, and explained relevant prerequisites as defined for the user.

</v-click>

<v-click>

✅ **Correct, well-reasoned response**

</v-click>

---

### Human as Judge — Example 2 (Poor)

<v-click>

> User asked: *"Briefly explain the difference between fully and partially observable environments. Give an example for the latter."*

</v-click>

<v-click>

**Model response:** Only summarized the basic prerequisites added to the prompt, neglecting to address the actual question.

</v-click>

<v-click>

In the **chain-of-thought reasoning**, the model recalled the question but then proceeded to elaborate further on the prerequisites, ultimately failing to answer.

</v-click>

<v-click>

❌ **Failed to address the actual query**

</v-click>

---

### Human as Judge — Consistency

<v-click>

One point mentioned in the LLM-as-a-Judge section is **better demonstrated** in this experiment:

</v-click>

<v-clicks>

- ✅ **RAFT method**: Model answers are **significantly more consistent**
- ❌ **RAG method**: Model sometimes only responds with an **intent to use a tool**, skips answering altogether, or attempts to call a **web search** despite no such tools being provided

</v-clicks>

---

## Embedding Models

Embedding models play a critical role in RAG and RAFT pipelines, as they directly influence the quality of retrieved documents and, consequently, the overall system performance.

<v-clicks>

- Multiple embedding models were evaluated to determine which achieves the **best retrieval quality**
- Different embedding **dimensions** were investigated for their effect on retrieval score

</v-clicks>

---

### Embedding Models — Key Finding

<v-clicks>

- Embedding models with dimensions **exceeding 1000** tend to produce **degraded retrieval performance**
- They retrieve a larger number of **irrelevant or semantically distant documents**
- Higher-dimensional embeddings **do not necessarily** lead to better retrieval — they may introduce **noise** into the similarity search process

</v-clicks>

<v-click>

> ⚠️ **Note:** An unexpected issue with the **HPC system** during the experimental phase resulted in the loss of all computed results, rendering this analysis incomplete in the final report.

</v-click>

---

## Summary of Evaluation Findings

| Aspect | Finding |
|--------|---------|
| **Baseline** | LLMs without context produce inaccurate, irrelevant, or misleading answers |
| **Context-augmented** | Improves faithfulness and relevancy, but still lacks precision |
| **LLM as Judge** | RAFT answers are more coherent and consistent than RAG |
| **Human as Judge** | RAFT produces consistent, hallucination-free answers when it answers directly |
| **Key Challenge** | Model tends to summarize prerequisites instead of answering the question |

<v-click>

> The evaluation demonstrates that the Tripartite RAFT pipeline improves consistency and reduces hallucinations, but further work is needed to ensure the model consistently addresses the user's actual question rather than defaulting to prerequisite summarization.

</v-click>
