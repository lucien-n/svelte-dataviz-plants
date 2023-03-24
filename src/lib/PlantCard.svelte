<script>
	export let data;
</script>

<section id="plant-{data.common_name} " class = "plant">
	<p>Common Name: {data.common_name}</p>
	<p>Scientific Name: {data.scientific_name}</p>
</section>

<style scoped>
	section {
		border: 2px solid black;
display: grid;

	}

</style>
