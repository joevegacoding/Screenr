<script context="module">
	export async function load({ fetch }) {
		const apiKey = import.meta.env.VITE_API_KEY;
		const res =
			await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${apiKey}&language=en-US
`);
		const data = await res.json();

		console.log(data);

		if (res.ok) {
			return {
				props: { popular: data.results }
			};
		}
	}
</script>

<script>
	import.meta.env.VITE_API_KEY;
	import PopularMovies from '../components/PopularMovies.svelte';
	export let popular;
	import global_style from '../global_style.css';
	import SearchMovies from '../components/SearchMovies.svelte';
	import { fly } from 'svelte/transition';
</script>

<section in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
	<PopularMovies {popular} />
</section>
