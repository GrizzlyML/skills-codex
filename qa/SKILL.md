---
name: qa
description: "Use in Codex for interactive QA, bug reporting, and issue drafting from observations. Clarifies symptoms, explores the codebase for domain context, and prepares durable GitHub issues in the project's domain language."
metadata:
  short-description: Turn QA observations into durable issues
---

# QA Session

Run an interactive QA session. Clarify the user's observations, explore the codebase for context, and prepare GitHub issues that are durable, user-focused, and use the project's domain language.

## For each issue raised

### 1. Listen and lightly clarify

Let the user describe the problem in their own words. Ask **at most 2-3 short clarifying questions**:

- What you expected vs what actually happened
- Steps to reproduce (if not obvious)
- Whether it's consistent or intermittent

Do not over-interview. If the description is clear enough, move on.

### 2. Explore the codebase in background

While talking, explore the relevant area to:

- Learn the domain language (check `docs/UBIQUITOUS_LANGUAGE.md`)
- Understand what the feature is supposed to do
- Identify the user-facing behavior boundary
- Check which bounded context this belongs to (`docs/CONTEXT_MAP.md`)

This helps me write a better issue — but the issue itself will NOT reference files, line numbers, or implementation details.

### 3. Assess scope

Before filing, decide: **single issue or breakdown?**

**Break down when:**
- Fix spans multiple independent areas
- Clearly separable concerns exist
- Multiple distinct failure modes or symptoms

**Keep as single when:**
- One behavior wrong in one place
- Symptoms share the same root behavior

### 4. File the GitHub issue(s)

Create with the GitHub connector or `gh issue create` when available. Before creating externally visible issues, confirm with the user unless they explicitly asked you to file them.

**All issues must be durable** — they should still make sense after major refactors.

#### Single issue template

```markdown
## What happened

[Actual behavior in plain language, using domain terms]

## What I expected

[Expected behavior]

## Steps to reproduce

1. [Concrete, numbered steps]
2. [Use domain terms, not module names]
3. [Include relevant inputs, flags, config]

## Additional context

[Extra observations — use domain language, don't cite files]
```

#### Breakdown template (per sub-issue)

```markdown
## Parent issue

#<parent-number> or "Reported during QA session"

## What's wrong

[This specific behavior problem, just this slice]

## What I expected

[Expected behavior for this slice]

## Steps to reproduce

1. [Steps specific to THIS issue]

## Blocked by

- #<issue-number> or "None — can start immediately"

## Additional context

[Relevant to this slice]
```

### Rules for all issues

- **No file paths or line numbers** — they go stale
- **Use the project's domain language** (from `UBIQUITOUS_LANGUAGE.md`)
- **Describe behaviors, not code** — "the experiment stats show 0 visitors" not "getExperimentStats() returns empty"
- **Reproduction steps are mandatory**
- **Keep it concise** — readable in 30 seconds

After filing, share all issue URLs and ask: "Next issue, or are we done?"

### 5. Continue the session

Keep going until you're done. Each issue is independent.

## Related skills

- `$holistic` — understand the broader context of a bug before filing
- `$domain` — if a bug reveals a terminology or domain model issue
- `$tdd` — implement the fix using tracer-bullet TDD
