<script>
	export let tv;
</script>

<div class="movie-card">
	<a sveltekit:prefetch sveltekit:noscroll href={`/tv/${tv.id}`}>
		<img src={`https://image.tmdb.org/t/p/w500${tv.poster_path}`} alt={tv.name} />
	</a>
	<div class="description">
		<h2>{tv.name}</h2>
		<p>{tv.first_air_date}</p>
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

		justify-content: center;
	}
</style>
