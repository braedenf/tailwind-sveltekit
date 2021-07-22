<script context="module">
	export async function load({ fetch }) {
		const res = await fetch('/api');

		if (res.ok) return { props: { destinations: await res.json() } };
		return {
			status: res.status,
			error: new Error()
		};
	}
</script>

<script>
	import DestinationCard from '$lib/DestinationCard.svelte';
	import {clickOutside} from '../lib/clickOutsideElement';

	export let destinations;

	let menuVisible = true;
</script>

<!-- Nav bar -->

<header use:clickOutside on:click_outside={() => menuVisible = !menuVisible}>
	<nav class="px-6">
		<div class="mt-6 flex justify-between">
			<img class="h-10" src="/img/logo-brand.svg" alt="Workcation" />
			<button on: on:click={() => menuVisible = !menuVisible} class="focus:outline-none focus:ring focus:ring-opacity-50 focus:ring-brand-light rounded" alt="Menu Button">
				{#if menuVisible}
					<svg xmlns="http://www.w3.org/2000/svg" class="h-10 text-brand hover:text-brand-light h-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
					</svg>
				{:else}
					<svg class="text-brand hover:text-brand-light h-10" xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
						<path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M4 6h16M4 12h16M4 18h16" />
					</svg>
				{/if}
			</button>
		</div>
		<ul class="py-3 font-headline mt-4 {menuVisible ? 'flex' : 'hidden'} flex-col space-y-2">
			<li class="hover:bg-brand hover:text-white p-2 rounded-lg shadow-sm"><a class="inline-block w-full" href="/">All Destinations</a></li>
			<li class="hover:bg-brand hover:text-white p-2 rounded-lg shadow-sm"><a class="inline-block w-full" href="/">About</a></li>
			<li class="hover:bg-brand hover:text-white p-2 rounded-lg shadow-sm"><a class="inline-block w-full" href="/">Contact</a></li>
		</ul>
	</nav>
</header>

<!-- Hero Section -->

<div>
	<div class="grid lg:grid-cols-2 2xl:grid-cols-5">
		<div
			class="p-8 py-12 max-w-md mx-auto sm:max-w-xl lg:px-12 lg:py-24 lg:max-w-full xl:mr-0 2xl:col-span-2"
		>
			<div class="xl:max-w-xl">
				
				<img
					class="mt-6 rounded-lg shadow-xl sm:mt-8 sm:h-64 sm:w-full sm:object-cover object-center lg:hidden"
					src="/img/beach-work.jpg"
					alt="Woman workcationing on the beach"
				/>
				<h1
					class="mt-6 text-2xl font-semibold tracking-tight font-headline text-gray-900 sm:mt-8 sm:text-4xl lg:text-3xl xl:text-4xl"
				>
					You can work from anywhere.
					<br class="hidden lg:inline" />
					<span class="text-brand">Take advantage of it.</span>
				</h1>
				<p class="mt-2 text-gray-600 sm:mt-4 sm:text-xl">
					Workcation helps you find work-friendly rentals in beautiful locations so you can enjoy
					some nice weather even when you're not on vacation.
				</p>
				<div class="mt-4 sm:mt-6">
					<a
						class="btn bg-brand hover:bg-brand-light focus:ring-brand-light active:bg-brand-dark"
						href="/">Book your escape</a
					>
				</div>
			</div>
		</div>

		<div class="hidden relative lg:block 2xl:col-span-3">
			<img
				class="absolute inset-0 w-full h-full object-cover object-center"
				src="/img/beach-work.jpg"
				alt="Woman workcationing on the beach"
			/>
		</div>
	</div>

	<!-- List of popular destinations -->

	<div class="py-8 px-8 max-w-md sm:max-w-xl lg:max-w-6xl lg:px-12 mx-auto">
		<h2 class="text-xl text-gray-900">Popular Destinations</h2>
		<p class="mt-2 text-gray-600">
			A selection of great work-friendly cities with lots to see and explore.
		</p>
		<div class="mt-6 grid gap-6 lg:grid-cols-2 xl:grid-cols-3">
			{#each destinations.data as destination}
				<DestinationCard {destination} />
			{/each}
		</div>
	</div>
</div>
