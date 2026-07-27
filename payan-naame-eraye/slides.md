---
theme: academic
title: Master thesis
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: true
layout: cover
class: text-white
# duration of the presentation
duration: 20min
coverBackgroundUrl: /intro.png
coverAuthor: [behrooz bozorgchamy]
---

# TripartiteRAFT 
---
layout: two-cols-header
---

# TripartiteRAFT
<v-click>

## Problem Statement & Motivation
Students often ask ChatGPT or other language models questions.
</v-click>

::left::
<v-click>

### 🎓 Challenge in Using Language Models for Education
</v-click>
<v-click>
These models do not know:
</v-click>
<v-clicks >

- The student’s background knowledge.
- The prerequisite topics they should already understand.
- What the instructor has covered in class.
</v-clicks>
::right::
<v-click at=1>

![qa](/front-view-female-student-writing-notes.png)
</v-click>
---
layout: two-cols-header
---

### ⚠️ Resulting Issues
::left::
<v-clicks >


- Answers may include inaccuracies.
- Some explanations may be irrelevant or missing.
- Answers may ignore details the instructor has already explained.
- Responses can sometimes contain hallucinations.
</v-clicks>
::right::
<v-click>

![dontfindanswer](/front-view-female-student-with-many-files.png)
</v-click>
---
hide: true
---
### 🎯 Thesis Goal

My thesis aims to address and solve these limitations by designing a system that:

<v-clicks>

- Adapts responses to the student’s knowledge level.
- Incorporates course‑specific content.
- Reduces hallucinations.
- Provides more accurate, context‑aware answers.
</v-clicks>

---

### 📋 Research Questions

<v-clicks>

- **RQ1**: How can the system dynamically adapt its responses to align with a student's current knowledge level and learning progress?
- **RQ2**: How can course-specific content be effectively integrated to ensure domain-relevant and accurate responses?
- **RQ3**: What techniques and architectural strategies can be employed to effectively reduce hallucinations in large language model-based tutoring systems?
- **RQ4**: How can the system generate more accurate, context-aware, and educationally valuable answers that support meaningful learning?
</v-clicks>


---
src: ./pages/datasets.md
---

---
src: ./pages/baseline.md
---

---
src: ./pages/raft-pipeline.md
---

---
src: ./pages/evaluation.md
---

---
src: ./pages/conclusion.md
---

---
layout: cover
---

# Thanks