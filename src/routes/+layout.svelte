<script lang="ts">
    import 'tailwindcss/tailwind.css';
    import '../app.post.css';

    import { Navigation } from '$lib/components';
</script>

<svelte:head>
    <title>Highcharts + Svelte</title>
</svelte:head>

<Navigation/>
<slot/>