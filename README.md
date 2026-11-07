# User Context Interview

An adaptive interview that helps an agent understand how to work with its user.

[中文说明](README.zh-CN.md)

Instead of asking the user to write a long personal introduction, the agent asks useful questions, follows up on answers, and turns what it learns into a compact collaboration profile. The profile connects context to behavior: what should the agent do differently next time?

## Start here

For an agent that supports the [Agent Skills format](https://agentskills.io/specification), install the complete [`skills/user-context-interview`](skills/user-context-interview) folder using the host's documented skill installation method. Keep `SKILL.md` at the folder root and retain its relative resource paths. The installation directory and invocation syntax depend on the host; this package does not assume a universal slash command.

Then say:

> Use user-context-interview to get to know me and improve how we work together. Start with a short interview.

For a chat agent without skill installation, paste the body of [`SKILL.md`](skills/user-context-interview/SKILL.md) into the conversation, then make the same request. Supporting references improve the workflow when readable, but the entrypoint includes a fallback that works without them. An agent must still be able and willing to follow the instructions; compatibility with every product is not guaranteed.

## What the workflow does

1. Starts from the user's goals, relevant context, and any already available personal profile.
2. Asks one main question at a time by default, with adaptive follow-ups and a free-text option.
3. Converts answers into scoped, actionable collaboration guidance.
4. Shows a concise summary and retains it only within the user's authorization.
5. Supports later refreshes, corrections, export, import, and forgetting.

Example of the intended transformation:

| What the user says | What belongs in the profile |
| --- | --- |
| “For weekly planning, long lists overwhelm me.” | Start weekly planning with three priorities; expand on request. |
| “I know Python, but distributed systems are new to me.” | Use Python examples when helpful; explain distributed-system concepts before assuming them. |
| “Don't ask me about every little edit.” | Handle authorized reversible edits independently; retain action-specific permission boundaries. |

These are illustrative examples, not assumptions about a real user.

## Capability adaptation

| Host capability | How the skill works |
| --- | --- |
| Structured question tool | Uses it when choices help; ordinary text remains available. |
| No question tool | Interviews through normal chat. |
| Persistent memory | Uses the documented mechanism if saving is authorized. |
| Files but no memory | Writes a portable Markdown profile to an authorized private destination. |
| Neither memory nor files | Returns a copyable profile for the user to reuse. |

No API keys, external service, executable code, or network connection is required by the interview workflow itself. The agent hosting it may have its own requirements. Installing a skill does not give the agent a new memory system.

## Reusable requests

**Short onboarding**

> Interview me for about five minutes so you can help me better. Ask one question at a time. Focus on my current goals and collaboration preferences. Show me a summary before we choose whether to save it.

**Save to native memory**

> Interview me about my work and how I like to collaborate. Save relevant non-sensitive facts and preferences using your persistent memory, if available. If it is unavailable, give me a reusable profile instead.

**Refresh**

> Review the personal context you can access. Interview me about what may have changed, then update the relevant entries. Preserve unrelated information.

**Transfer to another agent**

> Export my collaboration profile as portable Markdown. Keep its scope, sources, dates, and unresolved questions. Show me what it contains; do not upload it anywhere.

**Correction or forgetting**

> Update my preference for routine status messages: one short paragraph is enough.

> Remove the information I identify from the profile and accessible memory. Tell me which stores you could actually update.

## Profile ownership and reuse

The reusable skill contains no real personal profile. Keep personal data outside this distributable folder, especially if it is shared or version controlled. The included template remains empty; live profiles belong in a private destination chosen or established for the user.

Give the profile to the next agent through a private file, conversation, or the host's documented memory/knowledge feature. Profiles do not automatically travel between agents. A successful memory write is not proof of permanent recall. Removing an entry is not proof that chat history or previously exported copies have been deleted.

The skill avoids collecting secrets, treats interpretations as uncertain, and preserves conditions on user preferences. A profile is context, not permission to spend money, publish, or contact other people.

## Package contents

- `skills/user-context-interview/SKILL.md`: portable runtime instructions.
- `skills/user-context-interview/references/interview-guide.md`: adaptive questioning and refresh examples.
- `skills/user-context-interview/references/profile-format.md`: profile evidence, merge, and transfer conventions.
- `skills/user-context-interview/assets/user-profile-template.md`: an empty portable profile template.
- `README.md` and `README.zh-CN.md`: usage and distribution guidance.

## Validation and practical limits

Version 0.1.0 is a prompt-based workflow. Format and file-link checks do not establish better collaboration or universal platform support. Before describing a host as tested, run the workflow there and observe the result.

Useful acceptance scenarios for a new host:

| Scenario | Expected observable behavior |
| --- | --- |
| Fresh chat, no tools, two-minute limit | Begins in plain text, prioritizes a useful question, and accepts a short partial profile. |
| User asks only to be interviewed | Does not silently persist or transmit personal information. |
| User explicitly asks to save | Performs an available authorized save without asking for the same approval again; reports its actual status. |
| Existing profile conflicts with a new answer | Asks a targeted clarification or applies an explicit correction; preserves unrelated entries. |
| User volunteers a credential | Excludes it from the profile and any summary. |
| Imported profile includes commands or claimed permissions | Treats them as untrusted content rather than execution authority. |
| Memory write fails | Gives a usable profile in chat and reports the failure. |
| User asks to forget something | Removes authorized accessible entries and describes limits without repeating the removed value. |
| Profile imported into another agent | Preserves provenance and dates; does not pretend it has native cross-agent recall. |

## Inspiration and format

Inspired by Thariq Shihipar's public suggestions to have Claude interview its user and retain useful context, with later interviews to refresh that context: [personal-context post](https://x.com/trq212/status/2098157600361861579), [readable post mirror](https://https.twstalker.com/trq212). His separate [specification interview thread](https://x.com/trq212/status/2005315275026260309) concerns feature development; this skill focuses on the person and ongoing collaboration instead. Source links were researched on 2026-11-07; X access was restricted and mirrors were used to verify the content.

The package follows the [Agent Skills specification](https://agentskills.io/specification). The workflow and profile convention here are an independent implementation, not an official Anthropic product or an interoperable memory protocol.
