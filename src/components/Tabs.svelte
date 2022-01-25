<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();
	export let items;
	export let activeItem;
</script>

<div class="tabs">
	<ul>
		{#each items as item}
			<li on:click={() => dispatch('tabChanged', item)}>
				<div class:active={item === activeItem}>{item}</div>
			</li>
		{/each}
	</ul>
</div>

<style>
	.tabs {
		margin-bottom: 40px;
	}

	ul {
		display: flex;
		justify-content: flex-start;
		padding: 0;
		list-style: none;
		margin: 0;
	}

	li {
		margin: 0 1rem 0 0;
		font-size: 1.3rem;
		cursor: pointer;
	}
	.active {
		color: #e71d36;
		border-bottom: 2px solid #e71d36;
		padding-bottom: 8px;
	}
</style>
