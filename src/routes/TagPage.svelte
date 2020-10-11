<script>
	import { Router, Route, createHistory } from "svelte-navigator";
	import PackageList from "../components/PackageList.svelte";

	export let fetchTags;
	export let fetchData;

	async function fetchTag(tag) {
		return (await fetchTags).find(_ => _.name === tag);
	}

	async function fetchPackagesTagged(tag) {
		return (await fetchData).filter(_ => _.tags.indexOf(tag) !== -1);
	}
</script>

<Route path=":tag" let:params>
	<div class="tag-page">
		{#await fetchTag(params.tag)}
			<h1>Fetching Tag...</h1>
		{:then tag}
			<h2>{tag.name}</h2>
			<p>{tag.description}</p>

			<h3>Packages With This Tag</h3>

			{#await fetchPackagesTagged(params.tag)}
				<h1>Fetching Package...</h1>
			{:then packages}
				<PackageList packages={packages} />
			{:catch error}
				<p>Error: <code>{error}</code></p>
			{/await}
		{:catch error}
			<p>Error: <code>{error}</code></p>
		{/await}
	</div>
</Route>

<style lang="scss">
	.tag-page {
		position: relative;

		padding: 20px;
	}

	h2 {
		margin: 0;

		font-size: 40pt;
	}

	h3 {
		margin-top: 50px;
		margin-bottom: 20px;

		font-size: 20pt;
	}

	p {
		font-size: 14pt;
	}
</style>
