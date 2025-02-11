<script lang="ts">
	import Bounded from '$lib/components/Bounded.svelte';
	import Heading from '$lib/components/Heading.svelte';
	import type { Content } from '@prismicio/client';
	import { PrismicRichText } from '@prismicio/svelte';

	export let slice: Content.ExperienceSlice;
</script>

<Bounded data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
	<Heading tag="h2" size="lg">
		{slice.primary.heading}
	</Heading>
	{#each slice.primary.items as items}
		<div class="ml-6 mt-8 max-w-prose md:ml-12 md:mt-16">
			<Heading tag="h3" size="sm">
				{items.position}
			</Heading>

			<div class="mt-1 flex w-fit items-center gap-1 text-2xl font-semibold tracking-light text-slate-600">
				<span>{items.year}</span> {' '}
				<span class="text-3xl font-extralight">/</span> {' '}
				<span>{items.position}</span>
			</div>

			<div class="text-justify prose prose-xl prose-invert mt-4">
				<PrismicRichText field={items.description} />
			</div>
		</div>
	{/each}
</Bounded>
