<script>
	import '../app.css';
	import '@fontsource-variable/urbanist';
	import { PrismicPreview } from '@prismicio/svelte/kit';
	import { page } from '$app/stores';
	import { repositoryName } from '$lib/prismicio';
	import Footer from '$lib/components/Footer.svelte';
	import Header from '$lib/components/Header.svelte';

	export let data;
</script>

<svelte:head>
	<title>{$page.data.title}</title>
	{#if $page.data.meta_description}
		<meta name="description" content={$page.data.meta_description} />
	{/if}
	{#if $page.data.meta_title}
		<meta name="og:title" content={$page.data.meta_title} />
	{/if}
	{#if $page.data.meta_image}
		<meta name="og:image" content={$page.data.meta_image} />
		<meta name="twitter:card" content="summary_large_image" />
	{/if}
</svelte:head>

<Header settings={data.settings} />
<main>
	<slot />
</main>

<div class="bg-gradient-to-r from-purple-500 to-pink-500 opacity-50 absolute inset-0 -z-50 max-h-screen" />


<Footer settings={data.settings}/>

<PrismicPreview {repositoryName} />
