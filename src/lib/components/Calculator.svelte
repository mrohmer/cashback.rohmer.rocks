<script lang="ts">
    import Input from './Input.svelte';

    export let value: number|undefined;
    export let unit: string;
    export let vat: number;
    export let cashbackRate: number|undefined;

    const getSafeFloat = (nbr: number) => {
      if (typeof nbr !== 'number') {
        return 0;
      }
      if (isNaN(nbr)) {
        return 0;
      }
      return nbr;
    }

    const doTheCalc = (value: number, vat: number, cashbackRate: number) => {
      if (value === 0 || cashbackRate === 0) {
        return undefined;
      }
      const cashback = +(value * (1 - vat / 100) * (cashbackRate / 100)).toFixed(2);
      return {
        cashback,
        result: value - cashback,
      }
    }

    $: safeValue = getSafeFloat(value);
    $: safeVat = getSafeFloat(vat);
    $: safeCashbackRate = getSafeFloat(cashbackRate);
    $: result = doTheCalc(safeValue, safeVat, safeCashbackRate);
</script>

<div class="min-h-[100svh] flex flex-col items-center justify-center gap-4 max-w-xs mx-auto">
    <Input name="price" bind:value {unit} class="px-2" placeholder="0">
        Preis
    </Input>
    <Input name="cashback-rate" bind:value={cashbackRate} unit="%" class="px-2" placeholder="0">
        Cashback Rate
    </Input>
    <Input name="vat" bind:value={vat} unit="%" class="px-2" max="99" placeholder="0">
        Steuer
    </Input>

    <div class="h-px w-full bg-white"></div>

    <div class="px-2" class:opacity-50={!result}>
        <Input name="resul-cashback" value={(result?.cashback ?? 0).toFixed(2)} {unit} disabled class="px-2">
            Cashback
        </Input>
    </div>
    <div class="px-2" class:opacity-50={!result}>
        <Input name="result-total" value={(result?.result ?? 0).toFixed(2)} {unit} disabled class="px-2">
            Gesammtpreis
        </Input>
    </div>
</div>
