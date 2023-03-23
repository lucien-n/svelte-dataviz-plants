<script>
	import './app.css';
	import { plants } from './data';
	import PlantCard from './lib/PlantCardSmall.svelte';
	import PlantModal from './lib/PlantModal.svelte';

	let plantModalVisible = false;
	let plantModalData = {};

	async function getPlants() {
		return plants;
	}

	function showPlantModal(e) {
		console.log('Show modal for: ', e.detail.data.common_name);
		plantModalData = e.detail.data;
		plantModalVisible = true;
	}
</script>

<main class="w-full h-full">
	<section
		id="plants-cards"
		class="grid gap-3 grid-cols-2 sm:grid-cols-3 md:grid-cols-4 xl:grid-cols-5 w-full md:w-3/5 mx-auto"
	>
		{#await getPlants() then plants}
			{#each plants.data as plant}
				<PlantCard data={plant} on:card-click={showPlantModal} />
			{/each}
		{/await}
	</section>
	{#if plantModalVisible}
		<PlantModal
			data={plantModalData}
			on:close-modal={() => (plantModalVisible = false)}
		/>
	{/if}
</main>
