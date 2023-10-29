<script lang="ts">
	import { page } from '$app/stores';
	import '../app.postcss';
	import Header from '$lib/components/Header.svelte';
	import Footer from '$lib/components/Footer.svelte';

	export let errorPage: boolean = false;
	$: errorPage = $page.error?.message === 'Not Found';
</script>

<svelte:body class="bro" />

<div class="fixed inset-0 flex justify-center sm:px-8">
	<div class="flex w-full max-w-7xl lg:px-8">
		<div class="w-full bg-white ring-1 ring-zinc-100 dark:bg-zinc-900 dark:ring-zinc-300/20" />
	</div>
</div>
<div class={`relative ${errorPage ? 'flex w-full flex-col' : ''}`}>
	<Header />
	<main class:flex-auto={errorPage}>
		<slot />
	</main>
	<Footer />
</div>
