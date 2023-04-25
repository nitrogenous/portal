<script lang="ts">
	import { onMount } from 'svelte';
	import fetchStore from '../fetch';
	import Showcase from '../components/showcase.svelte';

	let url = 'http://4.tcp.eu.ngrok.io:14048/api/contents';
	let data: any, loading, error;

	onMount(async () => {
		[data, loading, error] = fetchStore(url);
	});
</script>

<h1 class="landing-title">portal</h1>

{#if $loading}
	Loading
{:else if $error}
	Error: {$error}
{:else if $data}
	<Showcase showcaseTitle="Movies" showcaseItems={$data.movies} />
	<Showcase showcaseTitle="Series" showcaseItems={$data.series} />
{/if}

<style>
	:global(body) {
		color: #f4f4f5;
		letter-spacing: 1px;
		background-color: #18181b;
		font-family: Helvetica, Arial, sans-serif;
	}

	.landing-title {
		display: flex;
		justify-content: center;
		color: #ff2f67;
	}
</style>
