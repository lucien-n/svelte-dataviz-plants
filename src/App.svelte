<script>
	import './app.css';

	import PlantCard from './lib/PlantCard.svelte';

	async function getPlants() {
		const data = await fetch(
			'https://perenual.com/api/species-list?page=1&key=sk-9lep6419bee20788e274'
		);
		const plants = await data.json();
		return plants;
	}
</script>

<main>
	{#await getPlants() then plants}
		{#each plants.data as plant}
			<PlantCard data={plant} />
		{/each}
	{/await}
</main>
