# 2026-10-07 Priced hotel recommendations and booking conversion (1.1.6)

- Record ID: 2026-10-07-hotel-skills-conversion
- Date: 2026-10-07, America/Los_Angeles
- Consulted: maintenance index/log, CONTRIBUTING, [public contract alignment](2026-10-04-public-docs-live-contract.md) and [release baseline](2026-10-02-release-baseline.md).
- Scope: public hotel skill, its quote-integrity reference, plugin manifests and copy-instructions in README. Related server work is recorded under the same record ID in the maintained server repository.

## Problem and cause

Hotel-interest answers could end at a property list and another request to check prices. The instruction to limit searches could be interpreted as prohibiting the formal rates calls needed for a priced shortlist. Optional preference and membership questions could also stall a quote when the dates and party were already known.

## Change and reason

A city or property enquiry with dates and party now proceeds to authoritative rates and the selected partner row's benefits in the same answer, ending in a concrete hotel/rate choice and secure-payment-page action. Missing dates and party are collected together. Optional preferences can accompany quotes, and members-only options retain verification before booking.

The linked reference covers matched room/party comparisons, actual quote currency, excluded or unknown fees, hotel-local deadlines, incomplete results, targeted suite recovery and selected-row continuity. Confirmation checks distinguish requested arrangements from supplier-confirmed ones. Multi-room cancellation limitations are explained before booking.

The approved separate benefit-estimate policy remains: no deduction from prices or valuation of availability-dependent perks. Public access remains eight hotel tools. No owner tools, internal identities or commission figures are added. Existing payment consent, family-token and unknown-outcome protections remain.

## Verification

Skill frontmatter and reference links checked; plugin manifests validated; matched versions are 1.1.6. Existing mocked public contract and advice tests are run with network disabled in an isolated harness, including cross-repository manifest checks. Final counts and any limitations are appended after completion. No live search, booking, payment, cancellation or email is performed.

## Version and release status

This is a candidate branch; publication details are recorded by its commit/PR. No backend deployment or service restart is performed by this change. Installed clients require the updated skill; connector-only clients receive new initialization guidance only after the related server change is deployed and their client reloads it.

## Limits and rollback

Instructions guide the assistant but do not prove conversion lift. No production conversion experiment is claimed. Restore the previous skill/manifests to roll back this document change. Runtime continuation and authorization gates remain server responsibilities.

## Completed validation — 2026-10-07 PDT

Five skill entrypoints passed frontmatter validation; public marketplace and the private owner manifest passed Claude validation. Explicit public manifest validation on the installed Claude Code 2.1.72 found pre-existing unsupported displayName/privacyPolicyUrl keys; the unchanged baseline failed identically. These keys were removed from the Claude manifest; display name remains in lhm.plugin.json and the privacy link remains in README. Final direct manifest validation is recorded below. All reference links resolve, the shared quote reference is identical, and both public manifest versions are 1.1.6. The isolated existing public advice/contract suite passed **88 tests**, including the actual adjacent public checkout. Initial harness lacked python-multipart and the repository’s existing synthetic card-link stand-in; after installing the form dependency and reproducing that fixture, all cases passed. No network, database, real booking or payment was used. Changed-source syntax, diff whitespace and the repository PII scanner passed. This does not claim model end-to-end behaviour or production conversion results.

Final direct public/owner plugin and marketplace validations passed on Claude Code 2.1.72; after the compatibility correction, the 88 contract cases passed again. The candidate changes have not been merged or deployed.
