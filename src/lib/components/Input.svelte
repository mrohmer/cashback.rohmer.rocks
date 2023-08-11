<script lang="ts">
  export let name = `input-${(Math.random() * 1000000)}`;

  export let value: number | string;
  export let placeholder: string | undefined;
  export let max: number | string | undefined;
  export let unit: string | undefined = undefined;

  export let disabled = false;

  let klass: string;

  export {klass as class};
</script>

<style>
    /* Chrome, Safari, Edge, Opera */
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }

    /* Firefox */
    input[type=number] {
        -moz-appearance: textfield;
    }
</style>

<div class="text-right w-full {klass}">
    {#if $$slots.default}
        <label for={name} class="opacity-70 text-xs -mb-1 block">
            <slot/>
        </label>
    {/if}
    <div class="text-5xl flex items-center">
        <div class="flex-1">
            <input type="number"
                   class="w-full text-right !bg-transparent pr-2 !outline-none"
                   id={name}
                   {name}
                   bind:value
                   {disabled}
                   min="0"
                   {max}
                   {placeholder}
            />
        </div>
        {#if unit}
            <div class="w-10 text-center">
                {unit}
            </div>
        {/if}
    </div>
</div>
