# 2026-10-08 Customer-facing hotel Skill refresh (1.1.7)

- Record ID: 2026-10-08-public-hotel-skill-refresh
- Date and timezone: 2026-10-08, America/Los_Angeles
- Consulted: maintenance index/log, CONTRIBUTING, [priced recommendations](2026-10-07-hotel-skills-conversion.md) and [public contract alignment](2026-10-04-public-docs-live-contract.md).
- Scope: public hotel Skill, quote-integrity reference, README and plugin manifests. Current advisor hotel search/booking playbooks were compared for customer-useful guidance; operational-only instructions were excluded.

## Problem and cause

The public Skill already supports formal quotes and booking continuation, but did not fully distinguish unchecked benefits from failed benefits lookups. The current service checks a bounded shortlist, so a selected negotiated row can need a targeted follow-up. Payment-page expiry, booking confirmation and payment/refund evidence also need distinct handling. The README still led with the connector directory, said the plugin was not listed, and promised loyalty credit too broadly.

## Change and reason

Version 1.1.7 adds targeted benefits recovery, comparison of all returned priced options, reuse of the chosen quote and supplied details, and precise confirmation checks. Facilities-only questions use property content without unnecessarily requiring stay dates. Unknown payment-page outcomes are verified through the public booking reads or advisor; the Skill does not invent access to a live payment-status tool. Expired unused pages can continue through a current matching quote, while a submitted attempt must be confirmed closed before replacement.

Trip identifiers come from the current own-bookings list. Hotel confirmation, card guarantee, captured payment and received refund are reported separately. Unsupported date changes, post-booking loyalty updates and special requests have an actionable advisor handoff, without automatic cancellation/rebooking or a false claim that a draft was sent.

The README now promotes the published Claude plugin entry and explains bundled Skills, the remote MCP connection and separate email authorization. Customer contact uses the current returned advisor address, with jay@flybest.org as fallback. Loyalty credit and status benefits depend on the selected rate and programme rules.

Existing selected-row pricing, actual currency, payment consent, family occupancy/token verification, cancellation preview/consent and unknown-outcome protections remain. The approved separate benefits-estimate policy remains. Public access is still the same eight hotel tools; no flight, saved-card booking, CRM, commission or advisor-only servicing tools are introduced.

## Verification

- Skill frontmatter validator passed.
- Claude Code 2.1.72 validated the plugin and marketplace manifests successfully.
- Both plugin versions are 1.1.7; the MCP endpoint and Skill directory remain unchanged.
- Structural checks passed for all Skill reference links, exactly eight public hotel tool names, current customer contact, and absence of operational-only tool names or private filesystem paths in changed customer files.
- Reviewed continuation paths: selected quote to payment page, unchecked benefits to targeted lookup, ambiguous trip to clarification, and submitted/unknown payment attempt to verification rather than duplicate booking.
- Diff whitespace checks passed. No live hotel search, booking, payment, cancellation or email was performed. These checks validate instructions and packaging, not model end-to-end behaviour or conversion results.

## Version and publication status

At the time of this record, the candidate is local and not yet pushed. The associated commit is the Git commit containing this record. A publication receipt will be appended after remote verification.

This changes plugin source and documentation only. No backend code is changed, no service is restarted, and no new backend deployment is claimed. Existing plugin installations need the updated Skill; directory refresh and installed-client uptake are separate from publishing repository source.

## Remaining limits and rollback

The public tools cannot inspect a payment page's live processing status or perform unsupported hotel servicing. The advisor remains the verification path for those cases. No directory reindex or installed-Claude update has been verified by these local checks. Restore the previous Skill, reference, README and plugin manifests to roll back.

## Publication receipt — 2026-10-08 16:08 PDT

This later receipt supersedes the local candidate status above. Source commit `b82e02b81ec2da50432f52dc5b17f4a6babb6fe6` was successfully pushed to [GitHub main](https://github.com/flybestorg-cyber/flybest-connector/commit/b82e02b81ec2da50432f52dc5b17f4a6babb6fe6), and a remote ref read at 23:08:30 UTC confirmed that exact commit. The published source manifests declare plugin version 1.1.7.

Claude Code 2.1.293 also validated the plugin and marketplace. Its plugin check reported only the expected warning that root CLAUDE.md is maintainer context rather than shipped Skill context; the customer instructions are in skills/flybest-hotels/SKILL.md. No backend deployment or service restart occurred. Repository publication does not establish that the Claude directory or an existing installation has ingested version 1.1.7; that needs a separate refresh check.
