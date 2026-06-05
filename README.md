# Design Research Skills Library

A shared library of AI skill specs for the design research and innovation team. Each skill is a structured markdown file that tells Claude how to assist with a specific research task — consistently, without needing to re-explain context each time.

---

## What Is a Skill?

A skill is a `SKILL.md` file that encodes:
- **When** to use a particular AI augmentation
- **How** Claude should approach the task
- **What** the output should look like
- **Where** the ethical boundaries are — what the AI must never do

Skills are not prompts you write from scratch each time. They are reusable, versioned, and shareable across the team.

---

## Ethical Framework

Every skill in this library has been assessed against four dimensions:

| Dimension | Question |
|---|---|
| **What it kills** | What human capability, serendipity, or researcher satisfaction does this risk removing? |
| **Researcher desirability** | Would an experienced researcher actually want this? (Rated 1–5) |
| **Feasibility** | Is this available now, low-build, or medium/high build? |
| **Hard stops** | What must AI never do in this task? |

Skills that automate core research work — coding qualitative data, clustering themes, interpreting patterns, developing insights, synthesising findings — are not in this library. Those tasks are the work. This library augments everything around them.

---

## How to Use a Skill

1. Open the relevant `SKILL.md` from this repo
2. In Claude, go to **Settings > Custom Instructions** or add to your project context
3. Paste the full skill spec, or reference it in your project system prompt
4. Use the trigger phrases listed in the skill to invoke it

---

## Library Structure

```
design-research-skills/
├── README.md
├── radar-scanning/
│   └── SKILL.md
├── literature-review/
│   └── SKILL.md
├── qual-data-collection/
│   └── SKILL.md
├── workshop-design/
│   └── SKILL.md
└── experiment-log/
    └── SKILL.md
```

Each folder = one skill domain. Add subfolders if a domain has multiple skills.

---

## How to Add a New Skill

1. Create a new folder using the naming convention: `domain-task` (e.g. `interview-guide-drafting`)
2. Add a `SKILL.md` using the team's standard schema (see any existing skill for the template)
3. Every skill must include the ethical assessment — no exceptions
4. Open a pull request with a one-line description of what the skill does and what experiment it came from (reference the experiment log ID)

---

## Linked Resources

- **Experiment Log:** `Design_Research_AI_Experiment_Log.xlsx` — tracks every experiment the team has run, including what worked, what didn't, and what became a skill
- **Skill Schema:** see any `SKILL.md` in this repo for the full template

---

## Maintainers

Design Research & Innovation Team  
*Questions or additions — open an issue or speak to the team lead.*
