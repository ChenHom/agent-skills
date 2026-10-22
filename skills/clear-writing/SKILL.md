---
name: clear-writing
description: Write or revise clear explanations, everyday prose, work reports, proposals, tutorials, and technical handoffs including commit and PR descriptions. Use when drafting these deliverables or when the user asks for clearer, plainer, easier-to-understand writing. Preserve creative voice in stories and marketing copy. Do not rewrite verbatim quotations, exact translations, code, or machine-readable output unless requested.
---

# Clear Writing

Use ASD-STE100-inspired clarity principles to reduce the reader's effort without losing meaning. Apply them to the requested writing, not to unrelated work.

## Scope

- Support general explanations, workplace writing, teaching, and technical writing in the user's requested language. Default to Traditional Chinese when the conversation uses it.
- Treat this as an adaptation, not formal ASD-STE100 compliance. Formal STE includes an approved English dictionary and detailed rules. Do not impose English word-count limits on Chinese or claim an arbitrary compliance percentage.
- Preserve the requested voice, audience, length, and format. For creative prose, use clarity selectively and retain imagery, rhythm, humor, and emotion.
- Applying this skill does not authorize commits, publishing, sending messages, changing repository configuration, or other external actions.

## Workflow

1. Infer the reader, purpose, and writing type from the request. Ask only when a missing detail materially affects the result.
2. Identify the main message and the facts that support it. Preserve conditions, exceptions, uncertainty, and causal relationships. Do not invent missing facts to make the prose sound complete.
3. Choose a structure that fits the purpose. For an explanation, answer first and then explain why or give an example. For a procedure, state prerequisites and place warnings before the affected action. For creative writing, preserve the narrative structure.
4. Draft or revise using the rules below. Read [examples](references/examples.md) only when examples for the selected writing type would help.
5. Check the result for changed meaning, inconsistent terms, unsupported certainty, and unnecessary repetition. Deliver the requested text without an unsolicited editing report. Include a short explanation of changes only when requested or useful.

## Writing Rules

- Give each sentence one main idea. Split overloaded sentences, but keep connected reasoning together. Avoid a sequence of disconnected fragments.
- Use the same term for the same concept. Keep identifiers, commands, error codes, units, and official names exact. Explain unfamiliar terms at first use when needed.
- State who or what performs an action when it matters. Prefer direct verbs: use “調整設定” rather than “進行設定的調整”.
- Put a condition before its dependent action when readers must know the condition first. Keep the scope of conditions and exceptions explicit.
- Use short, familiar wording without deleting necessary context. Do not shorten “can fail” into “fails”, “recommended” into “required”, or a correlation into a cause.
- Replace vague praise such as “提升可靠性” with the concrete behavior when evidence supports it. If details are unavailable, acknowledge that limitation rather than inventing specifics.
- Use paragraphs for connected reasoning, lists for steps or parallel items, and tables for comparisons. Add diagrams only when relationships are difficult to explain in text; do not generate interactive pages or videos merely because this skill is active.
- Separate observations, interpretations, and recommendations when readers might otherwise confuse them. Preserve source attribution and quotation wording.

## Adapt to the Deliverable

- **Everyday explanation:** answer the actual question, then add only the context and examples the reader needs. Do not force a report template onto a simple answer.
- **Report or proposal:** state the result or proposal, explain its basis, and identify decisions or next actions when relevant. Distinguish actual outcomes from forecasts.
- **Tutorial or procedure:** give executable steps in order. Usually use one action per step; keep simultaneous actions together when separating them would change the procedure. Include observable outcomes when available.
- **Commit:** describe the specific problem or change. Add the reason and actual validation when useful or required by the repository. Scale length to the change.
- **PR or technical handoff:** describe the final behavior, rationale, validation, and material limitations. Follow the repository template. Use verified file locations and evidence; never invent test runs or deployment status. When source access is unavailable, label the result as a draft based on supplied information.
- **Creative writing:** improve accidental ambiguity and awkward wording while preserving intentional ambiguity and style. Do not flatten all sentences into commands or remove deliberate repetition.

## Sources and Boundaries

These principles are adapted from ASD-STE100, not a reproduction of its full rules or dictionary:
- [Official overview](https://www.asd-ste100.org/about_STE.html)
- [Official FAQ](https://www.asd-ste100.org/STE_faq.html)
- [Request the official standard](https://www.asd-ste100.org/STE_downloads.html)

Evidence reporting for commits and PRs is an additional engineering practice, not a claim about STE requirements. For formal English STE compliance, consult the requested official edition and its dictionary; this skill alone cannot certify compliance.
