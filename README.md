# ShiftCare AI Skills

Ask your AI assistant to do your ShiftCare admin for you.

[ShiftCare](https://www.shiftcare.com) is care management software for
disability, aged care and home care providers, operating in Australia, the
United Kingdom, the United States and Canada. It covers rostering, care
delivery, documentation, compliance and billing on one record.

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
  **Account → AI Settings → AI Access → "MCP - External AI Model Access"**.
- **Permission to connect.** Admins can straight away. If you're a Coordinator,
  HR, Ops or Support user, an Admin also has to turn on **Allow Back Office
  Access** — without it the login will simply reject you. Support workers can't
  connect at all.
- **Write access, if you want it.** **Allow Write Actions** is a separate
  toggle, off until an Admin enables it. Writing is admin-only: a back-office
  role can never write through an assistant, whatever that toggle says.
- **An AI assistant that supports both MCP and skills.** We test Claude and
  Codex. Others, such as ChatGPT and Microsoft Copilot, generally work too.

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
| [`shiftcare-client-summary`](skills/shiftcare-client-summary/SKILL.md) | "Catch me up on this client" — shifts over a recent window you choose, the service pattern they show, progress-note coverage, and who was rostered most in that window. |
| [`shiftcare-create-note`](skills/shiftcare-create-note/SKILL.md) | "Add a note about..." — files it as a client communication or a shift progress note. |

**Compliance and quality**

These report what your records show, and what an advisory checklist suggests
reviewing. Whether you are compliant is a determination you and your regulator
make — no skill here makes it for you.

| Skill | What you can ask for |
| --- | --- |
| [`shiftcare-staff-compliance-check`](skills/shiftcare-staff-compliance-check/SKILL.md) | "Which credentials need attention?" — expired, expiring, missing and unverified records, optionally matched against an advisory NDIS or aged-care checklist. |
| [`shiftcare-complaints`](skills/shiftcare-complaints/SKILL.md) | "Log a complaint about..." — lodging, triaging and progressing complaints, and flagging when something needs your incident or escalation process instead. |
| [`shiftcare-action-items`](skills/shiftcare-action-items/SKILL.md) | "What should we do about this complaint?" — suggests and assigns follow-up actions. |

## Who can see what

**What ShiftCare controls:**

- Your assistant signs in to ShiftCare the same way you do, in a browser. There
  are no keys or passwords to copy around.
- It only sees what your own ShiftCare role lets you see — never more.
- Everything is read-only until an Admin turns on write actions, and even then
  any skill that changes your data asks you to confirm first. Back-office roles
  are read-only regardless.

**What your organisation is responsible for:**

- **Your care data leaves ShiftCare when you ask for it.** Client records,
  including personal and health information, travel to whichever AI assistant
  you connected, and are handled under that provider's terms. ShiftCare cannot
  see those conversations.
- Meeting your own obligations — NDIS, aged care, privacy law — for the data
  once it arrives there.

Worth reading before you start:
[Connecting an AI Assistant to Your Care Data](https://shiftcare.com/blog/connecting-ai-assistant-your-care-data),
on what an assistant can see, what it can't, and who is responsible, and the
[MCP data handling overview](https://help.shiftcare.com/en/articles/15652546-shiftcare-mcp-server-data-handling-overview).

The installer is Vercel's open-source `skills` CLI, which sends anonymous
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
in the skill frontmatter. Contributor rules are in [AGENTS.md](AGENTS.md),
and the security policy is in [SECURITY.md](SECURITY.md).

## License

Apache-2.0. See [LICENSE](LICENSE).
