<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import { Player, Video } from '@vime/svelte';
	import fetchStore from '../../../fetch';

	let {
		params: { imdbId }
	}: any = $page;

	let url = `http://4.tcp.eu.ngrok.io:14048/api/content/${imdbId}`;
	let data: any, loading, error;

	onMount(async () => {
		[data, loading, error] = fetchStore(url);
	});
</script>

{#if $loading}
	Loading
{:else if $error}
	Error: {$error}
{:else if $data}
	<div>
		<div class="navbar">
			<a href="/" class="landing-title"><h1>portal</h1></a>
			<h1 class="movie-title">{$data.name}</h1>
		</div>
		{#if $data.seasons}
			i'm to tired to handle tv series
		{:else}
			<Player controls>
				<Video crossorigin="" poster={$data.thumbnail}>
					<source data-src={$data.url} />
					{#each $data.subtitles.en as subtitle}
						<track kind="subtitles" src={subtitle} srclang="en" label="English" />
					{/each}
					{#each $data.subtitles.tr as subtitle}
						<track kind="subtitles" src={subtitle} srclang="tr" label="Turkish" />
					{/each}
				</Video>
			</Player>
		{/if}
	</div>
{/if}

<style>
	:global(body) {
		color: #f4f4f5;
		letter-spacing: 1px;
		background-color: #18181b;
		font-family: Helvetica, Arial, sans-serif;
	}

	.navbar {
		display: flex;
		position: relative;
		justify-content: center;
	}

	.landing-title {
		display: inline-flex;
		color: inherit;
		text-decoration: none;
		position: absolute;
		left: 15px;
	}

	.movie-title {
		color: #ff2f67;
		display: inline-flex;
		justify-content: center;
		text-align: center;
	}
</style>
