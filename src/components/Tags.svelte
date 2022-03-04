<script>
	import NavLink from "../components/NavLink.svelte";
	export let tags;
</script>

<div>
	{#each tags as tag}
		<NavLink to="/tag/{tag}"><span>{tag}</span></NavLink>
	{/each}
</div>

<style lang="scss">
	div {
		display: flex;
		flex-wrap: wrap;
		gap: 5px;

		span {
			&:hover {
				background-color: var(--color-tag-hover);
			}

			display: inline-block;
			border: 1px solid var(--color-tag-border);
			border-radius: 5px;
			padding: 5px 10px;
			font-weight: 600;
			font-size: 10pt;
		}
	}
</style>
