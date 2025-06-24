<script lang="ts">
	import { formatDate } from '$lib/utils';

	let { data } = $props();
</script>

<svelte:head>
	<title>Posts in category: {data.category}</title>
</svelte:head>

<section>
	<h1>Posts in category: &num;{data.category}</h1>
	<ul class="posts">
		{#each data.posts as post}
			<li class="post">
				<a href="/{post.slug}" class="title">{post.title}</a>
				<p class="date">{formatDate(post.date)}</p>
				<p class="description">{post.description}</p>
			</li>
		{/each}
	</ul>
</section>

<style>
	h1 {
		text-transform: capitalize;
	}
	.posts {
		display: grid;
		gap: var(--size-7);
		margin-top: var(--size-7);

		.post {
			max-inline-size: var(--size-content-3);
			margin-top: var(--size-5);

			&:not(:last-child) {
				border-bottom: 1px solid var(--border);
				padding-bottom: var(--size-7);
			}

			.title {
				font-size: var(--font-size-fluid-3);
				text-transform: capitalize;
			}

			.date {
				color: var(--text-2);
			}

			.description {
				margin-top: var(--size-3);
			}
		}
	}
</style>
