<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let data;

	function close() {
		dispatch('close-modal');
	}
</script>

<section id="modal-plant-{data.common_name}" class="modal">
	<div class="modal-card">
		<button class="modal-close" on:click={close}
			><img src="images/x-mark.svg" alt="close button" /></button
		>
		<!-- Image -->
		<div class="modal-image">
			<img src={data.image} alt="plant" />
		</div>
		<!-- Content -->
		<div class="modal-content">
			<!-- Names -->
			<div class="content-title">
				<!-- Common -->
				<p class="common">{data.common_name}</p>
				<!-- Scientific -->
				<p class="scientific">
					{data.scientific_name}
				</p>
			</div>
			<div class="content-description">
				<p>{data.cycle}</p>
				<!-- Sunlight -->
				<div class="sunlight">
					<img
						src="images/sun.png"
						alt="sunlight"
						width="32"
						height="32"
					/>
					<div class="sunlight">
						{#if data.sunlight.length > 0}
							{#each data.sunlight as sunlight}
								<p>{sunlight}</p>
							{/each}
						{:else}
							<p class="no-data">No data provided</p>
						{/if}
					</div>
				</div>
				<!-- Watering -->
				<div class="watering">
					<img
						src="images/watering_can.png"
						alt="watering"
						width="32"
						height="32"
					/>
					<div class="watering">
						<p>{data.watering}</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<style>
	.modal {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(40, 40, 40, 0.4);
		display: flex;
		align-items: center;
	}

	.modal-card {
		position: relative;
		border: 2px solid gray;
		height: 66.667%;
		max-width: 36rem;
		margin-left: auto;
		margin-right: auto;
		background-color: white;
	}

	.modal-close {
		position: absolute;
		background-color: white;
		outline: none;
		border: 2px solid rgb(110, 110, 110);
		right: -1rem;
		top: -1rem;
	}

	.modal-close > img {
		width: 2rem;
		height: 2rem;
	}

	.modal-close:hover {
		cursor: pointer;
	}

	.modal-image {
		height: 66.667%;
		width: 100%;
		overflow: hidden;
	}

	.modal-image > img {
		width: min-content;
		height: 100%;
		object-fit: cover;
	}

	.modal-image:hover {
		cursor: pointer;
	}

	.modal-content {
		padding: 0.5rem;
		font-size: 1.125rem;
		line-height: 1.75rem;
	}

	.content-title {
		display: flex;
		justify-content: space-between;
	}

	.content-title > .common {
		font-weight: 600;
	}

	.content-title > .scientific {
		font-style: italic;
		color: rgb(110, 110, 110);
	}

	.content-description > .sunlight {
		display: flex;
		gap: 0.5rem;
	}

	.content-description > .watering {
		display: flex;
		gap: 0.5rem;
	}

	.no-data {
		font-style: italic;
		color: rgb(110, 110, 110);
	}
</style>
