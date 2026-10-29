<script lang="ts">
 import reports from '#lib/data/reports-4471.json';
 import notes from '#lib/data/desk-notes.json';
 import { uniqueById, groupByCause, readAs, type Report } from '#lib/kb/causes';
 import { tenantOf } from '#lib/kb/locales';
 const unique = uniqueById(reports as Report[]);
 const merged = unique.filter(r => r.mergedInto === 4471);
 const groups = groupByCause(merged, tenantOf);
 const mismatches = groups.reduce((n,g) => n + Object.entries(g.taggedAs).reduce((s,[tag,count])=>s+(tag===g.cause?0:count),0),0);
</script>
<p>{reports.length} exported rows → {unique.length} unique report IDs → {merged.length} reports merged into #4471. {reports.length-unique.length} repeated export rows are counted once. Intake tags disagree with tenant-based classification for {mismatches} reports.</p>
<table><thead><tr><th>Problem</th><th>Unique reports</th><th>Tenants</th><th>Received</th><th>Qualification</th></tr></thead><tbody>
{#each groups as g}<tr><td>{g.cause}</td><td>{g.reports.length}</td><td>{g.tenants}</td><td>{g.firstSeen} → {g.lastSeen}</td><td>{readAs(g,notes.oneDayMove)} reports flagged by the desk as one-day moves</td></tr>{/each}
</tbody></table>
