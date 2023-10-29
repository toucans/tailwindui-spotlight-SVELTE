<script lang="ts">
	import Card from './Card.svelte';

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

<article class="md:grid md:grid-cols-4 md:items-baseline">
	<Card classStr="md:col-span-3">
		<Card Title href={`/articles/${meta.path.replace(/(\/index)?\.md$/, '')}`}>
			{meta.title}
		</Card>
		<Card Description>{meta.description}</Card>
		<Card Cta>Read article</Card>
	</Card>
	<Card Eyebrow eyebrowAs="time" datetime={meta.date} classStr="mt-1 hidden md:block">
		{formattedDate}
	</Card>
</article>
