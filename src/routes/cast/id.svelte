<script context="module">
	// import Number from './Number.svelte';
	//634649

	let locale;
	export async function load({ fetch, params }) {
		const apiKey = import.meta.env.VITE_API_KEY;
		console.log(params);
		const res =
			await fetch(`https://api.themoviedb.org/3/movie/${params.id}/credits?api_key=${apiKey}&language=en-US
`);
		const cast = await res.json();

		console.log(cast);

		if (res.ok) {
			return {
				props: { cast }
			};
		}
	}
</script>

<script>
	export let movieDetail;
	const number = movieDetail.budget;
	import { fly } from 'svelte/transition';
	import.meta.env.VITE_API_KEY;
</script>
