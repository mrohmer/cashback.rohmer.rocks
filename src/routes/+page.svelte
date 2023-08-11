<script lang="ts">
  import Calculator from "$lib/components/Calculator.svelte";

  import type { Snapshot } from './$types';

  let value: number|undefined = 0;
  let unit = '€';
  let vat = 19;
  let cashbackRate: number|undefined = 0;

  export const snapshot: Snapshot = {
    capture: () => ({value, unit, vat, cashbackRate}),
    restore: (v) => {
      value = v?.value ?? undefined;
      unit = v?.unit ?? '€';
      vat = v?.vat ?? 19;
      cashbackRate = v?.cashbackRate ?? undefined;
    },
  };

  const reset = () => {
    value = undefined;
    unit = '€';
    vat = 19;
    cashbackRate = undefined;
    window.scrollTo(0, 0);
  }
</script>

<svelte:head>
    <title>Cashback | Matthias Rohmer</title>
    <meta name="description" content="Calc Cashback." />
    <meta name="theme-color" content="#000000" />
    <link rel="manifest" href="/manifest.json" />
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="apple-mobile-web-app-title" content="Cashback" />
    <meta name="apple-mobile-web-app-status-bar-style" content="black" />
</svelte:head>

<Calculator bind:value bind:unit bind:vat bind:cashbackRate />

<div class="flex justify-center py-4 rounded-xl">
    <button class="btn btn-ghost" on:click={reset}>
        reset
    </button>

</div>
