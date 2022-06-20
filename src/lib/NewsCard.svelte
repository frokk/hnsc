<script>
	import moment from "moment";
	export let post;
</script>

{#if post && post.url}
<div class="NewsCard">
	<div class="NewsTitle">
		<a class="NewsTitleUrl" href={post.url}>{post.title}</a>
	</div>
	<div class="NewsInfo">
		<span>{`${post.points} ${(post.points > 1) ? "Upvotes" : "Upvote"}`} |</span>
		<span>
			Posted {moment(`${post.created_at}`, "YYYYMMDD").fromNow()} By
			<a class="NewsCardAuthor" href={`${window.location.href}?user=${post.author}`}>{post.author}</a>,
			has {post.num_comments} Comments
		</span>
	</div>
</div>
{/if}

<style>
	.NewsCard {
		display: block;
		transition: 0.1s all linear;
		margin: 10px 0;
		color: var(--fg);
	}
	.NewsCard a {
		cursor: pointer;
		text-decoration: none;
	}
	.NewsCard a:hover {
		text-decoration: underline;
	}
	.NewsCard a.NewsTitleUrl {
		color: var(--primary);
	}
	.NewsCard a.NewsCardAuthor {
		color: var(--tertiary);
	}
	.NewsCard .NewsInfo {
		text-align-last: left;
		display: block;
		font-size: 0.8rem;
	}
</style>
