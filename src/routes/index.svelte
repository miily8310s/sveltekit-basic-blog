<script context="module" lang="ts">
	export const load = async({ fetch }) => {
		const res = await fetch("https://jsonplaceholder.typicode.com/posts")
		const posts = await res.json()
		return {
			props: {
				posts
			}
		}
	}
</script>

<script lang="ts">
	import type { Post } from "$lib/types";
	export let posts: Post[]
</script>

<svelte:head>
	<title>Home</title>
</svelte:head>

<h1>Posts</h1>

<div class="posts">
	{#each posts as post}
		<div class="post">
			<h2>{post.title.slice(0, 20)}</h2>
			<p>{post.body}</p>
			<p class="link"><a sveltekit:prefetch href={`/blog/${post.id}`}>Read More</a></p>
		</div>
	{/each}
</div>

<style>
	.posts {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 20px;
	}
	.post {
		padding: 10px;
		border: 1px solid #ddd;
	}
	.link {
		text-align: right;
	}
</style>
