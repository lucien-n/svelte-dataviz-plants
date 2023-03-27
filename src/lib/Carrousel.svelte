<script>
	import { createEventDispatcher } from 'svelte/internal';

	const dispatch = createEventDispatcher();

	let tab = [];
	let flecheG;
	let flecheD;
	let slide;
	let indice_element_active = 1;

	let categories = [
		{ name: 'sunlight:full_sun', image: 'images/sun.png' },
		{ name: 'sunlight:sun-part_shade', image: 'images/sun.png' },
		{ name: 'sunlight:part_shade', image: 'images/sun.png' },
		{ name: 'sunlight:full_shade', image: 'images/sun.png' },
		{ name: 'watering:frequent', image: 'images/arrosoir.png' },
		{ name: 'watering:average', image: 'images/arrosoir.png' },
		{ name: 'watering:minimum', image: 'images/arrosoir.png' },
		{ name: 'watering:none', image: 'images/arrosoir.png' },
	];

	function augmenter(variable) {
		variable.style = 'z-index:2;transform:scale(1.2);width:calc(2*100%);';
	}
	function diminuer(variable) {
		variable.style = 'z-index:1;transform:scale(1);';
	}

	window.onload = () => {
		augmenter(tab[indice_element_active]);
	};

	function flecheGScale() {
		if (indice_element_active != 1) {
			diminuer(tab[indice_element_active]);
			augmenter(tab[indice_element_active - 1]);

			slide.scrollBy(-210, 0);
			indice_element_active = indice_element_active - 1;
		}
	}
	function flecheDScale() {
		if (indice_element_active != categories.length) {
			diminuer(tab[indice_element_active]);
			augmenter(tab[indice_element_active + 1]);
			slide.scrollBy(210, 0);
			indice_element_active = indice_element_active + 1;
		}
	}

	function changeCategory(category) {
		dispatch('change-category', { category: category });
	}
</script>

<section id="carrousel">
	<div class="ensemble-fleche">
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<img
			src="images/fleche_gauche.svg"
			alt=""
			class="img_svg"
			id="img_svg1"
			bind:this={flecheG}
			on:click={flecheGScale}
			on:keypress={(e) => {
				if (e.key === 'Enter') flecheGScale();
			}}
		/>
		<div class="slide" bind:this={slide}>
			<div class="card cardX" bind:this={tab[0]} />
			{#each categories as category, index}
				<div
					class="card card-{index + 1}"
					bind:this={tab[index + 1]}
					on:click={() => changeCategory(category.name)}
					on:keypress={(event) => {
						if (event.key === 'Enter')
							changeCategory(category.name);
					}}
				>
					<img src={category.image} alt="" class="img_categorie" />
					<h1>{category.name.split(':')[1]}</h1>
				</div>
				{#if index == categories.length - 1}
					<div class="card cardX" bind:this={tab[index + 2]} />
				{/if}
			{/each}
		</div>
		<img
			src="images/fleche_droite.svg"
			alt=""
			class="img_svg"
			bind:this={flecheD}
			on:click={flecheDScale}
			on:keypress={(e) => {
				if (e.key === 'Enter') flecheDScale();
			}}
		/>
	</div>
</section>

<style>
	.slide {
		padding-top: 80px;
		padding-bottom: 80px;
		display: flex;
		overflow: scroll;
		scroll-behavior: smooth;
	}
	.img_svg {
		width: 50px;
	}
	.ensemble-fleche {
		width: 700px;
		min-width: 700px;
		display: flex;
		margin: auto;
	}
	::-webkit-scrollbar {
		display: none;
	}

	.card {
		border: 1px solid black;
		width: 200px;
		height: 400px;
		min-width: 200px;
		min-height: 400px;
		transition-duration: 1000ms;
		margin: 5px;
		z-index: 1;
	}

	.card .img_categorie {
		width: 100%;
	}
	/* .card2 .img_categorie{
width: 100%
}
.card3 .img_categorie{
width: 100%
}
.card4 .img_categorie{
width: 100%
}
.card5 .img_categorie{
width: 100%
}
.card6 .img_categorie {
width: 100%;
} */
</style>
