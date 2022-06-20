<script>
	import NewsCard from "./NewsCard.svelte";
	export let posts;
</script>

<div class="posts">
	{#each posts as post}
		<NewsCard post={post} />
	{/each}
</div>

<style>
	.posts {
		text-align: left;
		min-height: calc(100vh - 11.2rem)
	}
</style>