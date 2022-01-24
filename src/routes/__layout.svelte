<script>
	import global_style from '../global_style.css';
	import Nav from '../components/Nav.svelte';

	let open = false;
</script>

<svlete:head>
	<title>The Movie Catalog</title>
</svlete:head>
<Nav />

<slot />
