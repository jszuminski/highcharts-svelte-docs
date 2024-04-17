<script lang="ts">
    export let label: string;
    export let value: boolean;
</script>

<label class="flex items-center gap-3">
    <span class="flex justify-center items-center text-sm font-medium text-gray-900 mt-1">
        {label}
    </span>

    <button
        type="button"
        class="{value ? 'bg-indigo-600' : 'bg-gray-200'} mt-1 relative inline-flex h-5 w-10 flex-shrink-0 cursor-pointer
            rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out
            focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-offset-2"
        on:click={() => value = !value}>

        <span aria-hidden="true" class="{value ? 'translate-x-5 ' : 'translate-x-0 '} pointer-events-none inline-block
            h-4 w-4 transform rounded-full bg-white shadow
            ring-0 transition duration-200 ease-in-out">
        </span>
    </button>
</label>