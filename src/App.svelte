<script>
	import './app.css';

	import PlantCard from './lib/PlantCard.svelte';
	import { plants } from './data';

	async function getPlants() {
		// const data = await fetch(
		// 	'https://perenual.com/api/species-list?page=1&key=sk-pHQb641c2838df533292'
		// );
		// const plants = await data.json();
		return plants;
	}
</script>

<main class="w-full h-full">
	<section
		id="plants-cards"
		class="grid gap-3 grid-cols-2 sm:grid-cols-3 md:grid-cols-4 xl:grid-cols-5 w-full md:w-3/5 mx-auto"
	>
		{#await getPlants() then plants}
			{#each plants.data as plant}
				<PlantCard data={plant} />
			{/each}
		{/await}
	</section>
</main>

<style>
	main {
		background-color: #e9f0e2;
	}
</style>
