<script>
	import Tags from "./Tags.svelte";
	import GitLogo from "./GitLogo.svelte";
	import NavLink from "./NavLink.svelte";

	export let pkg;
	let expanded = false;
</script>

<div class="package">
	<h2>
		<NavLink to="/package/{pkg.name}">{pkg.name}</NavLink>
	</h2>
	<h3>
		<NavLink to="/author/{pkg.author}">{pkg.author}</NavLink>
	</h3>

	<p>{pkg.description}</p>

	<GitLogo class="git-logo" gitUrl={pkg.git} />

	<div class="tags-container">
		<Tags tags={pkg.tags} />
	</div>
</div>

<style lang="scss">
	.package {
		position: relative;

		border-radius: 3px;
		box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.4);
		padding: 20px;
		padding-bottom: 60px;
		background-color: #1a1a1a;
		overflow: hidden;
	}

	h2 {
		margin: 0;
		color: #ccc;
		font-size: 14pt;

		:global(a) {
			color: white;
		}
	}

	h3 {
		margin-top: 0;
		color: #777;
		font-size: 12pt;
		font-weight: 500;

		:global(a) {
			color: #777;
		}
	}

	:global(.git-logo) {
		position: absolute;

		top: 20px;
		right: 20px;
		width: 32px;
		height: 32px;

		& > * {
			margin-left: 5px;
		}
	}

	.tags-container {
		position: absolute;

		left: 0px;
		bottom: 0px;

		padding: 10px 10px;

		width: 100%;

		z-index: 2;
	}

	:global(.actions > *) {
		margin-right: 15px;

		font-weight: 700;
	}
</style>
