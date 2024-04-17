<script lang="ts">
    export let label: string = '';
    export let placeholder: string = '';
    export let options: { value: string; label: string }[] = [];
    export let value: string;
</script>

<div>
    {#if label}
        <label class="block text-sm font-medium text-gray-700 mb-1" for="">
            {label}
        </label>
    {/if}
    <select
        placeholder={placeholder}
        bind:value
        class="block w-full rounded-md border-0 px-3 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300
            placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6;">
        {#each options as { value, label }}
            <option value={value}>{label}</option>
        {/each}
    </select>
</div>
