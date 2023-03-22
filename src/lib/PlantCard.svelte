<script>
	export let data;

	let image_url =
		data.default_image && data.default_image.original_url != null
			? data.default_image.original_url
			: 'https://placeholder.pics/svg/300';
</script>

<section
	id="plant-{data.common_name}"
	class="mx-auto flex border-zinc-500 border rounded-md h-1/6"
>
	<div
		class="flex w-2/5 overflow-hidden rounded-md border border-b-0 border-zinc-700 shadow-lg"
	>
		<img
			src={image_url}
			alt=""
			class="w-full h-full self-center rounded-lg rounded-r-none hover:cursor-pointer"
			style="object-fit: cover;"
		/>
	</div>
	<div class="p-2">
		<p>Common Name: {data.common_name}</p>
		<p>Scientific Name: {data.scientific_name}</p>
	</div>
</section>
