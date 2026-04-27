---
theme: academic
title: Phd Interview behrooz
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

# TripartiteRAG 
---
layout: two-cols-header
---

# TripartiteRAG
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

### 🎯 Thesis Goal

My thesis aims to address and solve these limitations by designing a system that:

<v-clicks>

- Adapts responses to the student’s knowledge level.
- Incorporates course‑specific content.
- Reduces hallucinations.
- Provides more accurate, context‑aware answers.
</v-clicks>
---
layout: two-cols-header
---

### Data Structure

::left::
<v-click>
```mermaid
flowchart TD
    symbol["Symbol(Topic)"]
    definition["Definition"]
    explain["Explain"]
    LM["Learner Model"]
    prerequisites["Prerequisites(symbol)"]
    symbol---explain
    symbol---definition
    LM-.-symbol
    prerequisites-->symbol
```
</v-click>
::right::
<v-clicks>

- All symbols and their relationships are stored in GraphDB, and data retrieval is possible only via SPARQL queries.
- The learner model is a separate system that predicts a student’s level of understanding based on their interactions with quizzes and problem‑solving tasks.
- The learner model data should get online, it is different for every user and changes frequently.
- You can see the whole system on the [ALeA system](https://alea.education/).
</v-clicks>
---

## Leaner Model

Leaner model is a probably base model tried to predict student understanding by their activity on quizzes and practice questions.
It calculate six expect of confidences of a topic. 

It fully complies with the European Union's privacy laws.


```ts
{
      "concept": "http://mathhub.info?a=FTML/math&p=propositions&m=prop&s=false",
      "confidences": {
        "Analyse": 0,
        "Apply": 0,
        "Create": 0,
        "Evaluate": 0,
        "Remember": 0.8213587457090796,
        "Understand": 0
      }
    },
```
---

## ✅ What I have done so far! 

### Create a small dataset of question

- Questions from AI2, AI1, and the SMAI content course are being added to a dataset.
- The dataset currently contains roughly 20 questions.
- In the coming weeks, more details and additional questions on these topics will be added.
- Some questions in the dataset already have answers, while others do not.
- The system is personalized for every person, which is why not all questions have fixed/standard answers.
- The instructor can specify topics or elements to include (e.g., “include this topic”), but cannot dictate strict, uniform answers for everyone.

---

### Indexing
<v-switch>
<template  #1>

```mermaid
flowchart LR
    Data["Data"]
    Data
```

#### Data
- The course materials and content related to each section, along with the UUID.
</template >

<template #2>
```mermaid 
flowchart LR
    Data["Data"]
    Process["Chunking"]
    Data-->Process
```
</template>
<template #3>
```mermaid 
flowchart LR
    Data["Data"]
    Process["Chunking"]
    Storage
    Data-->Process-->Storage
```
</template>
</v-switch>

---

### Generating
<v-click>

```mermaid
flowchart LR
input["`User Question`"]
VectorSearch["Vector Search"]
KeywordExtractor["Keyword Extractor"]
LexicalSearch["Lexical Search"] 
RetrievedScored["Retrieved and Scored Content"]



input-->VectorSearch
input-->KeywordExtractor-->LexicalSearch
VectorSearch-->RetrievedScored
LexicalSearch-->RetrievedScored



```

</v-click>

<v-click>

***
```mermaid
flowchart LR
BuildPrompt["Build Prompt"]
GetUserKnowledgeStatus["Get User Knowledge Status"]
RetrievedScored["Retrieved and Scored Content"]
GatherPrerequisites["Gather Prerequisites"]
GatherSymbols["Gather Symbols"]
RetrievedScored-->BuildPrompt
RetrievedScored-->GatherSymbols
RetrievedScored-->GatherPrerequisites
GetUserKnowledgeStatus-->BuildPrompt
GatherPrerequisites-->GetUserKnowledgeStatus
GatherSymbols-->GetUserKnowledgeStatus
```
</v-click>

---

## Demo
>Q: What is an AI agent?
<br>

>A: An AI agent is a software program that performs tasks and makes decisions on its own, using artificial intelligence (AI) techniques to interact with its environment and achieve specific goals.
There are several types of AI agents, including:
Goal-based agents: These agents have a set of goals or objectives that they try to achieve. They use reasoning and planning to determine the best course of action to reach their goals.
Utility-based agents: These agents evaluate actions based on their expected utility or reward. They choose the action with the highest expected utility, which is often calculated using a utility function.
Model-based agents: These agents have an internal model of the world and use it to reason about the consequences of their actions. They can plan and predict the outcomes of different actions.
Some key characteristics of AI agents include:
Perception: The ability to sense and understand the environment, including perceiving inputs such as sensor data or user requests.
Action: The ability to perform tasks and take actions in the environment, such as moving a robot arm or sending an email.
Reasoning: The ability to draw conclusions and make decisions based on available information and knowledge.
Learning: The ability to improve performance over time through experience and adaptation.
AI agents can be used in a wide range of applications, including:
Robotics
Virtual assistants (e.g. Siri, Alexa)
Chatbots
Recommendation systems
Autonomous vehicles
Overall, AI agents are an essential component of many modern AI systems, enabling them to interact with the world, make decisions, and achieve their goals.
---

## Remaining Tasks

<v-clicks depth=2>

- Evaluating my results.
    - Human review: instructor/TA rubric
    - LLM as judge: does the answer align with retrieved fragments?
- Try the RAFT method
    - Prepare a small dataset with questions and answers.
    - Fine-Tuning the model.
    - compare RAG results with new Results.
</v-clicks>