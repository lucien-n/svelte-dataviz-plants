<script>
	import PlantCard from './lib/PlantCard.svelte';

	async function getPlant() {
		const data = await fetch(
			'https://perenual.com/api/species-list?page=1&key=sk-jxea641c2a2474900306'
		);
		const response = await data.json();
		return response;
	}
</script>

<main>
	<!-- {#each plants as plant}
		<PlantCard name={plant.name} type={plant.type} />
	{/each} -->
	{#await getPlant() then response}
		{#each response.data as plant}
			<PlantCard data={plant} />
		{/each}
	{/await}
</main>
