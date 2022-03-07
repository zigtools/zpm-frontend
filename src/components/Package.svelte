<script>
	import Tags from "./Tags.svelte";
	import GitLogo from "./GitLogo.svelte";
	import NavLink from "./NavLink.svelte";

	export let pkg;
</script>

<div class="package">
	<div class="head">
		<div>
			<h2>
				<NavLink to="/package/{pkg.name}">{pkg.name}</NavLink>
			</h2>
			<h3>
				<NavLink to="/author/{pkg.author}">{pkg.author}</NavLink>
			</h3>
		</div>
		<GitLogo gitUrl={pkg.git} />
	</div>

	<p>{pkg.description}</p>

	<div class="tags-container">
		<Tags tags={pkg.tags} />
	</div>
</div>

<style lang="scss">
	.package {
		border-radius: 8px;
		box-shadow: var(--card-shadow);
		padding: 15px;
		background-color: var(--color-bg-1-alt);
		overflow: hidden;
	}

	.head {
		display: flex;
		justify-content: space-between;
	}

	h2 {
		margin: 0;
		color: var(--text-color-h2);
		font-size: 14pt;

		:global(a) {
			color: var(--text-color-h2);
		}
	}

	h3 {
		margin-top: 0;
		color: var(--text-color-h2);
		font-size: 12pt;
		font-weight: 500;

		:global(a) {
			color: #777;
		}
	}

	.tags-container {
		left: 0px;
		bottom: 0px;

		width: 100%;

		z-index: 2;
	}

	:global(.actions > *) {
		margin-right: 15px;

		font-weight: 700;
	}
</style>
