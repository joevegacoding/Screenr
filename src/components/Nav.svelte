<script>
	// 	let navWidth = 0;
	let navOpen = false;

	function handleNav() {
		navOpen = !navOpen;
		// 		navWidth === 0 ? navWidth = 40 : navWidth = 0;
	}

	function handleNavWithKey(e) {
		console.log(e.code);
		if (e.code === 'F1') {
			navOpen = !navOpen;
		}
	}

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
		<li><a href="">TV Shows</a></li>
		<li><a href="">People</a></li>
		<li><a href="">News</a></li>
	</ul>
	<div id="mySidenav" class="sidenav" class:open={navOpen}>
		<a href="#a" class="closebtn" on:click={handleNav}>&times;</a>
		<a href="#b">Movies</a>
		<a href="#c">TV Shows</a>
		<a href="#d">People</a>
		<a href="#e">News</a>
	</div>

	<div class="container" class:change={navOpen} on:click={handleNav}>
		<div class="bar1" />
		<div class="bar2" />
		<div class="bar3" />
	</div>
</nav>

<!-- Use keyboard to handle the sidenav -->
<svelte:window on:keydown={handleNavWithKey} />

<style>
	nav {
		display: flex;
		min-height: 10vh;
		align-items: center;
		justify-content: space-between;
		background-color: #151515;
		margin-bottom: 4vh;
		padding: 5px 15px;
	}

	.logo {
		color: #fff;
		margin-left: 17px;
		display: flex;
	}

	.logo img {
		width: 50%;
	}

	a {
		font-size: 1rem;
		font-weight: bold;
		font-family: 'Nunito', sans-serif;
		text-decoration: none;
		color: #fff;
		letter-spacing: 1px;
		text-transform: uppercase;
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

	@media screen and (max-width: 820px) {
		.nav-links {
			width: 65%;
			margin-right: 0.5rem;
		}
		.logo img {
			width: 80%;
		}
		.logo {
			color: #fff;
		}
	}

	.nav-links a {
		font-size: 0.9rem;
	}
	.burger {
		display: none;
	}
	.burger div {
		width: 25px;
		height: 3px;
		background-color: #fff;
		margin: 5px 2px 5px 5px;
	}

	@media screen and (max-width: 768px) {
		.nav-links li {
			opacity: 0;
		}

		.logo {
			margin-left: 0;
		}

		.logo img {
			width: 60%;
		}
	}

	/* Hamburger Menu icon */
	.container {
		display: none;
		position: absolute;
		right: 4%;
		/* display: inline-block; */
		cursor: pointer;
	}

	@media screen and (max-width: 768px) {
		.container {
			display: block;
			/* background-color: #fff; */
		}
	}

	.bar1,
	.bar2,
	.bar3 {
		width: 35px;
		height: 4px;
		background-color: #fff;
		margin: 6px 0;
		transition: 0.4s;
	}

	.change .bar1 {
		-webkit-transform: rotate(-45deg) translate(-9px, 6px);
		transform: rotate(-45deg) translate(-6px, 6px);
	}

	.change .bar2 {
		opacity: 0;
	}

	.change .bar3 {
		-webkit-transform: rotate(45deg) translate(-8px, -8px);
		transform: rotate(45deg) translate(-8px, -8px);
	}

	/* The side navigation menu */
	.sidenav {
		height: 110%;
		width: 0;
		position: fixed;
		z-index: 1;
		top: 0;
		left: 0;
		background-color: #151515f7;
		overflow-x: hidden; /* Disables horizontal scroll */
		padding-top: 80px;
		transition: 0.5s;
	}

	/* The navigation menu links */
	.sidenav a {
		padding: 20px 8px 20px 32px;
		text-decoration: none;
		font-size: 15px;
		color: #fff;
		display: block;
		transition: 0.3s;
	}

	/* When you mouse over the navigation links, change their color */
	.sidenav a:hover {
		color: #d0d0d0;
	}

	/* Position and style the close button (top right corner) */
	.sidenav .closebtn {
		position: absolute;
		top: 0;
		right: 25px;
		font-size: 36px;
		margin-left: 50px;
	}

	/* Style page content - use this if you want to push the page content to the right when you open the side navigation */
	#main {
		transition: all 0.5s;
		padding: 20px;
	}

	.pushMainToRight {
		margin-left: 40%;
		/* 	transform: translate3d(40%, 0, 0); */
	}

	.open {
		width: 40%;
	}

	/* On smaller screens, where height is less than 450px, change the style of the sidenav (less padding and a smaller font size) */
	@media screen and (max-height: 450px) {
		.sidenav {
			padding-top: 15px;
		}
		.sidenav a {
			font-size: 18px;
		}
	}
</style>
