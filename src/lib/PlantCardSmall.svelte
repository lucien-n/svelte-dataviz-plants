<script>
	import { createEventDispatcher } from 'svelte';

	const disptach = createEventDispatcher();

	export let data;

	data.image =
		data.default_image && data.default_image.original_url != null
			? data.default_image.original_url
			: 'images/plant_placeholder.png';

	function click() {
		disptach('card-click', { data: data });
	}
</script>

<section
	id="card-plant-{data.common_name}"
	class="plant-card"
	on:click={click}
	on:keypress={(event) => {
		if (event.key === 'Enter') click();
	}}
>
	<div class="plant-image">
		<img src={data.image} alt="plant" />
	</div>
	<div class="plant-description">
		<p class="common_name">{data.common_name}</p>
		<p class="scientific_name">
			{data.scientific_name}
		</p>
	</div>
</section>

<style scoped>
	.plant-card {
		font-size: large;
		height: 100%;
		border-radius: 0.75rem;
		background-color: white;
		box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
	}

	.plant-card:hover {
		cursor: pointer;
	}

	.plant-image {
		height: 80%;
		overflow: hidden;
		border-radius: 0.5rem;
	}

	img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		align-self: center;
	}

	.plant-description {
		padding: 0.5rem;
	}

	.common_name {
		font-weight: 600;
		color: #45542c;
		font-weight: bolder;
	}

	.scientific_name {
		font-style: italic;
		color: rgb(110, 110, 110);
		color: rgba(59, 167, 47, 0.815);
	}
</style>
