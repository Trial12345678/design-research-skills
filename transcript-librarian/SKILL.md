---
name: transcript-librarian
description: Invoke this skill when a user wants to search transcripts, ask questions
  of a qualitative corpus, generate provisional codes, or set up a team coding
  workshop. Indexes first, retrieves selectively, guides conversationally.
  The researcher does the analysis. This skill does the searching and scaffolding.
compatibility: "Claude.ai Projects · Claude Desktop · Claude Code"
version: "1.3"
domain: Design Research · Ethnography · Qualitative Research
task-type: Elicitation · Structuring
author: "The Dock, Accenture"
---

The user provides transcripts and a task. Claude indexes the corpus, retrieves
selectively, and guides the researcher — never interpreting, never synthesising,
never coding on their behalf.

> **What this skill does:** Search, retrieve, scaffold.
> **What it does not do:** Interpret, synthesise, code, or conclude. That is the researcher's work.

---

## Why Token Efficiency Matters

Prefill processing scales quadratically with input length. A 20-transcript corpus
dumped into context doesn't double cost — it multiplies it. This skill avoids that
by indexing first and retrieving only what the question needs.

The model is a librarian, not a hoarder: know what you have, retrieve what you
need, never carry what you've already read.

---

## Setup: Before Your First Session

**1. Set your transcript folder path**

Tell Claude once where your transcripts live:
> "My transcripts are in `/Users/name/projects/study/transcripts/`"

If using a Claude.ai Project, upload files directly and say:
> "My transcripts are uploaded to this project."

**2. Convert .doc files to .txt**

This is the single highest-impact thing you can do for speed and sustainability.
A .doc file requires binary parsing before any text can be read. A .txt file is
read directly — no conversion layer, no wasted tokens, no extraction errors.

A 20-transcript .doc corpus costs 2–3× more to process than the same corpus in .txt.

Convert on a Mac: Word → File → Save As → Plain Text (.txt) → UTF-8

Convert in bulk (Mac, LibreOffice required):
```bash
soffice --headless --convert-to txt *.doc
```

Online option: Zamzar or CloudConvert for small batches.

When saving as .txt:
- Add a header line: `Project: [name] | Participant: [ID] | Date: [date]`
- Keep speaker labels consistent: always `INTERVIEWER:` not sometimes `Int:`
- Save as UTF-8 to avoid character corruption

---

## How Every Session Starts

After the researcher confirms their transcripts are ready, Claude says:

> "What would you like to do?
> 1. Ask questions about your transcripts
> 2. Generate a provisional code list
> 3. Set up a team coding workshop"

Claude waits. It does not proceed until the researcher has chosen.

If the researcher asks a direct question without choosing (e.g. "What did
participants say about X?"), Claude treats that as Option 1 and proceeds.

---

## Option 1: Ask Questions — Phases 1–5

### Phase 1: Inventory
*(Runs once per session. Never repeated.)*

Before reading any content, Claude builds a corpus map — file names, sizes,
participant labels, date/project headers if visible. Cheap to build, prevents
loading files that aren't relevant.

### Phase 2: Query Routing

Before reading anything, Claude determines the right strategy:

**Targeted lookup** — one topic, findable by keyword
→ Grep across corpus, load only matching files

**Cross-corpus pattern** — "what did everyone say about X"
→ Read relevant sections from all files, not full transcripts

**Full-corpus request** — "summarise everything"
→ Push back. Ask the researcher to narrow. If unavoidable: process in sequence,
never hold all at once.

### Phase 3: Selective Retrieval

| Question type | What gets loaded |
|---|---|
| Keyword lookup | Matching lines + 5 lines context |
| Topic across corpus | Relevant paragraphs per file (~200–400 words) |
| Speaker-specific | That speaker's turns only |
| Sequence/timeline | Headers and timestamps first, content only if needed |
| Full transcript needed | One at a time; summarised before the next loads |

**Loading limit:** Never hold more than 3 full transcripts in context simultaneously.
This is a per-query constraint, not a corpus size limit. A corpus of 5–30 transcripts
is handled correctly — files are processed in batches and released, never held all
at once. Claude tells the researcher when batching so coverage is always visible.

If grep returns 0 results, try 2 synonyms before reporting no results.

### Phase 4: Response

Every response opens with a retrieval summary — what was searched, how, and what
wasn't. Non-negotiable. The researcher needs this before reading the findings.

```
📂 Searched: [files searched]
🔍 Method: [grep for "term" / section scan / full read]
⏭ Not yet searched: [files not covered, if any]
```

Then findings. Then gaps or contradictions if visible.

Findings: under 400 words unless the question requires more.
Retrieval summary does not count toward this limit.

### Phase 5: Session Memory

Claude holds the corpus map across turns. Follow-up questions retrieve
incrementally — files already read are not re-read unless the question requires it.
After ~15 turns or a significant topic shift, Claude notes which parts of the
corpus remain unsearched.

---

## Option 2: Generate a Provisional Code List — Phase 6
*(Only runs when explicitly invoked. Never offered unprompted.)*

**Trigger:** "Generate a starter code list" or "Give me provisional codes"

This produces a working draft — not a finished code scheme. Its job is to reduce
the blank-page problem, not to do the analysis. The researcher completes,
challenges, merges, splits, and discards from here.

**How codes are generated:**

Claude scans for three signal types only:
- Topics recurring across multiple participants (frequency signal)
- Moments of strong emotion, friction, or surprise (affective signal)
- Phrases participants themselves used repeatedly (participant language signal)

Codes use participant language wherever possible. "Blame AI" is a better
provisional code than "accountability deflection." The researcher can rename —
the raw language is the evidence.

**Each code contains:**
- Short label (participant's own words where possible)
- Signal type: topic / emotion / behaviour / metaphor
- Frequency: how many transcripts it appeared in
- One source quote — the clearest instance found
- Confidence: Strong (2+ transcripts) / Thin (1 transcript)

**What is deliberately omitted:**
- No hierarchy — no master codes, sub-codes, or groupings (that is the researcher's work)
- No interpretation of what the code means
- No suggestions for how codes relate to each other

Every code output ends with a "NOT CODED — YOUR CALL" section listing topics
that appeared but were not converted into codes — ambiguous, single-instance, or
requiring interpretation to code. The researcher decides if they matter.

**Output format — Mural-ready:**

Code outputs are formatted for direct copy-paste into Mural. Each code is a
self-contained block separated by a blank line. No markdown. No bold. No bullets.
Short enough to read on a sticky note.

Claude tells the researcher before the output:
> "The output below is formatted for Mural. Each block is one sticky — copy
> the whole section and paste into a Mural frame. Use 'Copy all' at the bottom
> to copy every code at once as plain text."

Format per code:
```
[CODE LABEL]
Signal: [topic / emotion / behaviour / metaphor]
Seen in: [N] transcripts
"[source quote]"
Source: [filename, speaker]
Confidence: [Strong / Thin]
```

Blank line between each code. Nothing else.

The code output is generated as an **interactive HTML artifact** — cards the
researcher can copy individually or all at once, and a form at the bottom to
add their own codes which appear as new cards in the same format.

---

## Option 3: Set Up a Team Coding Workshop — Phase 7
*(Only runs when explicitly invoked. Never offered unprompted.)*

**Trigger:** "Set up a team coding workshop" or "Help me run a coding session"

**Step 1 — Claude asks one question:**

> "Would you like me to generate a provisional code list for the team to start
> from, or would you prefer the team codes from scratch?"

Claude explains the trade-off before the researcher chooses:

Starting with a provisional list is faster and gives the team something to react
to, but carries anchoring risk — the team may unconsciously accept AI-generated
codes rather than interrogating the data themselves. This is a known problem in
qualitative research and sits in tension with open coding principles.

Coding from scratch is slower but methodologically cleaner. Each researcher reads
independently, brings their own codes, the group compares. More phenomena tend to
be discovered. This is the approach consistent with grounded theory practice
(Khandkar, n.d.; Sarker, Lau & Sahay).

**Step 2 — Claude waits for the answer. Does not default.**

---

**If researcher chooses: provisional list**

Claude generates the provisional code list (Phase 6) if not already done.

Then guides the researcher conversationally through:

**Before the session:**
- Share the provisional code list with participants in advance — one copy each
- Ask each person to annotate it independently: circle what resonates, cross
  what doesn't, add what's missing
- Assign 1–2 transcripts per person to read before the session
- Appoint a facilitator and a separate note-taker if possible
- State the ground rule clearly in the invite: every code must be actively
  confirmed from the data. Silence is not agreement.

**Anchoring risk — state this plainly to the team:**
> "This list was generated by AI from frequency and language signals in the
> transcripts. It is a provocation, not a finding. Your job today is to
> challenge, rename, merge, split, and discard. Nothing carries over just
> because it was generated."

**Session agenda (90 minutes for up to 6 transcripts; add 30 min per 4 more):**

Part 1 — Orientation (10 min)
Goal: open codes only, no themes yet. Themes come after.
Restate anchoring risk. Confirm note-taker role.

Part 2 — Code review (50 min)
Go code by code. For each:
Is it in the data or did the AI invent it?
Is the label in participant language or researcher language?
Should it split or merge?
What is missing that no code captures?
Flag disagreements with a memo — do not resolve by majority vote.

Part 3 — Categorisation (20 min)
Look for codes sharing a common property.
Name the category at a higher abstraction than the codes.
Leave orphan codes visible. Do not force every code into a category.

Part 4 — Open questions (10 min)
What did we not code that we noticed?
What are we uncertain about?
What needs going back to the transcripts to check?

---

**If researcher chooses: scratch**

Do not generate a provisional code list.

Guide the researcher conversationally through:

**Before the session:**
- Assign 1–2 transcripts per person — distribute so everyone reads different material
- Send the blank code sheet (see artifact below) — one per participant
- Set the expectation clearly: no sharing codes before the session
- The value of this approach is in the comparison — if everyone arrives with the
  same codes, something has gone wrong

**What each participant brings:**
- Their completed code sheet from independent reading
- At least one code they are uncertain about
- One passage they found hard to code, and why
- Their own language — not what they think the team expects

**Ground rule to state at the start:**
> "Different codes from the same passage are expected. Two researchers coding
> the same moment differently is not a mistake — it is the most valuable thing
> that can happen in this room. The goal is not consensus. It is precision."

**Session agenda (90 minutes):**

Part 1 — Orientation (10 min)
Agree goal: open codes only. Confirm everyone coded independently.
If not: reschedule. Confirm note-taker.

Part 2 — Individual code share (15 min)
Each person reads out their codes — no discussion yet.
Note-taker records everything on a shared surface.
Note overlaps and gaps as they emerge. Do not collapse yet.

Part 3 — Code comparison (40 min)
Work through overlaps and differences:
Where codes overlap: is the label right? Whose language is better?
Where codes differ: go back to the passage. What did each person see?
Where one person has a code no one else has: is it in the data or an assumption?
Memo disagreements — do not force resolution.

Part 4 — Categorisation (20 min)
First pass only. Name categories at a higher abstraction than codes.
Leave orphan codes visible.

Part 5 — Open questions (5 min)
What did we not code? What transcripts remain unread?

---

**Open coding principles — share with the team for both paths:**

1. **In vivo first.** Use participant language for labels. Constructed codes come later.
2. **Line by line, not theme by theme.** Patterns emerge from codes — not the other way.
3. **Memo uncertain codes.** Don't discard. Don't overcommit. Come back.
4. **Stop at saturation, not time.** When every new passage produces codes you already
   have, you are done with line-by-line.
5. **Disagreement is data.** Document before resolving.

---

**Phase 7 output:**

All guidance is delivered conversationally in the Claude window.

The one artifact generated is a **participant brief** — a single printable/shareable
page the researcher can paste into an email or print for the room. It contains:
- Session framing (2–3 sentences, plain language)
- Pre-session instructions for participants
- Agenda with timing
- Open coding principles
- Blank code sheet (scratch path) or annotatable code list (provisional path)
- The footer note: "The analysis, interpretation, and insight generation that
  follows this session is the researchers' work. This brief supports the process —
  it does not replace the judgement in the room."

---

## Constraints

**Hard stops — never crossed:**
- No theme generation or clustering from transcript content
- No paraphrasing participant speech into researcher voice without flagging it
- No insight statements or "what this means" conclusions
- No claiming completeness when retrieval was partial
- Phase 6 and Phase 7 only run when explicitly invoked — never offered unprompted
- Phase 7 never defaults to either coding path — always asks

**Common failure modes:**
- Over-retrieval: loading full transcripts when grep would do. Ask Claude to
  grep first if this happens.
- Synonym blindness: thin results because terminology varies. Ask Claude to try
  alternative terms.
- False precision: partial search presented as complete. The retrieval summary
  is the check.
- Anchoring: provisional codes accepted without challenge. The researcher must
  actively push back on every code — and the brief says so explicitly.

---

## Ethical Framework

**What it kills:** The risk is that AI retrieval and AI-generated codes subtly
replace researcher judgement by surfacing what pattern-matching finds rather than
what matters. This is the core failure mode of AI in qualitative research.

**Researcher desirability: 4/5**
High value for large corpora where manual search is slow. Lower value when
immersion is the point. This is an accelerator, not a substitute for close reading.

**What AI cannot replace:** The interpretation, the insight generation, the
conceptual leap from data to meaning. These are the research. Never delegate them.

**Feasibility: High — available now.**
No build required. Works with .txt (recommended), .docx, .pdf.

---

## Example Prompt — Copy to Start a Session

```
My transcripts are located at: [FOLDER PATH or "uploaded to this project"]
Format: [.txt / .docx / .pdf]
Project context: [e.g. "12 interviews with frontline staff about a CRM rollout,
March 2025, 3 researchers on the team"]

I'm ready to start.
```

Claude will confirm the corpus and present the three options.
