<script lang="ts">
    export let label: string = '';
    export let value: string;
</script>

<div>
    {#if label}
        <label class="block text-sm font-medium text-gray-700 mb-1" for="">
            {label}
        </label>
    {/if}

    <div class="flex items-center gap-2">
        <input
            type="color"
            bind:value
            class="mt-1 mb-1 block py-1 px-2 rounded-md border-0 text-gray-900 ring-1 ring-inset bg-gray-50 ring-gray-300 focus:ring-2 focus:ring-indigo-600 sm:text-sm sm:leading-6">

        <p class="text-xs font-medium">
            {value}
        </p>
    </div>
</div>

<!---
<div>
    <label for="series-color" class="block text-sm font-medium leading-6 text-gray-900">
        Color of the series
    </label>
    <input
        type="color"
        id="series-color"
        class="mt-1 block py-1 px-2 rounded-md border-0 text-gray-900 ring-1 ring-inset bg-gray-100 ring-gray-300 focus:ring-2 focus:ring-indigo-600 sm:text-sm sm:leading-6"
        bind:value={seriesColor}>
</div>
-->