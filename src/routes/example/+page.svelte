<script lang="ts">
	import Highcharts from 'highcharts';
	import ExportingModule from 'highcharts/modules/exporting';
	// import { HighchartsSvelte } from 'highcharts-svelte';
	import { HighchartsSvelte } from '$lib/components';
	import { Input, Select, Toggle } from '$lib/components';
	import ColorPicker from '$lib/components/color-picker.svelte';

	// Adding a module
	ExportingModule(Highcharts);

	let title = 'Highcharts works with Svelte!';
	let subtitle = 'Use this integration to make it super-easy.';
	let seriesType: 'line' | 'area' | 'areaspline' | 'column' = 'areaspline';
	let seriesColor = '#c85de3';
	let seriesData = [1, 4, 2, 4, 4, 5];

	const toggles = {
		legend: false,
		exporting: true,
		zoom: false
	};

	const toggleInputs = [
		{
			label: 'Legend enabled',
			key: 'legend'
		},
		{
			label: 'Exporting menu',
			key: 'exporting'
		},
		{
			label: 'Zoom enabled',
			key: 'zoom'
		}
	] as const;

	let options: Highcharts.Options;
	let selectedTab = 'customize';

	$: options = {
		chart: {
			zooming: {
				type: toggles.zoom ? 'xy' : undefined
			}
		},
		title: {
			text: title
		},
		subtitle: {
			text: subtitle
		},
		series: [
			{
				type: seriesType,
				color: seriesColor,
				data: seriesData
			}
		],
		legend: {
			enabled: toggles.legend
		},
		exporting: {
			enabled: toggles.exporting
		}
	};
</script>

<div class="max-w-6xl mx-auto py-12 px-6 grid grid-cols-1 lg:grid-cols-3 gap-4">
	<div class="col-span-2">
		<div class="px-4 py-4 border border-gray-300 rounded-2xl overflow-hidden shadow-sm">
			<HighchartsSvelte {options} highcharts={Highcharts} />
		</div>

		<!-- Later, add more examples
		<div class="mt-8 px-2">
			<h2 class="text-xs font-bold uppercase mb-1 text-gray-800">Other examples</h2>
			<div class="flex gap-6 items-center">
				<a href="/example/map">Maps</a>
				<div class="h-3 w-[1.5px] bg-gray-500/40"></div>
				<a href="/example/stock">Stock</a>
				<div class="h-3 w-[1.5px] bg-gray-500/40"></div>
				<a href="/example/gantt">Gantt</a>
			</div>
		</div>
        -->
	</div>

	<div
		class="px-6 py-6 border rounded-2xl shadow-sm {selectedTab === 'code'
			? 'bg-gray-600 border-gray-900 text-white'
			: 'border-gray-300'} lg:col-span-1 lg:col-start-1 lg:row-start-1"
	>
		<div class="mb-6">
			<div class="sm:hidden">
				<!-- Use an "onChange" listener to redirect the user to the selected tab URL. -->
				<select
					id="tabs"
					class="block w-full rounded-md border-gray-300 focus:border-indigo-500 focus:ring-indigo-500"
					bind:value={selectedTab}
				>
					<option value="customize">Customize</option>
					<option value="code">Code</option>
				</select>
			</div>
			<div class="hidden sm:block">
				<nav class="flex space-x-2" aria-label="Tabs">
					{#if selectedTab === 'customize'}
						<button
							class="flex gap-1.5 items-center bg-indigo-100 text-indigo-700 rounded-md px-3 py-2 text-sm font-medium"
							on:click={() => (selectedTab = 'customize')}
						>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								class="h-4 w-4 text-indigo-600 fill-indigo-600"
								viewBox="0 0 512 512"
								><path
									d="M430.11 347.9c-6.6-6.1-16.3-7.6-24.6-9-11.5-1.9-15.9-4-22.6-10-14.3-12.7-14.3-31.1 0-43.8l30.3-26.9c46.4-41 46.4-108.2 0-149.2-34.2-30.1-80.1-45-127.8-45-55.7 0-113.9 20.3-158.8 60.1-83.5 73.8-83.5 194.7 0 268.5 41.5 36.7 97.5 55 152.9 55.4h1.7c55.4 0 110-17.9 148.8-52.4 14.4-12.7 11.99-36.6.1-47.7z"
									fill="none"
									stroke="currentColor"
									stroke-miterlimit="10"
									stroke-width="32"
								/><circle cx="144" cy="208" r="32" /><circle cx="152" cy="311" r="32" /><circle
									cx="224"
									cy="144"
									r="32"
								/><circle cx="256" cy="367" r="48" /><circle cx="328" cy="144" r="32" /></svg
							>
							Customize
						</button>
						<button
							class="flex gap-1.5 items-center bg-gray-50 hover:bg-gray-200 text-gray-500 hover:text-gray-700 rounded-md px-3 py-2 text-sm font-medium"
							on:click={() => (selectedTab = 'code')}
						>
							<svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" viewBox="0 0 512 512"
								><path
									fill="none"
									stroke="currentColor"
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="32"
									d="M160 368L32 256l128-112M352 368l128-112-128-112M304 96l-96 320"
								/></svg
							>
							<span>Code</span>
						</button>
					{:else}
						<button
							class="flex gap-1.5 items-center bg-gray-500/50 text-gray-200 rounded-md px-3 py-2 text-sm font-medium"
							on:click={() => (selectedTab = 'customize')}
						>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								class="h-4 w-4 text-gray-200 fill-gray-200"
								viewBox="0 0 512 512"
								><path
									d="M430.11 347.9c-6.6-6.1-16.3-7.6-24.6-9-11.5-1.9-15.9-4-22.6-10-14.3-12.7-14.3-31.1 0-43.8l30.3-26.9c46.4-41 46.4-108.2 0-149.2-34.2-30.1-80.1-45-127.8-45-55.7 0-113.9 20.3-158.8 60.1-83.5 73.8-83.5 194.7 0 268.5 41.5 36.7 97.5 55 152.9 55.4h1.7c55.4 0 110-17.9 148.8-52.4 14.4-12.7 11.99-36.6.1-47.7z"
									fill="none"
									stroke="currentColor"
									stroke-miterlimit="10"
									stroke-width="32"
								/><circle cx="144" cy="208" r="32" /><circle cx="152" cy="311" r="32" /><circle
									cx="224"
									cy="144"
									r="32"
								/><circle cx="256" cy="367" r="48" /><circle cx="328" cy="144" r="32" /></svg
							>
							Customize
						</button>
						<button
							class="flex gap-1.5 items-center bg-indigo-500 text-gray-100 hover:text-gray-200 rounded-md px-3 py-2 text-sm font-medium"
							on:click={() => (selectedTab = 'code')}
						>
							<svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" viewBox="0 0 512 512"
								><path
									fill="none"
									stroke="currentColor"
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="32"
									d="M160 368L32 256l128-112M352 368l128-112-128-112M304 96l-96 320"
								/></svg
							>
							<span>Code</span>
						</button>
					{/if}
				</nav>
			</div>
		</div>

		{#if selectedTab === 'code'}
			<!-- TODO: Add 'Select All Code' button -->
			<!-- TODO: Add a code highlighter for TS -->
			<pre class="overflow-x-auto text-sm"><code
					>&lt;script lang="ts"&gt;
    import Highcharts from 'highcharts';
    import ExportingModule from 'highcharts/modules/exporting';
    import HighchartsSvelte from 'highcharts-svelte';

    // Adding a module
    ExportingModule(Highcharts);

    let title = 'Highcharts works with Svelte!';
    let subtitle = 'Use this integration to make it super-easy.'
    let seriesType: 'line' | 'area' | 'areaspline' | 'column' = 'areaspline';
    let seriesColor = '#c85de3';
    let seriesData = [1, 4, 2, 4, 4, 5];
    let legendEnabled = false;
    let exportingEnabled = true;
    let zoomEnabled = false;

    let options: Highcharts.Options;

    $: options = &lbrace;
        chart: &lbrace;
            zooming: &lbrace;
                type: zoomEnabled ? 'xy' : undefined
            &rbrace;
        &rbrace;,
        title: &lbrace;
            text: title
        &rbrace;,
        subtitle: &lbrace;
            text: subtitle
        &rbrace;,
        series: [&lbrace;
            type: seriesType,
            color: seriesColor,
            data: seriesData
        &rbrace;],
        legend: &lbrace;
            enabled: legendEnabled
        &rbrace;,
        exporting: &lbrace;
            enabled: exportingEnabled
        &rbrace;
    &rbrace;
&lt;/script&gt;

&lt;HighchartsSvelte options=&lbrace;options&rbrace; highcharts=&lbrace;Highcharts&rbrace;/&gt;

&lt;input
    type="text"
    name="Title"
    id="series-title"
    placeholder="Enter the title for your chart..."
    bind:value=&lbrace;title&rbrace;/&gt;</code
				></pre>
		{:else}
			<div>
				<h2 class="font-semibold text-xl mb-4">Customize your chart dynamically</h2>

				<div class="flex flex-col gap-4">
					<Input label="Title" placeholder="Enter the title for your chart..." bind:value={title} />

					<Input
						label="Subtitle"
						placeholder="Enter the subtitle for your chart..."
						bind:value={subtitle}
					/>

					<ColorPicker label="Color of the series" bind:value={seriesColor} />

					<Select
						label="Series type"
						options={[
							{ value: 'line', label: 'Line' },
							{ value: 'area', label: 'Area' },
							{ value: 'areaspline', label: 'Areaspline' },
							{ value: 'column', label: 'Column' }
						]}
						bind:value={seriesType}
					/>

					<div class="h-[1px] w-full bg-gray-200 my-4"></div>

					<div class="flex flex-col gap-4">
						{#each toggleInputs as toggle}
							<Toggle label={toggle.label} bind:value={toggles[toggle.key]} />
						{/each}
					</div>
				</div>
			</div>
		{/if}
	</div>
</div>

<slot name="panel" />
