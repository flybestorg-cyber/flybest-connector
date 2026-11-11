# 2026-11-11 Skill 1.1.21: wording the directory's check reads as a password-manager command

- Record ID: 2026-11-11-directory-hold-wording-1-1-21
- Date and time zone: 2026-11-11, America/Los_Angeles
- Related records: [2026-11-05-family-adults-fallback-1-1-15](2026-11-05-family-adults-fallback-1-1-15.md) (first note of the hold), [2026-11-05-signin-connect-hint-1-1-17](2026-11-05-signin-connect-hint-1-1-17.md) (ticket to the directory team), [2026-11-10-trip-list-scope-1-1-20](2026-11-10-trip-list-scope-1-1-20.md) (1.1.20 held), [2026-11-02-privacy-policy-url](2026-11-02-privacy-policy-url.md) (an earlier finding caused by wording in a record).
- Affected files: the skill file (nine sentences), the root maintenance instructions (one sentence reworded, one rule added), the change log and ten earlier records (one verb each), the 1.1.15 record (a rule name no longer in code formatting), the Claude manifest and the LobeHub manifest (1.1.20 → 1.1.21).

## Problem and cause

Since 2026-11-05 the Claude directory has held every new version (1.1.15 to 1.1.20) for a reviewer, under "Uses a credential from the user's machine" and "Update adds credential forward", both anchored on the Claude manifest. The directory keeps serving 1.1.14 from 2026-11-02. The manifest declares one remote MCP address and nothing else, and it has not changed since 1.1.14 apart from the version. The ticket sent to the directory team on 2026-11-06 has had no answer from a person.

What was established on 2026-11-11, from the directory's own documentation and from other publishers' public reports:

- The finding comes from a static check over every text file in the plugin folder. For this repository that is the whole repository, maintenance records included. It pairs "a part that reads a credential" with "a part that sends data". Here the sending part is the MCP address in the manifest, which is why the manifest is the file named. The portal does not quote the line it read as a credential.
- One publisher obtained the raw output for the same rule (altertable-ai/skills, pull request 118, 2026-11-04). The reading part was a skill sentence in which the verb p-a-s-s is followed by a parameter name in code formatting. The check read it as the Unix password manager of the same name fetching a secret. Their sentence was older than the hold: the check became stricter around 2026-11-03, the same days on which this plugin's long-standing credential warning turned into a hold.
- This skill has carried the same shape since 2026-09-28 (the sentence about the children fields) and 2026-10-14 (the sentence about the e-mail field). Versions 1.1.15 to 1.1.20 added five more sentences with that verb.
- The directory's documentation says a held version waits for an Anthropic reviewer, and that the author should do nothing unless the cause can be removed. A public bug report (anthropics/claude-code issue 103979, open since 2026-10-21) says a held version that arrives by push is not routed to a reviewer at all. Waiting may therefore never end.

This is the likely cause, not a proven one for this plugin. The portal's own Validate, which shows the result for any branch without submitting it, could not be run when this change was made.

## Change and reason

- Every sentence that used the verb is reworded with "relay", "hand", "include", "use", "set", "say" or "search with". The instruction in each sentence is the same as before.
- The same verb is replaced in the change log and in ten earlier records, because the check reads those files too. No fact in them changes. In the 1.1.15 record the rule name is no longer in code formatting.
- The root maintenance instructions gain one rule: keep that verb out of every file here, and run the portal's Validate on the branch before a change to the skill, the README or a record is merged.
- The two tool parameter names that contain the words "key" and "token" stay as they are. They are the service's own parameter names and the skill has to name them. If the hold remains, they are the next thing to test.
- Version 1.1.21, so that installed copies see an update.

## Customer experience and compatibility

No behaviour change: the skill gives the same instructions in other words. The remote service is untouched. The ChatGPT package is a separate upload that this check does not read, and it is not resubmitted.

## Verification

- `claude plugin validate .` reports nothing (Claude Code current on 2026-11-11).
- A whole-word search for the verb over every tracked file finds nothing.
- The reworded sentences were read against the previous ones, one by one.
- Not verified: the directory's result for this version. Receipt to be appended.

## Release status

- Commit: see this record's Git commit. Pushed to GitHub `main` on 2026-11-11 (evening, Los Angeles).
- Claude directory: receipt to be appended once the portal can be read.
- No service restart or backend deployment.

## Remaining limits and next steps

- If 1.1.21 is still held, the cause is another line. The way to find it is the portal's Validate on probe branches (developer portal → Submit new → Plugin bundle → Source → repository and branch → Validate; nothing is submitted), removing one file or one section at a time until the report shows no "Policy hold".
- The documented channel for a plugin that is stuck is the plugin's menu in the portal, "Get help" or "Contact Anthropic". The documentation says e-mail to the directory team can be delayed. That channel has not been used yet.
- Nothing in this repository can run the directory's check, so the rule above depends on whoever makes the next change.
