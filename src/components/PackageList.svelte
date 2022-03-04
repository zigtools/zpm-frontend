<script>
	import Package from "./Package.svelte";
	import Fuse from "fuse.js";
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
				const fuse = new Fuse(packages, {
					keys: ["name", "author", "description"],
					includeScore: true,
				});
				const result = fuse.search(searchValue || "");
				filtered_packages = result
					.filter((x) => x.score <= 0.2)
					.map((x) => x.item);
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
