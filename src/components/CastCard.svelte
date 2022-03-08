<script>
	export let cast;
</script>

<div class="class-section">
	<div class="section-title" />
	<div class="cast-container">
		<div {cast} class="cast-item">
			<img src={`https://image.tmdb.org/t/p/original${cast.profile_path}`} />
			<h2>{cast.name}</h2>
			<p>{cast.character}</p>
		</div>
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
</style>
