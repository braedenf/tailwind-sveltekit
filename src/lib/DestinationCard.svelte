<script>
	export let destination;
</script>

<div class="flex items-center rounded-lg shadow-lg overflow-hidden bg-white">
	<img class="h-32 w-32 flex-shrink-0" src={destination.imageUrl} alt={destination.imageAlt} />
	<div class="px-6 py-4">
		<h3 class="text-lg font-semibold text-gray-800">{destination.city}</h3>
		<p class="text-gray-600">${destination.averagePrice} / night average</p>
		<div>
			<a class="text-brand-dark hover:text-brand font-semibold font-sm" href="/">
				Explore {destination.propertyCount} properties
			</a>
		</div>
	</div>
</div>
