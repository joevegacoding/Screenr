<script>
	import global_style from '../global_style.css';
	import SearchMovies from '../components/SearchMovies.svelte';
	import Logo from '../assets/Logo.png';
</script>

<nav>
	<div class="logo">
		<a href="/"><img src={Logo} alt="" /></a>
	</div>

	<SearchMovies />

	<ul class="nav-links">
		<li><a href="">Movies</a></li>
		<li><a href="">Tv Shows</a></li>
		<li><a href="">People</a></li>
		<li><a href="">News</a></li>
	</ul>

	<div class="burger">
		<div class="line1" />
		<div class="line2" />
		<div class="line3" />
	</div>
</nav>
<div class="line" />

<style>
	nav {
		display: flex;
		min-height: 10vh;
		align-items: center;
		justify-content: space-between;
		background-color: #151515;
		margin-bottom: 7vh;
		padding: 5px 15px;
	}
	.logo {
		color: #fff;
		margin-left: 17px;
	}

	.logo img {
		width: 80%;
	}

	a {
		font-size: 1rem;
		font-weight: bold;
		font-family: 'Nunito', sans-serif;
		text-decoration: none;
		color: #fff;
		letter-spacing: 3px;
	}

	.nav-links {
		display: flex;
		justify-content: space-between;
		width: 30%;
		list-style: none;
		margin-right: 5rem;
	}
	@media screen and (max-width: 1080px) {
		.nav-links {
			width: 35%;
			margin-right: 2rem;
		}
	}

	.nav-links a {
		font-size: 0.9rem;
	}
	.burger {
		display: none;
	}
	.burger div {
		width: 30px;
		height: 3px;
		background-color: #fff;
		margin: 5px;
	}

	/* @media screen and (max-width: 768); */
</style>
