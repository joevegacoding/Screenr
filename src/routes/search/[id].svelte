<script context="module">
	export async function load({ fetch, params }) {
		const apiKey = import.meta.env.VITE_API_KEY;
		const res =
			await fetch(`https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&language=en-US&query=${params.id}&page=1&include_adult=false
`);

		const data = await res.json();

		console.log(data.results.count);

		if (res.ok) {
			return {
				props: { searchedMovie: data.results }
			};
		}
	}
</script>

<script>
	import MovieCard from '../../components/MovieCard.svelte';
	export let searchedMovie;
	import.meta.env.VITE_API_KEY;
</script>

<h2>Found {searchedMovie.length} items</h2>
<div class="searched-movies">
	{#each searchedMovie as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	.searched-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		grid-column-gap: 2rem;
		grid-row-gap: 2rem;
		margin: 0 5%;
	}
</style>
