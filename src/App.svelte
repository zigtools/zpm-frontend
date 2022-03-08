<script>
	import { Router, Route, createHistory } from "svelte-navigator";
	import Home from "./routes/Home.svelte";
	import About from "./routes/About.svelte";
	import Navigation from "./components/Navigation.svelte";
	import PackagePage from "./routes/PackagePage.svelte";
	import TagPage from "./routes/TagPage.svelte";
	import AuthorPage from "./routes/AuthorPage.svelte";
	import createHashSource from "./hashHistory.js";

	let fetchData = (async () => {
		const response = await fetch("https://zig.pm/api/packages");
		return await response.json();
	})();

	let fetchTags = (async () => {
		const response = await fetch("https://zig.pm/api/tags");
		return await response.json();
	})();

	let url = "";
	const hash = createHistory(createHashSource());
</script>

<!-- 
	We disable svelte/navigator focus managmenent by using primary={false}
	Otherwise we can't keep the focus on the search input when switching pages
	More information here: https://github.com/mefechoel/svelte-navigator#router 
-->
<Router {url} primary={false}>
	<Navigation />
	<main>
		<Route path="/">
			<Home {fetchData} />
		</Route>
		<Route path="/about">
			<About />
		</Route>
		<Route path="package/*">
			<PackagePage {fetchData} />
		</Route>
		<Route path="tag/*">
			<TagPage {fetchTags} {fetchData} />
		</Route>
		<Route path="author/*">
			<AuthorPage {fetchData} />
		</Route>
	</main>
</Router>

<style lang="scss">
	main {
		max-width: 1280px;
		margin: auto;
	}
</style>
