# ShiftCare AI Skills

Ask your AI assistant to do your ShiftCare admin for you.

These skills teach an AI assistant — Claude, ChatGPT, Microsoft Copilot — how to
work with your ShiftCare account properly. Once they're installed, you can ask
for things in plain English:

> *"Which staff have credentials expiring in the next 30 days?"*

> *"Book Tuesday morning support for a client, 9am to 12pm, every week."*

> *"What's on today, and is anything unstaffed?"*

> *"Write up a progress note for this morning's shift."*

Without these skills, an assistant connected to ShiftCare has to guess at how
your rostering, compliance and billing actually fit together. With them, it
follows the same steps an experienced coordinator would — and always asks you
to confirm before it changes anything in your account.

## What you need

- **A ShiftCare account** with AI access switched on. An Admin does this under
  **Account → AI Settings**. Changes to your data stay off until an Admin also
  enables write actions.
- **An AI assistant that supports MCP.** We test Claude and Codex. Others, such
  as ChatGPT and Microsoft Copilot, generally work too.

## Getting started

**1. Install the skills.** In your assistant's terminal, paste:

```
npx skills add shiftcare/ai-skills
```

**2. Ask your assistant to connect you.** Say:

> *"Connect me to ShiftCare"*

One of the skills you just installed does exactly this — it asks which region
you're in, sets the connection up, sends you to a normal ShiftCare browser
login, and checks everything works before you go further.

**3. Start asking.** Try *"what's on today?"*

To pick up the latest versions later:

```
npx skills update
```

## What each skill does

**Getting set up**

| Skill | What you can ask for |
| --- | --- |
| [`shiftcare-mcp`](skills/shiftcare-mcp/SKILL.md) | "Connect me to ShiftCare" — the one you use first. Sets up the connection and checks it works. |
| [`shiftcare-basics`](skills/shiftcare-basics/SKILL.md) | Background knowledge so your assistant understands ShiftCare terms and picks the right action. |
| [`shiftcare-onboarding-check`](skills/shiftcare-onboarding-check/SKILL.md) | "Is our account set up properly?" — a scorecard of gaps, with the help article for each one. |

**Day-to-day rostering**

| Skill | What you can ask for |
| --- | --- |
| [`shiftcare-daily-rundown`](skills/shiftcare-daily-rundown/SKILL.md) | "What needs attention today?" — yesterday and today's shifts, sorted by urgency. |
| [`shiftcare-create-shift`](skills/shiftcare-create-shift/SKILL.md) | "Book a shift for..." — one-off or recurring, confirmed with you before it's saved. |
| [`shiftcare-cancel-shift`](skills/shiftcare-cancel-shift/SKILL.md) | "Cancel Thursday's shift" — including whether the client is charged and the carer paid. |

**Clients and record-keeping**

| Skill | What you can ask for |
| --- | --- |
| [`shiftcare-client-summary`](skills/shiftcare-client-summary/SKILL.md) | "Catch me up on this client" — recent shifts, upcoming schedule, note coverage, regular staff. |
| [`shiftcare-create-note`](skills/shiftcare-create-note/SKILL.md) | "Add a note about..." — files it as a client communication or a shift progress note. |

**Compliance and quality**

| Skill | What you can ask for |
| --- | --- |
| [`shiftcare-staff-compliance-check`](skills/shiftcare-staff-compliance-check/SKILL.md) | "Who's out of compliance?" — expired, expiring, missing and unverified credentials, optionally checked against an NDIS or aged-care list. |
| [`shiftcare-complaints`](skills/shiftcare-complaints/SKILL.md) | "Log a complaint about..." — lodging and managing complaints, including linked incidents. |
| [`shiftcare-action-items`](skills/shiftcare-action-items/SKILL.md) | "What should we do about this complaint?" — suggests and assigns follow-up actions. |

## Your data stays yours

- Your assistant signs in to ShiftCare the same way you do, in a browser. There
  are no keys or passwords to copy around.
- It only sees what your ShiftCare role lets you see.
- Everything is read-only until an Admin turns on write actions — and even then,
  any skill that changes your data asks you to confirm first.
- The installer is Vercel's open-source `skills` CLI, which sends anonymous
  install counts. Set `DISABLE_TELEMETRY=1` to switch that off.

## More help

If the connection gives you trouble, or you'd like to follow the setup yourself
rather than have your assistant do it:

- [Introduction to the ShiftCare MCP Server](https://help.shiftcare.com/en/articles/14649246-introduction-to-the-shiftcare-mcp-server)
- Step-by-step setup for
  [Claude](https://help.shiftcare.com/en/articles/14612387-connecting-shiftcare-mcp-to-claude),
  [ChatGPT](https://help.shiftcare.com/en/articles/14630405-connecting-shiftcare-mcp-to-chatgpt)
  or [Microsoft Copilot](https://help.shiftcare.com/en/articles/15188287-connecting-shiftcare-mcp-to-microsoft-copilot)

## For developers

Run the static skill checks:

```
uv run --with skills-ref==0.1.1 scripts/validate_skills.py
```

[`public_ai_skills.yml`](public_ai_skills.yml) publishes the minimum and latest
supported version of each skill. Validation fails if it drifts from the versions
in the skill frontmatter. Contributor rules are in [AGENTS.md](AGENTS.md).

## License

Apache-2.0. See [LICENSE](LICENSE).
