<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import notes from '#lib/data/desk-notes.json';
  import { causeOf, uniqueById, type Report } from '#lib/kb/causes';
  import { tenantOf } from '#lib/kb/locales';

  let { ticket }: { ticket: number } = $props();

  const merged = $derived(uniqueById(reports as Report[]).filter((r) => r.mergedInto === ticket));
  // The desk sets the one-day reports aside (desk-notes.json) but still files them under their tenant's cause.
  const problems = $derived.by(() => {
    const shift = merged.filter((r) => notes.oneDayMove.includes(r.id));
    const rest = merged.filter((r) => !notes.oneDayMove.includes(r.id));
    const by = (c: string) => rest.filter((r) => (causeOf(r, tenantOf(r)) ?? 'unplaced') === c);
    return [
      { name: 'parser', what: 'shared parser reads day-first dates month first', n: by('parser').length },
      { name: 'hint', what: 'booking-v3 form hint says MM/DD/YYYY', n: by('hint').length },
      { name: 'one-day shift', what: 'date one day off, not a swap (cause not confirmed)', n: shift.length },
      { name: 'unplaced', what: 'no day-first tenant on file', n: by('unplaced').length },
    ].filter((p) => p.n > 0);
  });
</script>

<p class="sum">
  <strong>{merged.length}</strong> reports in #{ticket} · <strong>{problems.length}</strong> problems
</p>

<table>
  <thead><tr><th>problem</th><th>reports</th><th>what it is</th></tr></thead>
  <tbody>
    {#each problems as p (p.name)}
      <tr><td><code>{p.name}</code></td><td>{p.n}</td><td>{p.what}</td></tr>
    {/each}
  </tbody>
</table>

<style>
  .sum { font-size: 1.1rem; }
</style>
