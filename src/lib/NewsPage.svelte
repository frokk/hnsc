<script>
	import { onMount } from "svelte";
	import NewsCard from "./NewsCard.svelte";
	import Spinner from './Spinner.svelte';

	let posts = null;
	let IsLoadingData = true;

	onMount(async () => {
		let data = null;
		try {
			const response = await fetch('https://hn.algolia.com/api/v1/search_by_date?tags=story,front_page');
			data = await response.json()
			posts = data.hits;
			IsLoadingData = false;
		} catch (err) {
			console.log(err);
			posts = null;
		} finally {
		}
	});
</script>

{#if IsLoadingData == true}
	<Spinner />
{:else}
	<div class="posts">
		{#each posts as post}
			<NewsCard post={post} />
		{/each}
	</div>
{/if}

<style>
	.posts {
		text-align: left;
		min-height: calc(100vh - 11.2rem)
	}
</style>