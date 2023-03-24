<script>
	import { listen_dev } from 'svelte/internal';
	import { createEventDispatcher } from 'svelte/internal';

	let tab = [];
	let flecheG;
	let flecheD;
	let slide;
	let indice_element_active = 1;

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
		if (indice_element_active != 5) {
			diminuer(tab[indice_element_active]);
			augmenter(tab[indice_element_active + 1]);
			slide.scrollBy(210, 0);
			indice_element_active = indice_element_active + 1;
		}
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
		/>
		<div class="slide" bind:this={slide}>
			<div class="card cardX" bind:this={tab[0]} />
			<div
				class="card card1"
				bind:this={tab[1]}
				on:click={() => {
					createEventDispatcher('choix-categorie', {
						categorie: 'full_sun',
					});
				}}
			>
				<img src="./images/sun.png" alt="" class="img_categorie" />
			</div>
			<div
				class="card card2"
				bind:this={tab[2]}
				on:click={() => {
					createEventDispatcher('choix-categorie', { categorie: '' });
				}}
			>
				<img src="./images/nuage.png" alt="" class="img_categorie" />
			</div>
			<div
				class="card card3"
				bind:this={tab[3]}
				on:click={() => {
					createEventDispatcher('choix-categorie', { categorie: '' });
				}}
			>
				<img src="./images/arrosoir.png" alt="" class="img_categorie" />
			</div>
			<div
				class="card card4"
				bind:this={tab[4]}
				on:click={() => {
					createEventDispatcher('choix-categorie', { categorie: '' });
				}}
			>
				<img src="./images/sun.png" alt="" class="img_categorie" />
			</div>
			<div
				class="card card5"
				bind:this={tab[5]}
				on:click={() => {
					createEventDispatcher('choix-categorie', { categorie: '' });
				}}
			>
				<img src="./images/sun.png" alt="" class="img_categorie" />
			</div>
			<div class="card cardX" bind:this={tab[6]} />
		</div>
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<img
			src="images/fleche_droite.svg"
			alt=""
			class="img_svg"
			bind:this={flecheD}
			on:click={flecheDScale}
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
