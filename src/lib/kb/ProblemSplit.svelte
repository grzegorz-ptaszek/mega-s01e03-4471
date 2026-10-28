<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import notes from '#lib/data/desk-notes.json';
  import { causeOf, uniqueById, type Report } from '#lib/kb/causes';
  import { tenantOf } from '#lib/kb/locales';

  let { ticket }: { ticket: number } = $props();

  const merged = $derived(uniqueById(reports as Report[]).filter((r) => r.mergedInto === ticket));
  const by = (c: string) => merged.filter((r) => (causeOf(r, tenantOf(r)) ?? 'unplaced') === c);
  // Counted where the desk files them: by the tenant's cause. The one-day reports are footnoted, not split off.
  const oneDay = $derived(merged.filter((r) => notes.oneDayMove.includes(r.id)).length);
  const problems = $derived(
    [
      { name: 'parser', what: 'shared parser reads day-first dates month first', n: by('parser').length },
      { name: 'hint', what: 'booking-v3 form hint says MM/DD/YYYY', n: by('hint').length },
      { name: 'unplaced', what: 'no day-first tenant on file', n: by('unplaced').length },
    ].filter((p) => p.n > 0),
  );
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

{#if oneDay}
  <p class="note">{oneDay} of the <code>parser</code> reports read as a one-day move, not a month/day swap. The desk counts them with the parser.</p>
{/if}

<style>
  .sum { font-size: 1.1rem; }
  .note { color: var(--muted); font-size: 0.85em; }
</style>
