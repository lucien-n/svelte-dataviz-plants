<script>
	
	import PlantCard from './lib/PlantCard.svelte';
	import {plants} from './response_data';
	import Carrousel from './lib/Carrousel.svelte';


	async function getPlant() {
		// const data = await fetch(
		// 	'https://perenual.com/api/species-list?page=1&key=sk-cVD1641c2959b9ca1305'
		// );
		// const response = await data.json();
		// console.log(response)
		return plants;
	}
	
</script>


<main>
	<div>
		<Carrousel/>
	</div>
	
	<div id= "plants">
	<!-- {#each plants as plant}
		<PlantCard name={plant.name} type={plant.type} />
	{/each} -->
	{#await getPlant() then response}
		{#each response.data as plant}
			<PlantCard data={plant} />
		{/each}
	{/await}
</div>



</main>


<style>
#plants{
	display : grid;
	
}

</style>