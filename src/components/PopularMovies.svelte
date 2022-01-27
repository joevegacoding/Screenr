<script>
	export let popular;
	export let popularTV;
	import TVShowCard from './TVShowCard.svelte';
	import MovieCard from './MovieCard.svelte';
	import Tabs from '../components/Tabs.svelte';
	import { fly } from 'svelte/transition';
	let items = ['Movies', 'TV Shows'];
	let activeItem = 'Movies';

	const tabChanged = (e) => {
		activeItem = e.detail;
	};
</script>

<div class="header-section">
	<h3>Popular And Trending</h3>
	<Tabs {activeItem} {items} on:tabChanged={tabChanged} />
</div>

<div class="popular-movies">
	{#if activeItem === 'Movies'}
		{#each popular as movie}
			<div in:fly={{ z: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
				<MovieCard {movie} />
			</div>
		{/each}
	{:else if activeItem === 'TV Shows'}
		{#each popularTV as tv}
			<div in:fly={{ z: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
				<TVShowCard {tv} />
			</div>
		{/each}
	{/if}
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@100;300;400;500;700&display=swap');
	h3 {
		font-size: 3rem;
		font-family: 'Outfit', sans-serif;
		margin-bottom: 1rem;
	}

	.header-section {
		padding: 0rem 1rem 0.8rem 3.5rem;
	}

	@media screen and (max-width: 768px) {
		.header-section {
			padding: 0rem 1rem 0.8rem 2rem;
		}
	}

	.popular-movies {
		margin: 0 5%;

		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		grid-column-gap: 2rem;
		grid-row-gap: 2rem;
	}
</style>
