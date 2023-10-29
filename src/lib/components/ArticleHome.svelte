<script lang="ts">
	import type { PageData } from '../../routes/$types';
	import ChevronRightIcon from '$lib/assets/logos/chevron-right-icon.svelte';
	export let meta: {
		path: string;
		author: string;
		date: string;
		title: string;
		description: string;
	};

	const formattedDate = new Date(`${meta.date}T00:00:00Z`).toLocaleDateString('en-US', {
		day: 'numeric',
		month: 'long',
		year: 'numeric',
		timeZone: 'UTC'
	});
</script>

<article class="group relative flex flex-col items-start">
	<h2 class="text-base font-semibold tracking-tight text-zinc-800 dark:text-zinc-100">
		<div
			class="absolute -inset-x-4 -inset-y-6 z-0 scale-95 bg-zinc-50 opacity-0 transition group-hover:scale-100 group-hover:opacity-100 dark:bg-zinc-800/50 sm:-inset-x-6 sm:rounded-2xl" />
		<a href={meta.path.replace(/(\/index)?\.md$/, '')}
			><span class="absolute -inset-x-4 -inset-y-6 z-20 sm:-inset-x-6 sm:rounded-2xl" /><span class="relative z-10">{meta.title}</span></a>
	</h2>
	<time class="relative z-10 order-first mb-3 flex items-center text-sm text-zinc-400 dark:text-zinc-500 pl-3.5" datetime="2023-10-20"
		><span class="absolute inset-y-0 left-0 flex items-center" aria-hidden="true"
			><span class="h-4 w-0.5 rounded-full bg-zinc-200 dark:bg-zinc-500" /></span
		>{formattedDate}</time>
	<p class="relative z-10 mt-2 text-sm text-zinc-600 dark:text-zinc-400">
		{meta.description}
	</p>
	<div aria-hidden="true" class="relative z-10 mt-4 flex items-center text-sm font-medium text-teal-500">Read article<ChevronRightIcon /></div>
</article>
