<script lang="ts">
	import Container from '$lib/components/Container.svelte';
	import avatarImage from '$lib/assets/avatar.jpg';
	import { page } from '$app/stores';
	import DesktopNavigation from './DesktopNavigation.svelte';
	import ModeToggle from './ModeToggle.svelte';
	import MobileNavigation from './MobileNavigation.svelte';

	$: isHomePage = $page.url.pathname === '/';
	let headerRef: HTMLDivElement;
	let avatarRef: HTMLDivElement;
</script>

<!-- insert bind:this={headerRef} in header -->
<header class="pointer-events-none relative z-50 flex flex-col" style="--header-height: var(--header-height); --header-mb: var(--header-mb);">
	{#if isHomePage}
		<div bind:this={avatarRef} class="order-last mt-[calc(theme(spacing.16)-theme(spacing.3))]" />
		<!-- Equivalent of OuterContainer -->
		<div class="sm:px-8 top-0 order-last -mb-3 pt-3" style="position: var(--header-position);">
			<div class="mx-auto max-w-7xl lg:px-8">
				<!-- Equivalent of InnerContainer -->
				<div class="relative px-4 sm:px-8 lg:px-12">
					<div class="mx-auto max-w-2xl lg:max-w-5xl">
						<div class="top-[var(--avatar-top,theme(spacing.3))] w-full" style="position: var(--header-inner-position);">
							<div class="relative">
								<div
									class="absolute left-0 top-3 origin-left transition-opacity h-10 w-10 rounded-full bg-white/90 p-0.5 shadow-lg shadow-zinc-800/5 ring-1 ring-zinc-900/5 backdrop-blur dark:bg-zinc-800/90 dark:ring-white/10"
									style="opacity: var(--avatar-border-opacity, 0); transform: var(--avatar-border-transform);" />
								<a href="/" aria-label="Home" class="pointer-events-auto block h-16 w-16 origin-left">
									<img src={avatarImage} alt="" sizes="4rem" class={'rounded-full bg-zinc-100 object-cover dark:bg-zinc-800 h-16 w-16'} />
								</a>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	{/if}
	<div class="top-0 z-10 h-16 pt-6" style="position: var(--header-position);">
		<!-- Equivalent of OuterContainer -->
		<div class="sm:px-8 top-[var(--header-top,theme(spacing.6))] w-full" style="position: var(--header-inner-position);">
			<div class="mx-auto max-w-7xl lg:px-8">
				<!-- Direct equivalent of InnerContainer -->
				<div class="relative px-4 sm:px-8 lg:px-12">
					<div class="mx-auto max-w-2xl lg:max-w-5xl">
						<div class="relative flex gap-4">
							<div class="flex flex-1">
								{#if !isHomePage}
									<div
										class="h-10 w-10 rounded-full bg-white/90 p-0.5 shadow-lg shadow-zinc-800/5 ring-1 ring-zinc-900/5 backdrop-blur dark:bg-zinc-800/90 dark:ring-white/10">
										<a href="/" aria-label="Home" class="pointer-events-auto">
											<img src={avatarImage} alt="" sizes="2.25rem" class="rounded-full bg-zinc-100 object-cover dark:bg-zinc-800 h-9 w-9" />
										</a>
									</div>
								{/if}
							</div>
							<div class="flex flex-1 justify-end md:justify-center">
								<!-- <MobileNavigation /> -->
								<DesktopNavigation />
							</div>
							<div class="flex justify-end md:flex-1">
								<div class="pointer-events-auto">
									<ModeToggle />
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</header>
{#if isHomePage}
	<div style="height: var(--content-offset);" />
{/if}
