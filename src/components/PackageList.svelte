<script>
	import Package from "./Package.svelte";

	export let packages;
	let filtered_packages = packages;
</script>

<section>
	<input type="text" placeholder="Search" on:input={e => filtered_packages = packages.filter(_ => _.name.toLowerCase().indexOf(e.target.value.toLowerCase()) !== -1 || _.tags.indexOf(e.target.value) !== -1)}>

	<div class="packages">
		{#each filtered_packages as pkg}
			<Package pkg={pkg} />
		{/each}
	</div>
</section>

<style lang="scss">
	.packages {
		display: grid;
		gap: 20px;
		grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
		grid-auto-rows: 1fr;

		margin-top: 20px;
	}
</style>
