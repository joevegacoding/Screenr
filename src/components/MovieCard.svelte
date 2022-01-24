<script>
	export let movie;

	function movieClicked() {
		console.log(movie.id);
	}
</script>

<div class="movie-card">
	<a sveltekit:prefetch sveltekit:noscroll href={`/movie/${movie.id}`}>
		<img src={`https://image.tmdb.org/t/p/w500${movie.poster_path}`} alt={movie.title} />
	</a>
	<div class="description">
		<h2>{movie.title}</h2>
		<p>{movie.release_date}</p>
	</div>
</div>

<style>
	img {
		width: 80%;
		border-radius: 1rem;
		margin-bottom: 1rem;
		/* height: 50vh;
		object-fit: cover; */
	}
	h2 {
		font-size: 0.9rem;
	}

	.description {
		height: 5vh;
	}

	p {
		font-size: 0.8rem;
	}

	.movie-card {
		cursor: pointer;
	}
</style>
