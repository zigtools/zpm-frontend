<script>
	import { Route } from "svelte-navigator";

	import Tags from "../components/Tags.svelte";
	import Copy from "../components/Copy.svelte";
	import Markdown from "../components/Markdown.svelte";
	import NavLink from "../components/NavLink.svelte";
	import GitLogo from "../components/GitLogo.svelte";

	export let fetchData;

	async function fetchPkg(id) {
		return (await fetchData).find((_) => _.name === id);
	}

	async function getMainBranch(pkg) {
		if (isHostedOnGithub(pkg)) {
			return (
				await (
					await fetch(
						`https://api.github.com/repos/${pkg.links[
							"github"
						].replace("https://github.com/", "")}`
					)
				).json()
			).default_branch;
		}

		return;
	}

	async function fetchReadme(pkg) {
		if (isHostedOnGithub(pkg)) {
			return await (
				await fetch(
					`https://api.github.com/repos/${pkg.links["github"].replace(
						"https://github.com/",
						""
					)}/readme`,
					{
						headers: {
							accept: "application/vnd.github.VERSION.raw",
						},
					}
				)
			).text();
		}

		return;
	}

	function getContentBaseURL(pkg, default_branch) {
		if (isHostedOnGithub(pkg)) {
			return `https://raw.githubusercontent.com/${pkg.links[
				"github"
			].replace("https://github.com/", "")}/${default_branch}/`;
		}

		return;
	}

	function packageLinks(pkg) {
		const rename_list = { github: "Github", aquila: "aquila.red" };
		let links = Object.assign({}, pkg.links);
		Object.keys(links)
			.filter((key) => Object.keys(rename_list).includes(key))
			.forEach((key) => {
				links[rename_list[key]] = links[key];
				delete links[key];
			});

		Object.keys(links).forEach(
			(key) => links[key] == null && delete links[key]
		);

		return links;
	}

	function isHostedOnGithub(pkg) {
		return pkg.links.github && pkg.git.startsWith("https://github.com/");
	}
</script>

<Route path=":id" let:params>
	<div class="package-page">
		{#await fetchPkg(params.id)}
			<h1>Fetching Packages...</h1>
		{:then pkg}
			<header>
				<h2>{pkg.name}</h2>
				<GitLogo gitUrl={pkg.git} height="64" />
			</header>
			<h3>
				<NavLink to="/author/{pkg.author}">by {pkg.author}</NavLink>
			</h3>

			<Tags tags={pkg.tags} />

			<p>{pkg.description}</p>

			<div class="git-url">
				<p>Git</p>
				<div>{pkg.git} <Copy data={pkg.git} /></div>
			</div>

			{#if Object.keys(packageLinks(pkg)).length}
				<div class="package-links">
					<p>View on:</p>
					{#each Object.entries(packageLinks(pkg)) as [key, value]}
						<p>[ <a href={value}>{key}</a> ]</p>
					{/each}
				</div>
			{/if}

			{#await fetchReadme(pkg)}
				<h1>Fetching Readme</h1>
			{:then readme}
				{#if isHostedOnGithub(pkg)}
					{#await getMainBranch(pkg)}
						<h1>Fetching Readme</h1>
					{:then branch}
						<Markdown
							md={readme}
							baseUrl={getContentBaseURL(pkg, branch)}
						/>
					{/await}
				{:else}
					<Markdown md={readme} />
				{/if}
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

	.git-url {
		display: flex;
		overflow: hidden;
		border-radius: 8px;
		border: var(--code-block-border);
		margin-bottom: 10px;

		p {
			background-color: var(--color-bg-1);
			padding: 10px;
			margin: 0;
			color: var(--text-color-alt);
		}

		div {
			display: flex;
			justify-content: space-between;
			align-items: center;
			background-color: var(--code-block-background);
			padding: 5px;
			flex: 1 1 0%;
		}
	}

	.package-links {
		margin-bottom: 10px;

		p {
			display: inline-block;
			margin: 0;
			font-weight: 600;
		}
	}

	h2 {
		margin: 0;
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
</style>
