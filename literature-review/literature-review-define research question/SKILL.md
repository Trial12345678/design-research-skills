---
name: research-question-inverted-triangle
description: "Invoke when a researcher needs to develop or sharpen a research question using the inverted triangle method — narrowing from broad concept to bounded, answerable question. Includes question typology classification and FINER validity check. Works across design research, social science, and academic contexts."
---

The user provides a broad topic area, a partial question draft, or both. Claude 
produces a structured inverted triangle breakdown, a question type classification, 
and one or more candidate research questions with rationale for each narrowing 
decision.

## When To Use This

- "Help me develop a research question around [topic]"
- "My research question feels too broad / too vague"
- "I have a topic but don't know how to frame the question"
- "Sharpen this draft research question: [draft]"
- User is at the start of a literature review, dissertation, qual study, or 
  client research project and hasn't yet fixed the question

## Approach

Work through three levels explicitly. Do not collapse them.

**Level 1 — Concept (broad)**  
Name the overarching theoretical or social concept at stake. One or two words. 
This is the tip of the triangle. Ask: what is the larger phenomenon this sits 
within? (e.g. Precarity, Trust, Identity, Governance)

**Level 2 — Phenomenon (mid)**  
Narrow to a specific instance, manifestation, or domain of that concept. This 
is where the research lives — still broad enough to be interesting, specific 
enough to be tractable. (e.g. Job security in the gig economy)

**Level 3 — Research Question (point of triangle)**  
Frame a bounded, answerable question that specifies: the subject, the context 
or scope constraint, and what you are trying to understand or explain.

**Question Type — what kind of knowledge does this question seek to produce?**  
Classify the question before applying FINER. The type should be explicit because 
it determines method, scope, and what counts as a valid answer.

| Type | Logic | Signal phrases | Example |
|---|---|---|---|
| Descriptive | What exists / what is happening | "What are...", "How do..." | What practices do gig workers use to manage income uncertainty? |
| Exploratory | What is the nature or texture of X | "How does...", "What is the experience of..." | How do Deliveroo riders navigate the absence of employment protections? |
| Explanatory / Causal | Why does X produce Y | "Why does...", "What causes..." | Why do platform-based employment models increase financial precarity? |
| Generative | What new possibilities exist | "How might...", "In what ways could..." | How might algorithmic management be redesigned to support rider agency? |
| Evaluative | To what extent does X achieve Y | "To what extent...", "How effective is..." | To what extent do Irish labour laws protect workers classified as independent contractors? |

Flag if the question type implies a method the researcher may not have access to 
(e.g. causal questions require longitudinal data or controlled conditions; 
generative questions suit co-design or speculative methods).  
Flag if the researcher's stated method and question type are misaligned.

Decision points to navigate:
- If the user gives only a topic, generate 2–3 candidate Level 2 phenomena 
  before committing to one — let the researcher choose the angle
- If the user gives a draft question, diagnose first: is it too broad (no 
  scope constraint), too narrow (no theoretical grounding), or ambiguous 
  (unclear what kind of answer is being sought)?
- Always make the epistemological stance explicit: is this exploratory 
  (what/how), explanatory (why), or evaluative (to what extent)?
- Flag if the question as framed implies a method mismatch 
  (e.g. a "why" question answered through secondary data alone)

## Output Format

```
LEVEL 1 — CONCEPT
[One word or short phrase]

LEVEL 2 — PHENOMENON  
[One sentence: the specific manifestation being studied]

LEVEL 3 — CANDIDATE RESEARCH QUESTION(S)
Q1: [Full question]
Rationale: [Why this framing; what it makes possible; what it closes off]

Q2 (alternative framing): [Full question, different angle or scope]
Rationale: [...]

QUESTION TYPE: [Descriptive / Exploratory / Explanatory / Causal / Generative / Evaluative]
Method implication: [One line on what this type requires or rules out]

FINER CHECK (on recommended question)
Feasible: [Yes/Partial/No — brief note]
Interesting: [Why this matters to the field]
Novel: [What it adds beyond existing work — flag if unknown]
Ethical: [Any participant or data ethics considerations]
Relevant: [Relevance to context or client]

RECOMMENDED: Q[n] — [One sentence on why]
```

Length: Concise. The triangle output should fit on one page.

## Constraints and Watch-outs

**Never do:**
- Generate the research question without showing the narrowing steps — the 
  triangle is the method, not just the output
- Produce a question so broad it could anchor an entire PhD when the user needs 
  a bounded study
- Suggest the "best" question without stating what it trades off
- Assign a question type without explaining its method implications

**Commonly fails when:**
- The user's topic is genuinely too underdeveloped — in that case, ask one 
  clarifying question before proceeding: "What drew you to this topic?" The 
  answer usually contains the Level 2 phenomenon
- The context (sector, geography, population) is missing — a question without 
  scope is not a research question
- The researcher conflates question types (e.g. frames a generative question 
  but plans a descriptive method) — name the mismatch explicitly

**Ethical flag:**  
This skill augments structuring and elicitation — it does not generate the 
research question for the researcher to adopt wholesale. The researcher must own 
the question. Risk of anchoring: the first candidate question Claude produces 
may foreclose angles the researcher hasn't considered. Always offer at least two 
framings.

Researcher desirability: **4/5** — experienced researchers will use this as a 
thinking partner and push back on framings; junior researchers risk accepting 
the output uncritically.

## Example Prompt

I'm researching {{broad topic or draft question}}. 
Context: {{field / sector / population if known}}.  
{{Optional: what I already know or have read}}.
Use the inverted triangle to help me develop a rigorous, bounded research 
question.
