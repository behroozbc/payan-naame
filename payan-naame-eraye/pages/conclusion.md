## Conclusion

This thesis focused on the design and implementation of a personalized **Retrieval-Augmented Fine-Tuning (RAFT)** method for question answering and student response evaluation in educational environments.

<v-clicks>

- Primary objective: Develop and personalize a system tailored to each student
- Deliver customized answers based on their **individual knowledge background**
- This final chapter summarizes the work and revisits the research questions

</v-clicks>

---

### Summary of Contributions

<v-clicks>

1. **📚 A dataset of student questions** — Questions collected from students via forum requests, each answered with accurate and verified knowledge.

2. **📝 A dataset of question-answer pairs with knowledge background annotations** — Over 150 entries pairing questions with answers and student knowledge backgrounds, suitable for fine-tuning.

3. **⚙️ A complete RAFT and RAG pipeline** — Both pipelines developed and deployable on full-scale systems (e.g., ALEA platform). The RAG pipeline also works with more advanced models.

</v-clicks>

---

### Revisiting RQ1

**How can the system dynamically adapt its responses to align with a student's current knowledge level and learning progress?**

<v-click>

> The RAFT method demonstrates that the system can identify the student's level of understanding and tailor the answer based on their knowledge base. However, this does not provide a completely solid foundation for the model to fully address the student's needs.

</v-click>

---

### Revisiting RQ2

**How can course-specific content and pedagogical materials be effectively integrated to ensure domain-relevant and accurate responses?**

<v-click>

> After fine-tuning, the model exhibits a significantly better understanding of course-specific content, leading to more consistent and domain-relevant answers.

</v-click>

---

### Revisiting RQ3

**What techniques and architectural strategies can be employed to effectively reduce hallucinations in LLM-based tutoring systems?**

<v-click>

> The fine-tuning and RAFT pipeline demonstrate that the model achieves a better contextual understanding, which effectively mitigates hallucinations.

</v-click>

---

### Revisiting RQ4

**How can the system generate more accurate, context-aware, and educationally valuable answers that support meaningful learning?**

<v-click>

> The answer is visibly affirmative. Compared to the baseline, the model produces significantly more coherent and contextually grounded responses. Within the RAFT and RAG pipelines, the model demonstrates the ability to identify prerequisite concepts and explain them within the context of the given topic.

</v-click>

---

### ⚠️ Limitations

<v-clicks>

- **HPC access restriction** — Sudden and unforeseen loss of access to HPC resources ~3 weeks before submission
- All experimental results stored on HPC were **lost**
- Recreating results with limited computational power, GPU access, and model execution capabilities was exceedingly challenging
- Only the datasets were safe (stored locally)
- Question augmentation data from the pipeline was lost

</v-clicks>

<v-click>

> If this had been foreseen, the approach would have shifted to a version of RAG requiring less computational power.

</v-click>

---
layout: cover
---
## Future Work

---

### Compact Representation of FTML

<v-clicks>

- FTML is effective for rendering LaTeX on the web but contains **many HTML tags** unnecessary for LLMs
- These tags increase content size unnecessarily
- **Goal:** Develop a compact representation that reduces text volume, allowing more meaningful content within a smaller context window

</v-clicks>

---

### User Course Selection

<v-clicks>

- Users should be able to **select the relevant course** to improve retrieval accuracy
- Some courses overlap in content (e.g., AI1 and AI2 share topics)
- Course selection ensures only **course-specific content** is retrieved

</v-clicks>

---

### Application to Other Courses & Domains

<v-clicks>

- This thesis focused on a limited set of **computer science** courses
- Should be applied to **other disciplines** with broader topics to evaluate generalizability
- Particularly promising: **image-oriented courses** (e.g., medical diagrams with labeled anatomical structures)
- Multimodal RAG systems have demonstrated strong retrieval in both textual and visual spaces

</v-clicks>

---

### Prerequisite Relevance Indicators

<v-clicks>

- No mechanism currently exists to indicate the **relevance level** of prerequisites
- Some identified prerequisites bear **no meaningful relation** to the content (e.g., "word" flagged as a prerequisite)
- **Future work:** Assign a relevance score to each prerequisite — primary, secondary, or tangential
- This would enable the model to **prioritize genuinely relevant prerequisites**

</v-clicks>

---

### Validity of LLM-as-a-Judge in Education

<v-clicks>

- One aspect of this thesis used LLMs as judges for evaluation metrics
- **Open questions:**
  - How reliably can an LLM determine whether an answer is correct?
  - To what extent can it assess relevance and quality?
- Future research should investigate whether LLMs are a **reliable choice** for assessment in educational domains

</v-clicks>

---

### Larger & More Sophisticated Models

<v-clicks>

- Experiments with larger models were **not possible** due to HPC restrictions
- Future research should apply the method to models with **more parameters**
- Examine how results **scale** and whether performance improves accordingly

</v-clicks>

---

### MathHub Content Stability & Accessibility

<v-clicks>

- MathHub content undergoes **frequent changes**, posing reproducibility challenges
- **Needed:** Versioned snapshots of MathHub content
- MathHub lacks a comprehensive **Python library** for programmatic access
- Significant time was spent loading data and understanding data structures
- Future work should focus on **versioned snapshots** and **official client libraries**

</v-clicks>
