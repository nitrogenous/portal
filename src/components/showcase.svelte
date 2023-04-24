<script lang="ts">
	import Card from './card.svelte';

	export let showcaseTitle: string;
	export let showcaseItems: any[];
</script>

<div class="showcase-wrapper">
	<span>{showcaseTitle}</span>
	<div class="showcase-items">
		{#each showcaseItems as item}
			<Card imdbId={item.imdbId} name={item.name} thumbnail={item.thumbnail} />
		{/each}
	</div>
</div>

<style>
	span {
		margin: 10px 15px;
		font-size: 23px;
		font-weight: bold;
	}

	.showcase-wrapper {
		display: flex;
		margin: 10px;
		padding: 10px 15px;
		border-radius: 5px;
		flex-direction: column;
		background-color: #27272a;
	}
</style>
