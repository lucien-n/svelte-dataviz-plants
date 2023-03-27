<script>
	import './app.css';
	import { plants } from './data';
	import PlantCard from './lib/PlantCardSmall.svelte';
	import PlantModal from './lib/PlantModal.svelte';
	import Carrousel from './lib/Carrousel.svelte';
	import { writable } from 'svelte/store';

	let plantModalVisible = false;
	let plantModalData = {};

	const category = writable('');

	let get_plants = getPlants();

	async function getPlants() {
		return plants;
	}

	function showPlantModal(e) {
		plantModalData = e.detail.data;
		plantModalVisible = true;
	}

	const _ = category.subscribe((_) => {
		get_plants = getPlants();
	});
</script>

<main>
	<div class="container">
		<div>
			<Carrousel
				on:change-category={(event) =>
					category.set(event.detail.category)}
			/>
		</div>
		<section id="plants-cards">
			{#await get_plants then plants}
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
