<script>
	import Footer from './lib/Footer.svelte'
	import Spinner from './lib/Spinner.svelte';
	import NewsPage from './lib/NewsPage.svelte';
	import UserPage from './lib/UserPage.svelte';

	import { onMount } from 'svelte';

	let IsLoadingData = true;
	let fetchedPosts = null;
	let fetchedUser = null;
	let QueryUsername;
	let IsUserPage = false;

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
		if (QueryUsername != "" && QueryUsername != null && QueryUsername != undefined) {
			IsUserPage = true;
		}
		if (IsUserPage == true) {
			let data = null;
			try {
				const response = await fetch(`https://hn.algolia.com/api/v1/users/${QueryUsername}`);
				data = await response.json()
				fetchedUser = data;
				IsLoadingData = false;
			} catch (err) {
				console.log(err);
				fetchedPosts = null;
			} finally {
				console.log(data);
			}
		} else {
			let data = null;
			try {
				const response = await fetch('https://hn.algolia.com/api/v1/search_by_date?tags=story,front_page');
				data = await response.json()
				fetchedPosts = data.hits;
				IsLoadingData = false;
			} catch (err) {
				console.log(err);
				fetchedPosts = null;
			} finally {
				console.log(data);
			}
		}
	})
</script>

<main>
	<h1>Hacker News</h1>
	{#if IsLoadingData == true}
		<Spinner />
	{:else}
		{#if IsUserPage == true}
			<UserPage user={fetchedUser} />
		{:else}
			<NewsPage posts={fetchedPosts}/>
		{/if}
	{/if}
</main>
<Footer />

<style>
	main {
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
		max-width: 14rem;
	}

	@media (min-width: 480px) {
		h1 {
			max-width: none;
		}
	}
</style>
