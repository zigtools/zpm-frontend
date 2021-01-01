<script>
	import { Router, Route, createHistory } from "svelte-navigator";
	import utils from "../utils";

	import Tabs from "../components/Tabs.svelte";
	import Tags from "../components/Tags.svelte";
	import Markdown from "../components/Markdown.svelte";
	import NavLink from "../components/NavLink.svelte";
	import GitLogo from "../components/GitLogo.svelte";

	export let fetchData;

	async function fetchPkg(id) {
		return (await fetchData).find((_) => _.name === id);
	}

	async function fetchReadme(pkg) {
		if (pkg.git && pkg.git.startsWith("https://github.com/")) {
			return utils.atobUnicode(
				(
					await (
						await fetch(
							`https://api.github.com/repos/${pkg.git.replace(
								"https://github.com/",
								""
							)}/readme`
						)
					).json()
				).content
			);
		}

		return;
	}
</script>

<Route path=":id" let:params>
	<div class="package-page">
		{#await fetchPkg(params.id)}
			<h1>Fetching Packages...</h1>
		{:then pkg}
			<header>
				<h2>{pkg.name}</h2>
				<GitLogo gitUrl={pkg.git} />
			</header>
			<h3>
				<NavLink to="/author/{pkg.author}">by {pkg.author}</NavLink>
			</h3>

			<!-- <pre><code class="block">{pkg.git}</code></pre> -->
			<Tags tags={pkg.tags} />

			<p>{pkg.description}</p>

			<div class="install">
				<Tabs tabs={utils.tabsFromPackage(pkg)} />
			</div>

			<div class="sep" />

			{#await fetchReadme(pkg)}
				<h1>Fetching Readme</h1>
			{:then readme}
				<Markdown md={readme} />
			{/await}
		{:catch error}
			<p>Error: <code>{error}</code></p>
		{/await}
	</div>
</Route>

<style lang="scss">
	header {
		display: flex;
		justify-content: space-between;
	}

	.package-page {
		position: relative;
		padding: 20px;
	}

	h2 {
		margin: 0;
		color: #fff;
		font-size: 40pt;
	}

	h3 {
		margin-top: 0;
		color: #777;
		font-size: 16pt;
		font-weight: 500;

		:global(a) {
			color: #777;
		}
	}

	p {
		font-size: 14pt;
	}

	.install {
		display: flex;

		border: 2px solid #222;
		border-radius: 5px;

		overflow: hidden;
	}

	.sep {
		margin-top: 20px;

		border-radius: 5px;

		width: 100%;
		height: 3px;
	}
</style>
