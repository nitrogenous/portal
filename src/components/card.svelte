<script lang="ts">
	import { redirect } from '@sveltejs/kit';

	export let imdbId: string;
	export let name: string;
	export let thumbnail: string | undefined;

	const redirectToContent = () => {
		console.log(123);
		redirect(302, `/content/${imdbId}`);
	};
</script>

<a href={`/content/${imdbId}`}>
	<div id={imdbId} class="card-wrapper">
		<img
			src={thumbnail}
			alt={`thumbnail of ${name}`}
			on:error={() => {
				thumbnail = '/defaultMovie.png';
			}}
		/>
		<span>{name}</span>
	</div>
</a>

<style>
	a {
		text-decoration: none;
		color: inherit;
	}

	.card-wrapper {
		width: 200px;
		min-width: 200px;
		max-width: 200px;
		overflow: hidden;
		margin: 2.5px;
		text-align: center;
		border-radius: 5px;
		display: inline-flex;
		flex-direction: column;
		height: 375px;
		min-height: 375px;
		max-height: 375px;
		background-color: #52525b;
	}

	.card-wrapper:hover {
		cursor: pointer;
		filter: drop-shadow(0px 4px 6px #ff2f67);
	}

	img {
		width: 200px;
		height: 300px;
		min-height: 300px;
		max-height: 300px;
	}

	span {
		height: 75px;
		display: flex;
		font-size: 17px;
		align-items: center;
		justify-content: center;
	}
</style>
