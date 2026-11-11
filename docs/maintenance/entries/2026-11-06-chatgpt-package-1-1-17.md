# 2026-11-06 ChatGPT plugin package 1.1.17

- Record ID: 2026-11-06-chatgpt-package-1-1-17
- Date and time zone: 2026-11-06, America/Los_Angeles
- Related records: [2026-11-02-chatgpt-package-1-1-14](2026-11-02-chatgpt-package-1-1-14.md) (how the package is built), [2026-11-05-family-adults-fallback-1-1-15](2026-11-05-family-adults-fallback-1-1-15.md), [2026-11-05-chat-signin-1-1-16](2026-11-05-chat-signin-1-1-16.md), [2026-11-05-signin-connect-hint-1-1-17](2026-11-05-signin-connect-hint-1-1-17.md).
- Affected files in this repository: this record and the change log only. The ChatGPT package itself is not kept here.

## Change

The published 1.1.14 package with:
- `skills/flybest-hotels/SKILL.md` replaced with this repository's 1.1.17 skill (family adults' prices, sign-in link in a tool result, two sets of tools);
- `.codex-plugin/plugin.json` version 1.1.17;
- the three 1.1.14 ChatGPT edits kept (Settings → Apps → Connect reminder, neutral comment, "the current client's sign-in");
- the sign-in-link bullets written without Claude's settings: in apps such as Codex a tool can return a one-time link; relay it, call again after sign-in, a new chat signs in with its own link; with two sets of FlyBest tools use the signed-in one. The skill contains no Claude-specific step.

References, listing text, URLs, icon and MCP configuration are unchanged. No tool or server change: the server behaviour (family fallback, chat sign-in) is already live for every client.

## Release status

- 2026-11-06: package built (`app-…-1.1.17.zip`, same file list as 1.1.14). The owner said 「发布」 at about 02:30 PST.
- Uploaded with "Create draft from ZIP" (the dialog's file input, no system picker). Metadata: no findings; skill checks passed after about five minutes.
- Submitted for review with a private note to the reviewers (skill text only; metadata, icon, URLs and MCP configuration unchanged). Three of the six standard attestations were ticked by the assistant; ticking the rest was refused by the assistant's permission check, so the owner ticked them and submitted.
- About 03:00 PST the portal shows "Publication: Version 1.1.17", "1.1.17 · Published" and "Listed publicly", replacing 1.1.14.
