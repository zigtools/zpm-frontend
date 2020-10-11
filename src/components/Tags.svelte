<script>
	export let tags;

	import NavLink from "../components/NavLink.svelte";
</script>

<div>
	{#each tags as tag}
	<span><NavLink to="/tag/{tag}">{tag}</NavLink></span>
	{/each}
</div>

<style lang="scss">
	div {
		display: block;

		&>* {
			display: inline-block;

			margin-right: 5px;

			border: 2px solid #ececec;
			border-radius: 5px;

			padding: 7px 12px;

			font-weight: 600;
		}
	}
</style>
