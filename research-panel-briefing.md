---
name: research-panel-briefing
description: Runs a structured, multi-perspective deep-research investigation on any contested or complex topic by simulating five expert viewpoints (Practitioner, Academic, Skeptic, Economist, Historian), mapping where they contradict, synthesizing an executive research briefing, then peer-reviewing it for confidence and bias. Saves a citable report as Markdown or Word, in the spirit of Stanford's STORM methodology. Use whenever the user wants to deeply research a topic, asks for a "research briefing," "深度研究," "多视角分析," wants a topic examined from multiple expert angles, mentions STORM, or wants a controversial/contested topic investigated before a recommendation. Trigger even without these exact words — any request for in-depth, well-rounded research where evidence quality and disagreement matter (not a quick factual lookup) should use this.
---

# Research Panel Briefing

This skill runs a deep, multi-perspective research investigation. Instead of answering a contested topic with a single confident take, it walks through four progressively-deepening stages designed to surface genuine disagreement before forming a synthesis. The point is intellectual honesty: a contested topic rarely has one settled answer, and no single voice — including Claude's own first instinct — should quietly dominate the conclusion.

Use this for topics where reasonable, informed people actually disagree: health and nutrition debates, economic policy, technology adoption, historical controversies, scientific disputes, business strategy calls, social/cultural debates. Don't use it for simple factual lookups ("when was X founded") — there's no panel to convene for those.

## Step 0: Confirm scope and research mode

Before starting, make sure you have two things (ask only what isn't already clear from the request):

1. **The topic.** If it's vague ("AI safety"), either ask the user to narrow it slightly or propose a specific framing and confirm before going further — the whole exercise is more useful on a well-scoped question.

2. **Research mode.** This determines whether you actually search the web or rely on reasoning alone, and it changes how much the final report can be trusted — so resolve it deterministically from the prompt's wording rather than guessing:

   - **Grounded mode (real search + citations)** — trigger this when the request contains language like "联网检索" / "联网搜索" / "联网" / "真实来源" / "有据可查" / "查证" / "引用真实来源", or English equivalents like "web search," "real sources," "grounded," "cited," "verified research," "fact-check." In this mode, use whatever web search / fetch tool is available throughout every step to find actual studies, expert statements, data, and critiques. Every substantive claim in the final briefing should trace back to a real source, cited inline (short paraphrases, no long quotes — follow whatever citation convention the current environment uses). Slower, but the output is genuinely STORM-like: verifiable.
   - **Reasoning mode (no search)** — trigger this when the request contains language like "不联网" / "不用联网" / "不要搜索" / "纯推理" / "不用检索", or English equivalents like "no search," "reasoning only," "don't search the web," "brainstorm." Rely on existing knowledge to simulate the five perspectives. Faster, good for exploratory or conceptual/philosophical topics where evidence is thinner. Label the output clearly as synthesized reasoning rather than verified research, and explicitly flag specific factual claims (named studies, statistics, dates) you're not certain of instead of stating them with false confidence — don't invent a citation-shaped sentence for something you haven't actually verified.
   - **Neither phrase present** — don't guess silently and don't assume tool availability either way. Ask one direct question in plain text (e.g. "这次需要联网检索真实来源,还是纯推理分析就行?") and wait for an answer before proceeding. This keeps the skill portable across any agent environment, chat or otherwise — it doesn't rely on any particular UI element to ask the question.

3. **The user's role/angle** (for Step 3's actionable insight) — e.g. investor, policymaker, product manager, parent, founder. If they don't offer one, "a general, informed decision-maker" is a fine default.

## Step 1: Five expert perspectives

Simulate five distinct, genuinely-differentiated viewpoints on the topic. Don't write five perspectives that secretly agree — steelman each one, including the ones you might personally find less compelling.

For each of the five, produce:
- **Core position** — 2 sentences.
- **Strongest evidence supporting their view** — in grounded mode, real sources, cited; in reasoning mode, describe the kind of evidence that would back this position, flagged as illustrative rather than verified.
- **The one thing they'd tell you that no other perspective would** — the distinct insight only this vantage point produces.

The five perspectives:

1. **THE PRACTITIONER** — works with this daily. What do they know that academics miss? What practical realities get ignored in theory?
2. **THE ACADEMIC** — has studied this for years. What does the peer-reviewed evidence actually say? Where does it contradict popular belief?
3. **THE SKEPTIC** — thinks the mainstream view is wrong. What's the strongest real counterargument? What do proponents conveniently ignore?
4. **THE ECONOMIST** — follows the money. Who profits from the current narrative? What financial incentives shape the research or the discourse?
5. **THE HISTORIAN** — has seen similar patterns before. What historical parallels exist, and what happened when those played out?

In grounded mode, actively search for material that represents each angle — practitioner interviews/forums, peer-reviewed papers or meta-analyses, contrarian critiques, industry/financial analysis, historical case studies — rather than inventing plausible-sounding specifics. If you can't find solid real support for a perspective, say so honestly instead of filling the gap.

## Step 2: Map the contradictions

Treat the five write-ups as a dataset and analyze them as a set:

1. **Direct contradictions** — where do two or more perspectives clash? List each conflict with the specific claims that clash.
2. **Evidence strength ranking** — which perspective has the strongest evidence behind it? Which the weakest, and why?
3. **The crux question** — the one question that, if answered, would resolve the biggest contradiction.
4. **Universal agreement** — what do all five perspectives agree on? (This is probably true — even the people who disagree on everything else confirm it.)
5. **The blind spot** — what did none of the five perspectives address? This is often the most valuable finding, since it marks where the field hasn't looked.

## Step 3: Synthesize the research briefing

Pull Steps 1–2 into one structured briefing:

1. **One-paragraph summary** — explain the topic as if briefing a CEO who has 60 seconds and needs the nuance, not just the headline.
2. **Five key findings**, ranked by reliability. For each, note which perspectives support it and which challenge it.
3. **The hidden connection** — one non-obvious link between findings that only becomes visible by holding all five perspectives together.
4. **The actionable insight** — given the user's stated role, what should they actually do differently? Be concrete, not generic.
5. **The frontier question** — the single open question that, if answered, would most change how this topic is understood.

## Step 4: Peer-review the briefing

Critique the Step 3 synthesis the way a skeptical reviewer would — this step exists specifically to stop the briefing from being trusted more than it deserves:

1. **Confidence scores** — rate each of the five key findings 1–10 for reliability, with a one-line reason for each score.
2. **Weakest link** — which claim are you least confident in, and what specific information would be needed to verify it?
3. **Bias check** — which of the five perspectives ended up overrepresented in the synthesis? Did one voice quietly dominate?
4. **Missing perspective** — is there a sixth angle that should have been included, and would it change the conclusions?
5. **Overall grade** — if a Stanford professor reviewed this briefing, what grade would they give, and what's the one thing they'd tell you to fix?

Be genuinely critical here, not performatively so — if a finding deserves a 4/10, say 4/10. False modesty ("everything's a 7") defeats the point of this step as much as false confidence does.

## Output: save the briefing as a file

The user wants this kept as a deliverable, not left in the chat scrollback. After Step 4:

1. Compile Steps 1–4 into one polished document (Steps 3–4 as the main body, Steps 1–2 as supporting detail/appendix).
2. Default to Markdown (.md). Use Word (.docx) instead if the user asked for Word specifically, or the context is clearly a formal deliverable for clients/leadership — if so, read `/mnt/skills/public/docx/SKILL.md` before producing it.
3. In grounded mode, include a final "Sources" section listing the URLs actually used.
4. Save to `/mnt/user-data/outputs/` and share it via `present_files`. Don't just print the whole document inline in chat after saving it — the file is the deliverable.

## Notes on tone and rigor

- Resist false balance: if the grounded evidence clearly favors one perspective, the Step 4 confidence scores and grade should say so rather than averaging everything into a comfortable "it's complicated."
- Resist contrarianism for its own sake: the Skeptic's job is to steelman the strongest *real* counterargument, not manufacture controversy where the evidence is actually solid.
- This exercise earns its keep on genuinely contested, multi-stakeholder topics. If the user's question turns out to be a simple, settled factual matter, say so honestly rather than padding five perspectives onto something that doesn't need them.
