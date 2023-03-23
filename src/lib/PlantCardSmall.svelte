<script>
	import { createEventDispatcher } from 'svelte';

	const disptach = createEventDispatcher();

	export let data;

	let image_url =
		data.default_image && data.default_image.original_url != null
			? data.default_image.original_url
			: 'images/plant_placeholder.png';

	// So we don't have to redo this ↑ in PlantModal.svelte
	data.image = image_url;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<section
	id="card-plant-{data.common_name}"
	class="bg-white border-zinc-500 border rounded-md h-full hover:cursor-pointer shadow-md transition ease-in-out duration-300 hover:shadow-2xl hover:border-zinc-00"
	on:click={() => disptach('card-click', { data: data })}
>
	<div class="h-2/3 overflow-hidden rounded-t-md shadow-lg">
		<img
			src={data.image}
			alt=""
			class="w-full h-full self-center hover:cursor-pointer"
			style="object-fit: cover;"
		/>
	</div>
	<div class="p-2">
		<p class="font-semibold text-md">{data.common_name}</p>
		<p class="italic text-zinc-500">
			{data.scientific_name}
		</p>
	</div>
</section>
