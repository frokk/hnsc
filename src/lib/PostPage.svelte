<script>
	import { onMount } from 'svelte';
	import moment from "moment";
	import Spinner from './Spinner.svelte';
	export let PostID;

	let post;
	let IsLoading = true;

	onMount(async () => {
		try {
			const response = await fetch(`http://hn.algolia.com/api/v1/items/${PostID}`);
			let data = await response.json()
			post = data;
			IsLoading = false;
		} catch (err) {
			console.log(err);
		} finally {
		}
	})
</script>

{#if IsLoading == true || PostID == undefined}
	<Spinner />
{:else}
	<div>
		<h4>{post.title}</h4>
		<div class="postText">{@html post.text}</div>
		<div class="postInfo">
			<span class="points">{`${post.points} ${post.points == 1 ? "Point" : "Points"}`}</span> |
			<span class="author">By {post.author}</span> |
			<span class="date">Posted {moment(`${post.created_at}`).format('DD/MM/YYYY, h:mm A')} ({moment(`${post.created_at}`, "YYYYMMDD").fromNow()})</span>
		</div>
	</div>
{/if}

<style>
	div {
		text-align: left;
		color: #fff;
	}
	div.postText {
		margin: 15px 0;
	}
</style>