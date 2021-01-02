<script>
	import { Route } from "svelte-navigator";
	import PackageList from "../components/PackageList.svelte";

	export let fetchData;

	async function fetchPackagesByAuthor(user) {
		let data = await fetchData;
		let result = data.filter((_) => _.author == user);
		return result;
	}
</script>

<Route path=":author" let:params>
	<div class="tag-page">
		<h2>{params.author}</h2>
		<h3>Packages from this author</h3>

		{#await fetchPackagesByAuthor(params.author)}
			<h1>Fetching Packages...</h1>
		{:then packages}
			<PackageList {packages} />
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
		font-weight: 300;
		font-size: 14pt;
	}

	p {
		font-size: 14pt;
	}
</style>
