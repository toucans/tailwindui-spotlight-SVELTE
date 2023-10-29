<script lang="ts">
	import Container from '$lib/components/Container.svelte';
	import { onMount } from 'svelte';
	import type { PageData } from './$types';
	import Article from '$lib/components/Article.svelte';
	import { error } from '@sveltejs/kit';
	export let data: PageData;
	import './app.css';

	interface Article {
		metadata: {
			author: string;
			date: string;
			title: string;
			description: string;
		};
	}

	let urlPath = data.params['slug'];

	const am = import.meta.glob('../*.md', { eager: true });

	let article: Article | null = null;
	let articleKey: string;
	for (const key of Object.keys(am)) {
		const modifiedKey = key.replace(/(\/index)?\.md$/, '').replace(/^.*\//, '');
		if (modifiedKey === urlPath) {
			articleKey = modifiedKey;
			article = am[key] as Article;
			break;
		}
	}

	let formattedDate: string;
	if (article) {
		formattedDate = new Date(`${article.metadata.date}T00:00:00Z`).toLocaleDateString('en-US', {
			day: 'numeric',
			month: 'long',
			year: 'numeric',
			timeZone: 'UTC'
		});
	} else {
		throw error(404, 'Not Found');
	}

	let MarkdownComponent: ConstructorOfATypedSvelteComponent;
	onMount(async () => {
		if (article) {
			const module = await import(`../${articleKey}.md`);
			MarkdownComponent = module.default;
		}
	});
</script>

{#if article}
	<Container classStr="mt-16 lg:mt-32">
		<div class="xl:relative">
			<div class="mx-auto max-w-2xl">
				<!-- {previousPathname && (
              <button
                type="button"
                onClick={() => router.back()}
                aria-label="Go back to articles"
                class="group mb-8 flex h-10 w-10 items-center justify-center rounded-full bg-white shadow-md shadow-zinc-800/5 ring-1 ring-zinc-900/5 transition dark:border dark:border-zinc-700/50 dark:bg-zinc-800 dark:ring-0 dark:ring-white/10 dark:hover:border-zinc-700 dark:hover:ring-white/20 lg:absolute lg:-left-5 lg:-mt-2 lg:mb-0 xl:-top-1.5 xl:left-0 xl:mt-0"
              >
                <ArrowLeftIcon class="h-4 w-4 stroke-zinc-500 transition group-hover:stroke-zinc-700 dark:stroke-zinc-500 dark:group-hover:stroke-zinc-400" />
              </button>
            )} -->
				<article>
					<header class="flex flex-col">
						<h1 class="mt-6 text-4xl font-bold tracking-tight text-zinc-800 dark:text-zinc-100 sm:text-5xl">
							{article.metadata.title}
						</h1>
						<time dateTime={article.metadata.date} class="order-first flex items-center text-base text-zinc-400 dark:text-zinc-500">
							<span class="h-4 w-0.5 rounded-full bg-zinc-200 dark:bg-zinc-500" />
							<span class="ml-3">{formattedDate}</span>
						</time>
					</header>
					<div class="mt-8 prose dark:prose-invert">
						<svelte:component this={MarkdownComponent} />
					</div>
				</article>
			</div>
		</div>
	</Container>
{:else}
	nah
{/if}
