<script lang="ts">
	import Container from '$lib/components/Container.svelte';
</script>

<footer class="mt-32">
	<Container outer>
		<div class="border-t border-zinc-100 pb-16 pt-10 dark:border-zinc-700/40">
			<Container inner>
				<div class="flex flex-col items-center justify-between gap-6 sm:flex-row">
					<div class="flex gap-6 text-sm font-medium text-zinc-800 dark:text-zinc-200">
						<a class="transition hover:text-teal-500 dark:hover:text-teal-400" href="/about">About</a>
						<a class="transition hover:text-teal-500 dark:hover:text-teal-400" href="/projects">Projects</a>
						<a class="transition hover:text-teal-500 dark:hover:text-teal-400" href="/speaking">Speaking</a>
						<a class="transition hover:text-teal-500 dark:hover:text-teal-400" href="/uses">Uses</a>
					</div>
					<p class="text-sm text-zinc-400 dark:text-zinc-500">
						&copy; {new Date().getFullYear()} Spencer Sharp. All rights reserved.
					</p>
				</div>
			</Container>
		</div>
	</Container>
</footer>
