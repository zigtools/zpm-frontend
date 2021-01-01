<script>
	import NavLink from "../components/NavLink.svelte";
	export let tags;
</script>

<div>
	{#each tags as tag}
		<span><NavLink to="/tag/{tag}">{tag}</NavLink></span>
	{/each}
</div>

<style lang="scss">
	div {
		display: block;

		& > * {
			&:hover {
				background-color: #333;
			}

			display: inline-block;

			margin-right: 5px;

			border: 2px solid #333;
			border-radius: 5px;
			padding: 5px 10px;

			font-weight: 600;
			font-size: 10pt;
		}
	}
</style>
