<script>
	import Package from "./Package.svelte";
	import { onMount } from "svelte";
	import { searchQuery } from "../stores.js";

	export let packages;
	packages.sort((a, b) => {
		return a.name.toLowerCase().localeCompare(b.name.toLowerCase());
	});

	let filtered_packages = packages;

	onMount(() => {
		searchQuery.subscribe((searchValue) => {
			console.log(packages);
			if (searchValue == null || searchValue === "") {
				filtered_packages = packages;
			} else {
				filtered_packages = packages.filter(
					(pkg) =>
						pkg.name.toLowerCase().indexOf(searchValue) !== -1 ||
						pkg.description.toLowerCase().indexOf(searchValue) !==
							-1 ||
						pkg.tags.indexOf(searchValue) !== -1
				);
			}
		});
	});
</script>

<section>
	<div class="packages">
		{#each filtered_packages as pkg}
			<Package {pkg} />
		{/each}
	</div>
</section>

<style lang="scss">
	.packages {
		display: grid;
		gap: 10px;
		grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
		grid-auto-rows: 1fr;

		margin-top: 20px;
	}
</style>
