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

	export let destinations;
</script>

<!-- Hero Section -->

<div>
	<div class="grid lg:grid-cols-2 2xl:grid-cols-5">
		<div
			class="p-8 py-12 max-w-md mx-auto sm:max-w-xl lg:px-12 lg:py-24 lg:max-w-full xl:mr-0 2xl:col-span-2"
		>
			<div class="xl:max-w-xl">
				<img class="h-10" src="/img/logo-brand.svg" alt="Workcation" />
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
