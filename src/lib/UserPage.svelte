<script>
	import { onMount } from 'svelte';
	import moment from "moment";
	import Spinner from './Spinner.svelte';
	export let UserName;

	let user;
	let IsLoading = true;

	onMount(async () => {
		try {
			const response = await fetch(`https://hn.algolia.com/api/v1/users/${UserName}`);
			let data = await response.json()
			user = data;
			IsLoading = false;
		} catch (err) {
			console.log(err);
		} finally {
		}
	})
</script>

{#if IsLoading == true || UserName == undefined}
	<Spinner />
{:else}
	<div>
		<div>User: {user.username}</div>
		<div>Karma: {user.karma}</div>
		<div>Joined On: {moment(user.created_at).format('MMMM DD YYYY, h:mm:ss a')} ({moment(user.created_at, "YYYYMMDD").fromNow()})</div>
		<div>Updated On: {moment(user.updated_at).format('MMMM DD YYYY, h:mm:ss a')} ({moment(user.updated_at, "YYYYMMDD").fromNow()})</div>
		<div>Posts: {user.submission_count}</div>
	</div>
{/if}

<style>
	div {
		text-align: left;
		color: #fff;
	}
</style>