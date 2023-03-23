<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let data;

	function close() {
		dispatch('close-modal');
	}
</script>

<section
	id="modal-plant-{data.common_name}"
	class="fixed top-0 left-0 w-full h-full bg-zinc-700 bg-opacity-40 flex items-center "
>
	<div
		class="relative bg-white border-zinc-500 border rounded-md shadow-md h-2/3 max-w-xl mx-auto"
	>
		<button class="absolute -right-4 -top-4" on:click={close}
			><img
				src="images/x-mark.svg"
				class="w-8 h-8 bg-white rounded-2xl"
				alt=""
			/></button
		>
		<!-- Image -->
		<div class="h-2/3 w-full overflow-hidden rounded-t-md shadow-lg">
			<img
				src={data.image}
				alt=""
				class="w-min h-full object-cover hover:cursor-pointer"
			/>
		</div>
		<!-- Data -->
		<div class="p-2 text-lg">
			<!-- Names -->
			<div class="flex justify-between">
				<!-- Common -->
				<p class="font-semibold">{data.common_name}</p>
				<!-- Scientific -->
				<p class="italic text-zinc-500">
					{data.scientific_name}
				</p>
			</div>
			<p class="italic">{data.cycle}</p>
			<!-- Sunlight -->
			<div class="flex gap-2">
				<img src="images/sun.png" alt="" width="32" height="32" />
				<div class="flex text-md">
					{#if data.sunlight.length > 0}
						{#each data.sunlight as sunlight}
							<p class="italic">{sunlight}</p>
							{#if !(data.sunlight.indexOf(sunlight) + 1 >= data.sunlight.length)}
								<p class="mx-2 self-center italic text-sm">&</p>
							{/if}
						{/each}
					{:else}
						<p class="italic text-zinc-600">No data provided</p>
					{/if}
				</div>
			</div>
			<!-- Watering -->
			<div class="flex gap-2">
				<img
					src="images/watering_can.png"
					alt=""
					width="32"
					height="32"
				/>
				<div class="text-md self-end">
					<p class="italic">{data.watering}</p>
				</div>
			</div>
		</div>
	</div>
</section>
