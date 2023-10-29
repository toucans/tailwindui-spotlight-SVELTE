<script lang="ts">
	import { page } from '$app/stores';
	import Container from '$lib/components/Container.svelte';
	import { onMount } from 'svelte';
	import Layout from './+layout.svelte';

	onMount(() => {
		document.body.classList.remove('flex-col');
		return () => {
			document.body.classList.add('flex-col');
		};
	});
</script>

{#if $page.error?.message === 'Not Found'}
	<Container classStr="flex h-full items-center pt-16 sm:pt-32">
		<div class="flex flex-col items-center">
			<p class="text-base font-semibold text-zinc-400 dark:text-zinc-500">404</p>
			<h1 class="mt-4 text-4xl font-bold tracking-tight text-zinc-800 dark:text-zinc-100 sm:text-5xl">Page not found</h1>
			<p class="mt-4 text-base text-zinc-600 dark:text-zinc-400">Sorry, we couldn’t find the page you’re looking for.</p>
			<a
				class="inline-flex items-center gap-2 justify-center rounded-md py-2 px-3 text-sm outline-offset-2 transition active:transition-none bg-zinc-50 font-medium text-zinc-900 hover:bg-zinc-100 active:bg-zinc-100 active:text-zinc-900/60 dark:bg-zinc-800/50 dark:text-zinc-300 dark:hover:bg-zinc-800 dark:hover:text-zinc-50 dark:active:bg-zinc-800/50 dark:active:text-zinc-50/70 mt-4"
				href="/">Go back home</a>
		</div>
	</Container>
{:else}
	<h1>{$page.status}: {$page.error?.message}</h1>
{/if}
