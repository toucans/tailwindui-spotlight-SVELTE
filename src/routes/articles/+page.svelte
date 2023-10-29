<script lang="ts">
	import Article from '$lib/components/Article.svelte';
	import SimpleLayout from '$lib/components/SimpleLayout.svelte';

	// import type { PageData } from './$types';
	// export let data: PageData;
	interface IArticle {
		author: string;
		date: string;
		title: string;
		description: string;
	}
	interface IArticleWithPath extends IArticle {
		path: string;
	}
	const am = import.meta.glob('./**/*.md', { eager: true });
	const articlesArray: IArticleWithPath[] = Object.entries(am).map(([path, articleData]) => {
		const { metadata } = articleData as { metadata: IArticle };
		return { path, ...metadata };
	});
</script>

<svelte:head>
	<title>Articles - Spencer Sharp</title>
	<meta
		name="description"
		content="All of my long-form thoughts on programming, leadership, product design, and more, collected in chronological order." />
</svelte:head>
<SimpleLayout
	title="Writing on software design, company building, and the aerospace industry."
	intro="All of my long-form thoughts on programming, leadership, product design, and more, collected in chronological order.">
	<div class="md:border-l md:border-zinc-100 md:pl-6 md:dark:border-zinc-700/40">
		<div class="flex max-w-3xl flex-col space-y-16">
			{#each articlesArray as meta}
				<Article {meta} />
			{/each}
		</div>
	</div>
</SimpleLayout>
