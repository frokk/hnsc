<script>
	import moment from "moment";
	export let user;
</script>

<div>
	<div>User: {user.username}</div>
	<div>Karma: {user.karma}</div>
	<div>Joined On: {moment(user.created_at).format('MMMM DD YYYY, h:mm:ss a')} ({moment(user.created_at, "YYYYMMDD").fromNow()})</div>
	<div>Updated On: {moment(user.updated_at).format('MMMM DD YYYY, h:mm:ss a')} ({moment(user.updated_at, "YYYYMMDD").fromNow()})</div>
	<div>Posts: {user.submission_count}</div>
</div>

<style>
	div {
		text-align: left;
		color: #fff;
	}
</style>