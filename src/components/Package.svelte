<script>
	import Tags from "../components/Tags.svelte";
	import NavLink from "../components/NavLink.svelte";

	export let pkg;
	let expanded = false;
</script>

<div class="package">
	<h2>{pkg.name}</h2>
	<h3>{pkg.author}</h3>

	<p>{pkg.description}</p>

	<Tags tags={pkg.tags} />

	<div class="tooltip">
		{#if pkg.git}
			<a href={pkg.git}><img src={pkg.git.startsWith("https://github.com") ? "img/github.svg" : "img/git.svg"} alt="git"></a>
		{/if}
	</div>

	<div class="actions">
		<NavLink to="/package/{pkg.name}">Details</NavLink>
		<!-- <a on:click={() => expanded = !expanded}>Install</a> -->
	</div>

	<div class="install {expanded ? "visible" : ""}">
		<code>zpm install {pkg.name}</code>
	</div>
</div>

<style lang="scss">
	.package {
		position: relative;

		border: 2px solid #ececec;
		border-radius: 5px;

		padding: 20px;
		padding-bottom: 60px;

		overflow: hidden;
	}

	h2 {
		margin: 0;

		font-size: 18pt;
	}

	h3 {
		margin-top: 0;

		color: #666;
		font-size: 12pt;
		font-weight: 500;
	}

	p {
		// margin-bottom: 25px;
	}

	.tooltip {
		position: absolute;

		top: 20px;
		right: 20px;

		&>* {
			margin-left: 5px;
		}

		img {
			width: 20px;
		}
	}

	.actions {
		position: absolute;

		left: 0px;
		bottom: 0px;

		border-top: 2px solid #ececec;

		padding: 15px 20px;

		width: 100%;

		z-index: 2;
		background-color: white;
	}

	:global(.actions>*) {
		margin-right: 15px;

		font-weight: 700;
	}

	.install {
		position: absolute;

		top: 0px;
		right: 0px;

		display: block;
		pointer-events: none;
		opacity: 0;

		width: 100%;
		height: calc(100% - 51.67px);

		color: black;

		transition: 0.1s all ease-in-out;
		background-color: rgba(0, 0, 0, 0.75);

		&.visible {
			display: block;
			opacity: 1;
			pointer-events: all;
		}

		&>code {
			position: absolute;

			top: 50%;
			left: 50%;

			transform: translate(-50%, -50%);

			border-radius: 3px;

			padding: 15px;

			background-color: #e2e2e2;
		}

		z-index: 1;
	}
</style>
