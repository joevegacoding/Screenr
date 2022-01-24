<script context="module">
	import Number from './Number.svelte';
	let locale;
	export async function load({ fetch, params }) {
		console.log(params);
		const res =
			await fetch(`https://api.themoviedb.org/3/movie/${params.id}?api_key=6c585d930b6b55e72e3e31c6506a6ee4&language=en-US
`);
		const movieDetail = await res.json();

		console.log(movieDetail);

		if (res.ok) {
			return {
				props: { movieDetail }
			};
		}
	}
</script>

<script>
	export let movieDetail;
	const number = movieDetail.budget;
	import { fly } from 'svelte/transition';
</script>

<div
	class="movie-details"
	in:fly={{ y: 50, duration: 500, delay: 500 }}
	out:fly={{ duration: 500 }}
>
	<div class="img-container">
		<img
			src={`https://image.tmdb.org/t/p/original${movieDetail.backdrop_path}`}
			alt={movieDetail.title}
		/>
	</div>
	<div class="text-container">
		<h1>{movieDetail.title}</h1>
		<p class="overview">{movieDetail.overview}</p>
		<p>
			<span>Release Date: </span>{movieDetail.release_date} <br />
			<span>Budget: </span>$<Number {number} {locale} /> <br />
			<span>Rating: </span>{movieDetail.vote_average}/10<br />
			<span>Runtimers: </span>{movieDetail.runtime}mins
		</p>
	</div>
</div>

<style>
	h1 {
		padding: 1rem 0rem 2rem;
	}

	p {
		padding: 1rem 0rem;
	}

	img {
		width: 100%;
		border-radius: 1rem;
	}

	.movie-details {
		margin: 2rem 10%;
	}

	span {
		font-weight: bold;
	}
</style>
