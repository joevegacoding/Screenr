<script context="module">
	import Number from './Number.svelte';

	let locale;
	export async function load({ fetch, params }) {
		const apiKey = import.meta.env.VITE_API_KEY;
		console.log(params);
		const res =
			await fetch(`https://api.themoviedb.org/3/movie/${params.id}?api_key=${apiKey}&language=en-US
`);

		const castRes = await fetch(
			`https://api.themoviedb.org/3/movie/${params.id}/credits?api_key=${apiKey}&language=en-US`
		);
		const movieDetail = await res.json();
		const castDetail = await castRes.json();
		const casts = castDetail.cast;
		console.log(movieDetail);
		console.log(casts);

		if (res.ok && castRes.ok) {
			return {
				props: { movieDetail, castDetail }
			};
		}
	}
</script>

<script>
	export let movieDetail;
	export let castDetail;
	const number = movieDetail.budget;
	import { fly } from 'svelte/transition';
	import.meta.env.VITE_API_KEY;
</script>

<div in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }} class="card">
	<header class="card__gallery">
		<div class="card__gallery-item card__gallery-item__main">
			<img
				src={`https://image.tmdb.org/t/p/original${movieDetail.backdrop_path}`}
				alt={movieDetail.title}
			/>
		</div>
	</header>
	<main class="card__user">
		<img
			src={`https://image.tmdb.org/t/p/original${movieDetail.poster_path}`}
			alt={movieDetail.title}
			class="card__user-image"
		/>
		<div class="card__user-info">
			<h2 class="card__user-info__name">{movieDetail.title}</h2>

			<p class="card__user-info__stats">⭐️ {movieDetail.vote_average}/10</p>
			<p class="card__user-info__desc">{movieDetail.tagline}</p>
		</div>
		<div class="card__user-actions">
			<h2>Overview</h2>
			<p class="card__user-info__desc">{movieDetail.overview}</p>
		</div>
	</main>
</div>
<div>
	<h2>Cast</h2>

	<div class="cast-container">
		{#each castDetail.cast as cast}
			<div {cast} class="cast-item">
				<img src={`https://image.tmdb.org/t/p/original${cast.profile_path}`} />
				<h2>{cast.name}</h2>
				<p>{cast.character}</p>
				<!-- <h2>fds</h2> -->
			</div>
		{/each}
	</div>
</div>

<style>
	h1 {
		text-align: center;
		margin-bottom: 2rem;
		color: #1abc9c;
	}
	.cast-container {
		display: flex;
		overflow-x: auto;
		padding: 3rem 2rem;
		margin: 0 1.5rem;
	}
	.cast-container::-webkit-scrollbar {
		display: none;
	}
	.cast-container .cast-item {
		margin: 8px;
		transition: 0.3s all;
	}
	.cast-container .itcast-itemem:last-of-type {
		margin-right: 8px;
	}
	.cast-container .cast-item img {
		height: 200px;
		border-radius: 15px;
		cursor: pointer;
		filter: contrast(90%);
		transition: 0.3s all;
	}
	.cast-container .cast-item img:hover {
		filter: contrast(100%);
	}
	.cast-container .cast-item:hover {
		transform: translateY(-4px);
	}

	h2 {
		color: black;
		background-color: transparent;
		font-size: 1.2rem;
	}

	ul {
		list-style: none;
	}
	button {
		font-family: inherit;
		border: none;
		background: transparent;
		cursor: pointer;
	}
	h1,
	h2,
	h3 {
		margin-top: 0;
		line-height: 1.1;
	}
	a,
	a:visited,
	a:active {
		text-decoration: none;
	}
	.card {
		width: fit-content;

		margin: 1rem 5rem;
	}
	.card__gallery {
		display: grid;
		grid-template-columns: repeat(1, 175px);
		grid-auto-rows: 175px;
	}

	.card__gallery-item__main {
		display: flex;
		justify-content: center;
		/* width: 130%; */
	}

	@media screen and (max-width: 756px) {
		.card__gallery-item__main {
			width: 100%;
		}

		.card {
			width: fit-content;

			margin: 0rem 0.7rem;
		}
		.card__gallery {
			grid-template-columns: repeat(1, 1fr);
		}
		.card__gallery :last-child {
			grid-column: span 2;
		}
	}
	@media screen and (max-width: 579px) {
		.card__gallery {
			grid-template-columns: repeat(1, 1fr);
		}
		.card__gallery :last-child {
			grid-column: unset;
		}
	}
	@media screen and (max-width: 383px) {
		.card__gallery {
			grid-template-columns: 1fr;
		}
	}
	.card__gallery-item {
		height: 175px;
		overflow: hidden;
	}

	.card__gallery-item img {
		width: 100%;
		height: 150%;
		object-fit: cover;
		/* border-radius: 3%; */
		display: block;
	}
	.card__gallery-item__main {
		grid-column: span 4;
		grid-row: span 2;
		height: auto;
	}
	@media screen and (max-width: 383px) {
		.card__gallery-item__main {
			grid-column: unset;
			grid-row: unset;
			/* border-radius: 10%; */
		}
	}
	.card__user {
		padding: 30px;
		display: flex;
		align-items: center;
	}
	@media screen and (max-width: 579px) {
		.card__user {
			flex-wrap: wrap;
			justify-content: center;
		}
	}
	@media screen and (max-width: 383px) {
		.card__user {
			padding: 15px;
		}
	}
	.card__user-image {
		/* height: auto; */
		width: 250px;
		position: relative;
		border-radius: 20px;
		object-fit: cover;
		margin-right: 20px;
		margin-top: -121px;
		border: 10px solid #fff;
	}
	@media screen and (max-width: 579px) {
		.card__user-image {
			margin-right: 0;
		}
	}
	.card__user-info {
		flex: 2;
		margin-right: 20px;
	}
	@media screen and (max-width: 579px) {
		.card__user-info {
			flex-basis: 100%;
			text-align: center;
			margin: 0;
		}
	}
	.card__user-info__name {
		font-size: 24px;
		font-weight: bold;
		margin-bottom: 16px;
	}
	.card__user-info__stats {
		font-size: 1.2rem;
		font-weight: 500;
		margin-bottom: 14px;
	}
	.card__user-info__desc {
		font-size: 14px;
		color: rgba(128, 128, 128, 0.774);
	}
	.card__user-actions {
		flex: 4;
		color: #151515;
	}

	.card__user-actions h2 {
		margin-bottom: 1rem;
	}

	.card__user-actions p {
		color: #151515;
		font-size: 1rem;
	}
	@media screen and (max-width: 579px) {
		.card__user-actions {
			margin-top: 20px;
		}
	}
	.card__user-actions button {
		display: block;
		padding-left: 20px;
		padding-right: 20px;
		padding-top: 10px;
		padding-bottom: 10px;
		width: 100%;
		border-radius: 6px;
		font-size: 14px;
		font-weight: 600;
	}
	.card__user-actions-follow {
		color: #fff;
		background-color: var(--primary-light);
		margin-bottom: 15px;
	}
	.card__user-actions-follow {
		background-color: #383a3f;
	}
	.card__user-actions-message {
		background-color: transparent;
		color: #000;
		border: 2px solid var(--primary-light);
	}
	.card__user-actions-message:hover {
		background-color: #f0f0f0;
	}
</style>
