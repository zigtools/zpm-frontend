<script>
	import Package from "./Package.svelte";
	import { onMount } from "svelte";
	import { searchQuery } from "../stores.js";

	export let packages;
	packages.sort((a, b) => {
		return a.name.toLowerCase().localeCompare(b.name.toLowerCase());
	});

	let filtered_packages = packages;
	let list_limit = 30;

	function handleScroll() {
		window.onscroll = () => {
			let bottomOfWindow =
				Math.max(
					window.pageYOffset,
					document.documentElement.scrollTop,
					document.body.scrollTop
				) +
					window.innerHeight ===
				document.documentElement.offsetHeight;

			if (bottomOfWindow) {
				list_limit += 30;
			}
		};
	}

	onMount(() => {
		handleScroll();

		searchQuery.subscribe((searchValue) => {
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
				list_limit = 30;
			}
		});
	});
</script>

<section>
	<div class="packages">
		{#each filtered_packages.slice(0, list_limit) as pkg}
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
