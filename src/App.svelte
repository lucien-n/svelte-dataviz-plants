<script>
	import './app.css';
	import { plants } from './data';
	import PlantCard from './lib/PlantCardSmall.svelte';
	import PlantModal from './lib/PlantModal.svelte';
	import Carrousel from './lib/Carrousel.svelte';

	let plantModalVisible = false;
	let plantModalData = {};

	async function getPlants() {
		return plants;
	}

	function showPlantModal(e) {
		plantModalData = e.detail.data;
		plantModalVisible = true;
	}
</script>

<main>
	<div class="container">
		<div>
			<Carrousel />
		</div>
		<section id="plants-cards">
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
	</div>
</main>

<style>
	main {
		width: 100%;
		height: 100%;
	}
	.container {
		width: 70%;
		margin-left: auto;
		margin-right: auto;
	}

	section#plants-cards {
		display: grid;
		gap: 0.75rem;
		grid-template-columns: repeat(5, minmax(0, 1fr));
		width: 100%;
		margin-left: auto;
		margin-right: auto;
	}
</style>
