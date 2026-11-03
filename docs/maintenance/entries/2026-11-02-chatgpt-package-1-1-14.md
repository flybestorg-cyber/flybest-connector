# 2026-11-02 ChatGPT plugin package 1.1.14 (sign-in reminder) published

- Record ID: 2026-11-02-chatgpt-package-1-1-14
- Date and time zone: 2026-11-02, America/Los_Angeles
- Related records:
  - [2026-11-02-signin-reminder-1-1-14](2026-11-02-signin-reminder-1-1-14.md): the Claude plugin skill this package carries.
  - [2026-10-26-chatgpt-package-1-1-11](2026-10-26-chatgpt-package-1-1-11.md): how the ChatGPT package is built.
  - The 1.1.12 ChatGPT package was published on 2026-10-27.
- Affected files in this repository: this record and the change log only. The ChatGPT package itself is not kept here.

## Problem and cause

The published ChatGPT package (1.1.12) carried the 1.1.12 skill. It did not have the 1.1.14 rule: while the FlyBest tools are not in the conversation, every hotel or travel reply starts with a reminder to connect and sign in, and gives no hotel prices before sign-in.

In ChatGPT, connecting usually happens at install time. However, OpenAI documents that an installed plugin can still have its app disconnected or unauthorized. Such users never reach our server, so the server cannot remind them; only the bundled skill can.

## Change and reason

The package is the published 1.1.12 package with three edits:
- `skills/flybest-hotels/SKILL.md` replaced with this repository's 1.1.14 skill;
- `.codex-plugin/plugin.json` version set to 1.1.14;
- three lines in the skill adapted for ChatGPT:
  - the example reminder says "in ChatGPT open Settings → Apps, choose FlyBest, click Connect and enter the code we e-mail you; if it already says connected, make sure FlyBest is turned on for this chat", instead of the Claude and Claude Code steps;
  - the comment explaining the rule says the sign-in is a separate step after installing, instead of naming Claude apps;
  - the existing client-neutral edit is kept ("complete the current client's sign-in").

Everything else matches the repository skill: the references, listing text, URLs, icon and the MCP configuration are unchanged. There are no tool or server changes.

## Version and release status

- 2026-11-02 about 23:50 PST: uploaded with "Create draft from ZIP". Metadata and skill checks passed with no findings.
- On the owner's 「确认」 it was submitted for review, with the six standard attestations ticked and a short note for the reviewers. It was approved at once ("Ready to publish").
- On the owner's 「发布」 it was published (Publish plugin → Publish Version). The portal shows "Publication: Version 1.1.14" and "1.1.14 · Published", replacing 1.1.12.

## Remaining limits

- Not tested inside ChatGPT with a disconnected app. The same rule was tested in a clean Claude Code install (hotel questions get the reminder and no prices, a coding question gets none).
- Whether ChatGPT loads a plugin's skills while its app is disconnected is not documented. If it does not, the reminder never shows there and nothing is lost.
