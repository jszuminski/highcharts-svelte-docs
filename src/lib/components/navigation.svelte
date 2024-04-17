<script lang="ts">
	import { fade } from 'svelte/transition';
	import { base } from '$app/paths';
	import { page } from '$app/stores';

	const links = [
		{
			name: 'Example',
			href: `${base}/example`
		},
		{
			name: 'Docs',
			href: `${base}/docs`
		},
		{
			name: 'Changelog',
			href: `${base}/changelog`
		},
		{
			name: 'npm',
			href: 'https://www.npmjs.com/package/highcharts-svelte'
		},
		{
			name: 'Highcharts API',
			href: 'https://api.highcharts.com/highcharts'
		}
	];

	let mobileMenuOpen = false;
</script>

<nav class="bg-white shadow">
	<div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
		<div class="relative flex h-16 justify-between">
			<div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
				<button
					type="button"
					class="relative inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-100 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500"
					aria-controls="mobile-menu"
					aria-expanded="false"
					on:click={() => (mobileMenuOpen = !mobileMenuOpen)}
				>
					{#if !mobileMenuOpen}
						<svg
							class="h-6 w-6"
							fill="none"
							viewBox="0 0 24 24"
							stroke-width="1.5"
							stroke="currentColor"
							aria-hidden="true"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"
							/>
						</svg>
					{:else}
						<svg
							class="h-6 w-6"
							fill="none"
							viewBox="0 0 24 24"
							stroke-width="1.5"
							stroke="currentColor"
							aria-hidden="true"
						>
							<path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
						</svg>
					{/if}
				</button>
			</div>

			<div class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-start">
				<div class="flex flex-shrink-0 items-center">
					<img
						class="h-8 w-auto"
						src="https://media.licdn.com/dms/image/C4D0BAQEil3t3MpDTIA/company-logo_200_200/0/1637830067451/highsoft_logo?e=2147483647&v=beta&t=nupH1rbX-GGeMwCGMOREOkJu0jVgeSzvWVPQLBij8VU"
						alt="Highsoft / Highcharts logo"
					/>
				</div>
				<div class="hidden sm:ml-8 sm:flex sm:space-x-8">
					{#each links as { name, href }}
						<a
							{href}
							class="inline-flex items-center border-b-2 border-transparent px-1 pt-1 text-sm font-medium
                                {$page.url.pathname === href
								? ' border-indigo-500 text-gray-900'
								: ' border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'}"
						>
							{name}
						</a>
					{/each}
				</div>
			</div>
		</div>
	</div>

	<!-- Mobile menu, show/hide based on menu state. -->
	{#if mobileMenuOpen}
		<div class="sm:hidden" id="mobile-menu" transition:fade>
			<div class="space-y-1 pb-4 pt-2">
				{#each links as { name, href }}
					<a
						{href}
						class="block border-l-4 py-2 pl-3 pr-4 text-base font-medium {$page.url.pathname ===
						href
							? 'border-indigo-500 bg-indigo-50 text-indigo-700'
							: 'border-transparent text-gray-500 hover:border-gray-300 hover:bg-gray-50 hover:text-gray-700'}"
					>
						{name}
					</a>
				{/each}
			</div>
		</div>
	{/if}
</nav>
