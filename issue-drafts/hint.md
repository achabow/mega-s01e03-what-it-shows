# booking-v3 date hint conflicts with day-first locale parsing — 33 reports from #4471

## Problem
For form submissions from day-first booking-v3 tenants, the hint says MM/DD/YYYY while the form reads dates in the tenant convention. The shared-parser fix does not repair the misleading hint. Affected tenants: alder.physio, copper.studio, pale.harbour.

## Coverage
33 unique report IDs merged into #4471 across 3 tenants. Received 2026-04-17 through 2026-09-22. This is the supplied 4 October export, not a live count.

## Method
Deduplicate the export by report ID, filter mergedInto === 4471, join tenant records, determine locale order with Intl.DateTimeFormat.formatToParts, then run causeOf(channel, tenant). Do not group by subject, browser locale, or intakeTag. Across both issues: 427 raw rows, 412 unique reports, 379 parser + 33 hint = 412; no report belongs to both.

## Expected fix and verification
Make booking-v3 date hints and parsing use the same explicit tenant format. Test all three affected tenants with ambiguous dates and verify the submitted date equals the date promised by the hint.

## Evidence
The reproducible kb page is src/routes/kb/incidents/4471-review/+page.svx; its rendered output is build/kb/incidents/4471-review.html. Counts are computed from src/lib/data and the supplied causeOf logic. The page carries the author's signature and RenderStamp desk reference.

## Covered report IDs
R-41230, R-41241, R-41251, R-41259, R-41262, R-41275, R-41294, R-41305, R-41308, R-41366, R-41372, R-41384, R-41387, R-41396, R-41400, R-41406, R-41415, R-41416, R-41418, R-41428, R-41439, R-41441, R-41449, R-41453, R-41456, R-41460, R-41472, R-41485, R-41493, R-41539, R-41572, R-41582, R-41584
