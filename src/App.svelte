<script>
	import { Router, Route, createHistory } from "svelte-navigator";
	import Home from "./routes/Home.svelte";
	import About from "./routes/About.svelte";
	import NavLink from "./components/NavLink.svelte";
	import PackagePage from "./routes/PackagePage.svelte";
	import TagPage from "./routes/TagPage.svelte";
	import createHashSource from "./hashHistory.js";

	let fetchData = (async () => {
		const response = await fetch("https://zpm.random-projects.net/api/packages");
		return await response.json();
	})();

	let fetchTags = (async () => {
		const response = await fetch("https://zpm.random-projects.net/api/tags");
		return await response.json();
	})();

	let url = "";
	const hash = createHistory(createHashSource());
</script>

<Router url={url} history={hash}>
	<div class="container">
		<nav>
			<h1><NavLink to="/">zpm</NavLink></h1>
			<div class="items">
				<NavLink to="/">Home</NavLink>
				<NavLink to="/about">About</NavLink>
			</div>
		</nav>
	</div>
	<main>
		<Route path="/">
			<Home fetchData={fetchData}/>
		</Route>
		<Route path="/about">
			<About />
		</Route>
		<Route path="package/*">
			<PackagePage fetchData={fetchData}/>
		</Route>
		<Route path="tag/*">
			<TagPage fetchTags={fetchTags} fetchData={fetchData}/>
		</Route>
	</main>
</Router>

<style lang="scss">
	.container {
		position: fixed;

		top: 0;
		left: 0;

		width: calc(100% - 40px);

		padding: 20px;
		padding-bottom: 0;

		z-index: 10;
	}

	nav {
		position: relative;

		border: 2px solid #ececec;
		border-radius: 5px;

		padding: 20px;

		background-color: white;

		h1 {
			margin: 0;

			font-size: 18pt;
		}

		.items {
			position: absolute;

			top: 50%;
			right: 20px;

			transform: translate(0, -50%);
		}
	}

	:global(nav .items>*) {
		font-weight: 700;
		margin-left: 20px;
	}

	main {
		margin-top: 113px;
	}
</style>
