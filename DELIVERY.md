# S01E03 delivery

This repository contains the supplied support-kb export plus an investigation, a proposed replacement decision, and a real static build.

- Investigation source: `src/routes/kb/incidents/4471-review/+page.svx`
- Rendered page: `build/kb/incidents/4471-review.html`
- Signed desk reference: DR-QDX7-TKMA
- Proposed decision: `src/routes/kb/decisions/0002-dedupe-by-cause/+page.svx`
- Preserved original accepted decision: `src/routes/kb/decisions/0001-dedupe-by-subject/+page.svx`

## Reproduce

Use Node 24 or a supported Node 22 release, then `npm ci` and `npm run build`. Run `npm run preview` and open `/kb/incidents/4471-review`.

The data is the supplied export dated 4 October 2026; the investigation was prepared on 29 October. It does not claim to measure current support intake.

## Findings

427 exported rows collapse to 412 unique report IDs. The supplied causeOf function, after a tenant join and platform-derived date ordering, assigns 379 to parser and 33 to hint. Intake tags disagree for 38 reports. Five one-day-move reports remain in the parser classification but have unresolved symptoms. The received/merged timeline distinguishes April onset from the July bulk merge.

The owner approved publication. Two issue drafts and their report-ID coverage are in issue-drafts/.
