# 2026-11-10 ChatGPT plugin package 1.1.20

- Record ID: 2026-11-10-chatgpt-package-1-1-20
- Date and time zone: 2026-11-10, America/Los_Angeles
- Related records: [2026-11-06-chatgpt-package-1-1-17](2026-11-06-chatgpt-package-1-1-17.md) (the previous package and how it differs from the Claude skill), [2026-11-06-skill-essentials-1-1-18](2026-11-06-skill-essentials-1-1-18.md), [2026-11-09-chat-link-email-1-1-19](2026-11-09-chat-link-email-1-1-19.md), [2026-11-10-trip-list-scope-1-1-20](2026-11-10-trip-list-scope-1-1-20.md).
- Affected files in this repository: this record and the change log only. The ChatGPT package itself is not kept here.

## Change

The owner asked for both packages to be brought to 1.1.20. The published 1.1.17 ChatGPT package with:
- `skills/flybest-hotels/SKILL.md` replaced with this repository's 1.1.20 skill: the Essentials section first (1.1.18), the confirmation e-mail asked once in a chat signed in by link (1.1.19), the trip list covering the current sign-in (1.1.20);
- `.codex-plugin/plugin.json` version 1.1.20;
- the 1.1.17 ChatGPT edits kept unchanged (Settings → Apps → Connect reminder, neutral comment, sign-in link written for apps such as Codex, "the current client's sign-in");
- two more neutral wordings for text added since 1.1.17: the Essentials comment says "some apps" keep only the first part of a skill, and the confirmation bullet says "connected in the app's settings". The skill contains no Claude-specific step.

References, listing text, URLs, icon and MCP configuration are unchanged (same file list as 1.1.17). No tool or server change.

## Release status

- 2026-11-10: package built (`app-…-1.1.20.zip`) and uploaded with "Create draft from ZIP". Metadata: no findings.
- Skill checks passed after about four minutes ("No findings with the plugin's metadata and skills"). The draft 1.1.20 is in the portal, not submitted: submitting needs the six standard attestations, which are the owner's to confirm.
- Seen in the portal the same day, unrelated to this package: the MCPs tab shows "Needs attention". OpenAI's automatic check of the live server's instructions (reviewed 2026-11-09 21:02 portal time) reports "appear to compare the plugin with alternatives, disparage them, or instruct the model to prefer this plugin" on the unpublished update, so ChatGPT keeps serving the earlier instructions and the earlier `sabre_hotel_search` definition; the other seven tools are published. The update that is held is the one that added the "Core rules" block (service release of 2026-11-06). Service-side follow-up is recorded in sabre-booking's pending list.

