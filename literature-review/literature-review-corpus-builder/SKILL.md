---
name: literature-corpus-search
description: Build a ranked, credibility-flagged source corpus for a literature review from peer-reviewed journals, working papers, books, professional body publications, and credible think tanks. Invoke when a researcher needs to establish what is already known on a topic before analysis begins.
---

The user provides a research question or topic scope. Claude searches across credible academic and policy sources and returns a flat ranked list of relevant sources with succinct annotations and credibility flags. The researcher decides what to read — Claude does not interpret, synthesise, or draw conclusions from the sources.

## When To Use This

- Trigger phrase: "build me a corpus on [topic]" or "find sources for my literature review on [topic]"
- When a researcher is starting a literature review and needs to move from a blank page to a working source list
- When an existing corpus needs to be expanded or pressure-tested for gaps

## Approach

**Step 1 — Clarify scope before searching**
Ask the user two questions before running any searches:
- What is the research question or topic? (If not already stated)
- How many sources do you need? (This changes per project — always ask)

Do not proceed until you have both answers.

**Step 2 — Search across approved source types only**
Search within these source types exclusively:
- Peer-reviewed academic journals (Google Scholar, Semantic Scholar, JSTOR, PubMed where relevant)
- Working papers and preprints (SSRN, arXiv, NBER)
- Books and monographs (prioritise those with academic or institutional backing)
- Industry / professional body publications (e.g. CIPD, CBI, ILO, WHO, OECD)
- Think tanks — credible only, assessed against these signals drawn from the On Think Tanks credibility framework:
  - Transparent funding and independence from donor influence
  - Named authors with verifiable credentials
  - Methodology disclosed
  - Track record of cited, policy-relevant work
  - Examples of credible think tanks: Brookings, ODI, RAND, Chatham House, IPPR, Resolution Foundation, Nesta, RSA
  - **Where a source cannot be fully accessed (e.g. paywalled journals), return the citation and abstract only. Do not infer content from title alone.**

**Do not include:** news articles, blogs, LinkedIn posts, consultancy thought leadership without disclosed methodology, anonymous or undated sources, or any source that cannot be verified.

**Step 3 — Rank by relevance**
Return sources as a flat list, ranked by relevance to the research question. Most directly relevant first.

**Step 4 — Prioritise recent, flag seminal**
Default to sources from the last 10 years. Where an older source is foundational to the field (widely cited, established the core framework or debate), include it and mark it explicitly as a seminal work.

**Step 5 — Apply credibility flags**
Every source gets a credibility flag. Use one of three:
- ✅ High credibility — peer-reviewed or equivalent rigour, transparent methodology, credentialed authors
- ⚠️ Credibility caveat — useful but check funding source / independence / methodology before relying on it
- 🚩 Credibility concern — include only if directly relevant; researcher should verify independently before citing

## Output Format

Open with one line confirming the research question and number of sources requested.

Then list sources in this format:

---
**[Number]. [Title]**
[Author(s)] · [Year] · [Source type: Journal / Working paper / Book / Think tank report / Professional body]
[One succinct bullet: the core argument or finding and why it is relevant to the research question]
[Credibility flag: ✅ / ⚠️ / 🚩 + one-line reason if ⚠️ or 🚩]
[DOI / URL where available]
---

Close with a short note on any obvious gaps in the corpus (e.g. limited recent work, geographic skew, practitioner perspectives missing) so the researcher knows where to dig further.

## Constraints and Watch-outs

- **Do not synthesise.** Your job is source identification and annotation. The researcher does the analysis. Never draw conclusions across sources or suggest what the literature "shows."
- **Do not pad the list.** If strong sources are limited, return fewer and say so. A shorter honest corpus is better than a longer unreliable one.
- **Popularity ≠ credibility.** Highly cited does not mean methodologically sound. Flag accordingly.
- **Think tank bias risk.** Many think tanks have funding relationships that influence findings. Always check independence signals before including. When in doubt, use the ⚠️ flag.
- **Preprint caution.** SSRN and arXiv papers have not been peer reviewed. Include when relevant but always flag as ⚠️ minimum.
- What this skill risks degrading: researcher-led discovery through citation chaining, which surfaces unexpected connections that a search agent won't find. Treat this corpus as a starting point, not a complete picture. Researcher desirability: 4/5.

## Example Prompt

```
Research question: {{e.g. What does the evidence say about psychological safety in high-performing teams?}}
Number of sources needed: {{e.g. 15}}
Any specific angles to prioritise: {{e.g. organisational context, not clinical / therapeutic settings}}
```
