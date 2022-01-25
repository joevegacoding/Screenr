<script context="module">
	export async function load({ fetch }) {
		const apiKey = import.meta.env.VITE_API_KEY;
		const resMovie =
			await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${apiKey}&language=en-US
`);

		const resTV =
			await fetch(`https://api.themoviedb.org/3/tv/popular?api_key=${apiKey}&language=en-US
`);
		const dataMovie = await resMovie.json();
		const dataTV = await resTV.json();
		console.log(dataMovie);
		console.log(dataTV);

		if (resMovie.ok) {
			return {
				props: { popular: dataMovie.results, popularTV: dataTV.results }
			};
		}
	}
</script>

<script>
	import.meta.env.VITE_API_KEY;
	import PopularMovies from '../components/PopularMovies.svelte';
	export let popular;
	export let popularTV;

	import global_style from '../global_style.css';
	import SearchMovies from '../components/SearchMovies.svelte';
	import { fly } from 'svelte/transition';
</script>

<section in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
	<PopularMovies {popular} {popularTV} />
</section>

<style>
	body {
		overflow-x: hidden;
	}
</style>
