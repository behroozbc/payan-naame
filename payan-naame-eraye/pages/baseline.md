## Baseline

To evaluate the effectiveness of the proposed approach, two baseline methods are established. These baselines serve as reference points against which the performance of the full pipeline can be measured.

<v-clicks>

- **Zero-shot Baseline** — Queries the LLM directly without any external context
- **Context-augmented Baseline** — Provides the LLM with retrieved context (simple RAG)

</v-clicks>

---

### Zero-shot Baseline

<v-clicks>

- Queries the LLM **directly** without providing any external context
- Assesses the model's **own knowledge** — how much it already knows about the topic by default
- No supplementary information is given to the model

</v-clicks>

<v-click>

**Prompt:**

```
You are a question-answering model for students.
Please provide answers that are easy for students to understand.
Use all material provided in the context.
I provide the user's status regarding some prerequisites
of the topic. If the user does not know some prerequisites,
cover them before explaining the question to the user.
Answer in an academic tone.

User query:
{query}
```

</v-click>

---

### Context-augmented Baseline

<v-clicks>

- Provides the LLM with **context retrieved** by the search pipeline
- Constitutes a simple **Retrieval-Augmented Generation (RAG)** approach
- The model is supplied only with relevant documents.

</v-clicks>

---

### Purpose of the Context-augmented Baseline

<v-clicks>

- Isolates the effect of **merely adding context** to the LLM's input
- Addresses **RQ2** — incorporates relevant source material
- Suffers from a significant limitation: the generated answer follows a **"one-size-fits-all"** approach
- Disregards the user's **prior knowledge and prerequisites**
- Consequently, it **fails to address RQ1**

</v-clicks>

<v-click>

**Prompt:**

```
You are a question-answering model for students.
Please provide answers that are easy for students to understand.
Use all material provided in the context.
I provide the user's status regarding some prerequisites
of the topic. If the user does not know some prerequisites,
cover them before explaining the question to the user.
Answer in an academic tone.

User query:
{query}

Your response should mixed of this content:
{docs_content}
```

</v-click>
