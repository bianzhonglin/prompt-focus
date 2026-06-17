---
name: prompt-focus
description: Review and optimize an LLM prompt (system/user prompt, instruction template) so it is focused, clear, contradiction-free, and keeps every output contract. Use when the user says "optimize this prompt", "make the prompt focused", "the prompt drifted / is verbose / repeats itself / contradicts the code", or "I edited the prompt, clean it up". Model-agnostic and project-agnostic.
user-invocable: true
---

# Prompt Focus — Review & Optimize LLM Prompts

Tighten a prompt written for an LLM so it is **focused, clear, executable, and constraint-complete**.
The audience is the **model that runs the task**, not a human maintainer: the model only needs
"what to do, how to do it, which hard constraints apply, what output format" — not background
narration that does not change its behavior.

Works on any system prompt, user-prompt template, or agent instruction. Model- and project-agnostic.

## When to trigger

- The user asks to optimize a specific prompt.
- After the user edited a prompt and it drifted: got verbose, repeated itself, contradicts itself,
  carries useless background, diluted a constraint, or pulled in out-of-scope requirements.
- If the target prompt is unclear, ask which one first. Do not batch-edit prompts unprompted.

## Workflow

1. **Locate + read in full.** Get the entire target prompt.
2. **Cross-check against ground truth (if a codebase exists).** If the prompt describes the structure
   or allowed values of any field/output, verify it against the real validation logic (schema,
   validator, parser, downstream consumer). When prompt and code disagree, **the code wins** — fix the
   prompt. A wrong constraint description makes the model emit invalid output; this is the top priority.
   For a standalone text prompt with no code, treat the user's stated intent and any given examples as
   ground truth instead.
3. **Extract the hard-constraint list first** (see Guardrails): output format, field names, enum values,
   allow-lists, count limits, required/default-item rules. This is what must survive verbatim.
4. **Run the seven-dimension review**, deleting/merging then adding/clarifying. For each deletion ask:
   "If I remove this, does the model's output get worse?" If no, delete it.
5. **Verify.** Assert the hard constraints still appear and the redundancy is gone; run any relevant
   tests. Never assume the change took effect.

## Seven-dimension review checklist

First four are delete/merge; last three are add/clarify.

1. **Drop meta-description (focus).** Remove background with no operational meaning to the model:
   "this is stage N of the pipeline", "the upstream/downstream is X", "why it was designed this way",
   "does not depend on X". State what to output, not where it sits in the system.
2. **De-duplicate.** State each constraint once, in the best place (usually the rules section). Common
   repetition: the same sentence restated in the goal, the rules, the example heading, the reference
   section, and the final requirements — collapse to one.
3. **Drop noise.** Delete reference blocks the current task does not use (e.g. embedding a whole
   allow-list/enum table for a field this stage does not output). Test: is this block a required input
   for the current task's inference/output? If not, delete it.
4. **Disambiguate.** Replace vague wording with decidable phrasing: "keep it short" → "no more than 3
   sentences"; "an appropriate format" → give the exact JSON structure. Quantify whenever possible.
5. **Fix contradictions.** Constraints must be consistent with each other, with the examples, and with
   real validation. Classic: a rule says "strict allow-list" while the code does not validate that
   field and allows free text → correct the description to match the code.
6. **Show, don't just tell.** Give one example that demonstrates the expected output format; add a
   counter-example / forbidden case where mistakes are likely. Examples must be copy-paste-ready in
   structure and labeled "do not output the example content itself".
7. **Structure.** Organize with clear sections (role / task / constraints / output format / examples /
   reference) and delimiters (Markdown headings, XML tags). Put instructions first, long reference last.

## Six most common drifts after a user edits a prompt → fix

1. **Stacked duplicates** — the new constraint was added alongside the old one instead of replacing it
   → merge synonymous constraints; keep one authoritative statement.
2. **Contradiction** — a newly added requirement fights an existing constraint or example → find both
   sides, confirm the intended one with the user, keep a single rule.
3. **Scope drift** — a field/requirement unrelated to this prompt's task got tacked on → move it back to
   the prompt it belongs to, or delete it.
4. **Diluted constraint** — "must / never / exactly N" hard wording was softened for fluency → restore
   the imperative force of the hard constraint.
5. **Embedded rationale** — the "why we changed it" note was written into the prompt body → move such
   notes to code comments / docs, not the prompt.
6. **Loosened format contract** — editing copy changed the JSON structure / field names / enums out of
   sync with the parser → realign to the parser and lock the contract.

## Guardrails (never break)

- **Never delete hard constraints**: output format, field names, enum values, allow-lists, count
  limits, required items, default-item rules (e.g. exactly-one-default).
- **Never change business semantics or the output contract** — change wording only, not "what is
  wanted". If the contract must change, confirm with the user first.
- **Never optimize a prompt that was not named.**
- **Always verify after editing**: assert hard constraints still present + run relevant tests. Do not
  judge success by eye.
- **Focus is not constraint-cutting**: trim redundant phrasing, not the constraints themselves.

## Authoritative basis

- Write clear instructions, use delimiters, specify the steps and the output length/format, show
  examples (show & tell), split complex tasks into subtasks, give the model room to think
  — OpenAI Prompt Engineering Guide.
- Be clear and direct, use multishot examples, organize with XML/structured tags, assign a role, use
  chain-of-thought, control the output format, eliminate ambiguity and contradictions
  — Anthropic Prompt Engineering (prompting best practices).

## Verification

With a codebase (adapt to the actual prompt and tests):

```python
from your_module import TARGET_PROMPT as s
assert "this is stage" not in s.lower() and "does not depend" not in s.lower()  # meta-desc removed
assert s.count("<a constraint keyword>") <= 1                                   # constraint not repeated
assert "<an enum / allow-list value>" in s                                      # hard constraint intact
```
Then run the relevant prompt/contract tests.

Standalone text prompt (no code): re-read the optimized prompt against the hard-constraint list from
step 3 and confirm each item is still present and unambiguous.
