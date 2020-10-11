<script>
	import { Router, Route, createHistory } from "svelte-navigator";
	import { atobUnicode } from "../utils";

	import Tags from "../components/Tags.svelte";
	import Markdown from "../components/Markdown.svelte";

	export let fetchData;

	async function fetchPkg(id) {
		return (await fetchData).find(_ => _.name === id);
	}
	
	async function fetchReadme(pkg) {
		if (pkg.git && pkg.git.startsWith("https://github.com/")) {
			return atobUnicode((await (await fetch(`https://api.github.com/repos/${pkg.git.replace("https://github.com/", "")}/readme`)).json()).content);	
		}

		return;
	}
</script>

<Route path=":id" let:params>
	<div class="package-page">
		{#await fetchPkg(params.id)}
			<h1>Fetching Packages...</h1>
		{:then pkg}
			<h2>{pkg.name}</h2>
			<h3>{pkg.author}</h3>

			<Tags tags={pkg.tags}/>

			<p>{pkg.description}</p>

			<div class="links">
				{#if pkg.git}
					<a href={pkg.git}><img src={pkg.git.startsWith("https://github.com") ? "img/github.svg" : "img/git.svg"} alt="git"></a>
				{/if}
			</div>

			<div class="sep"></div>
			
			{#await fetchReadme(pkg)}
				<h1>Fetching Readme</h1>
			{:then readme}
				<Markdown md={readme}/>
			{/await}
		{:catch error}
			<p>Error: <code>{error}</code></p>
		{/await}
	</div>
</Route>

<style lang="scss">
	.package-page {
		position: relative;

		padding: 20px;
	}

	h2 {
		margin: 0;

		font-size: 40pt;
	}

	h3 {
		margin-top: 0;
		margin-bottom: 20px;
	}

	p {
		font-size: 14pt;
	}

	.links {
		position: absolute;

		right: 20px;
		top: 20px;

		&>* {
			margin-left: 5px;
		}

		img {
			width: 40px;
		}
	}

	.sep {
		border-radius: 5px;

		width: 100%;
		height: 3px;

		background-color: #ececec;
	}

</style>
