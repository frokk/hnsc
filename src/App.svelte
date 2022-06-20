<script>
	import Footer from './lib/Footer.svelte'
	import NewsPage from './lib/NewsPage.svelte';
	import UserPage from './lib/UserPage.svelte';
	import PostPage from './lib/PostPage.svelte';
	import { onMount } from 'svelte';

	let QueryUsername;
	let QueryPost;
	let IsReady = false; // To Prevent From Un-necessary Rendering
	let IsUserPage = false;
	let IsPostPage = false;

	function getURLParam(name) {
		var url = window.location.href;
		name = name.replace(/[\[\]]/g, '\\$&');
		var regex = new RegExp('[?&]' + name + '(=([^&#]*)|&|#|$)');
		var results = regex.exec(url);
		if (!results) return null;
		if (!results[2]) return '';
		return decodeURIComponent(results[2].replace(/\+/g, ' '));
	}

	onMount(async function() {
		QueryUsername = getURLParam("user");
		QueryPost = getURLParam("post");
		if (QueryUsername != "" && QueryUsername != null && QueryUsername != undefined) {
			IsUserPage = true;
		} else if (QueryPost != "" && QueryPost != null && QueryPost != undefined) {
			IsPostPage = true;
		}
		IsReady = true;
	})
</script>

<main>
	<h1>Hacker News</h1>
	{#if IsReady == true}
		{#if IsUserPage == true}
			<UserPage UserName={QueryUsername} />
		{:else if IsPostPage == true}
			<PostPage PostID={QueryPost} />
		{:else}
			<NewsPage />
		{/if}
	{/if}
</main>
<Footer />

<style>
	main {
		padding: 10px;
		position: relative;
		text-align: center;
		margin: 2rem auto 0.8rem auto;
		min-height: calc(100vh - 100px);
		max-width: 50rem; /* 50rem = 800px */
	}

	h1 {
		color: var(--fg);
		text-transform: uppercase;
		font-size: 4rem;
		font-weight: 100;
		line-height: 1.1;
		margin: 0 auto 2rem auto;
	}

	@media (max-width: 470px) {
		h1 {
			font-size: 2.5rem;
		}
	}
</style>
