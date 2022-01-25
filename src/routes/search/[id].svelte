<script context="module">
	export async function load({ fetch, params }) {
		const res =
			await fetch(`https://api.themoviedb.org/3/search/movie?api_key=6c585d930b6b55e72e3e31c6506a6ee4&language=en-US&query=${params.id}&page=1&include_adult=false
`);

		const data = await res.json();

		console.log(data);

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
</script>

<div class="searched-movies">
	{#each searchedMovie as movie}
		<h1>Found: {movie.count}</h1>
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
