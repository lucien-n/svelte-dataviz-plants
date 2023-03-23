<script>
	export let data;

	let image_url =
		data.default_image && data.default_image.original_url != null
			? data.default_image.original_url
			: 'https://placeholder.pics/svg/100';
</script>

<section
	id="plant-{data.common_name}"
	class=" bg-white border-zinc-500 border rounded-md h-full hover:cursor-pointer shadow-md transition ease-in-out duration-300 hover:shadow-2xl hover:border-zinc-00"
>
	<div class="h-2/3 overflow-hidden rounded-t-md shadow-lg">
		<img
			src={image_url}
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
