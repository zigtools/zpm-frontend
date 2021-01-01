<script>
	import PackageList from "../components/PackageList.svelte";

	export let fetchData;
</script>

<div>
	{#await fetchData}
		<h1>Fetching Packages...</h1>
	{:then packages}
		<PackageList {packages}/>
	{:catch error}
		<p>Error: <code>{error}</code></p>
	{/await}
</div>

<style lang="scss">

	div {
		padding: 20px;
	}

</style>
