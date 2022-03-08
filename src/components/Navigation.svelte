<script>
	import NavLink from "./NavLink.svelte";
	import { searchQuery } from "../stores.js";
	import { useNavigate } from "svelte-navigator";
	import { useLocation } from "svelte-navigator";

	let inputRef;
	let inputVal;

	const navigate = useNavigate();
	let location = useLocation();

	async function onSearchInput(e) {
		searchQuery.set(inputVal);
		if ($location.pathname != "/") {
			navigate("/", { state: { shouldFocusSearch: true } });
		}
	}

	function handleKeydown(e) {
		if (e.key == "s" && document.activeElement != inputRef) {
			inputRef.focus();
			e.preventDefault();
		}
	}

	function handleHomeLink(e) {
		searchQuery.set(null);
		inputVal = null;
	}
</script>

<svelte:window on:keydown={handleKeydown} />

<div class="container">
	<nav>
		<NavLink to="/" on:click={handleHomeLink}
			><img src="/img/zpm.svg" alt="logo" /></NavLink
		>
		<input
			bind:this={inputRef}
			bind:value={inputVal}
			on:input={onSearchInput}
			type="text"
			placeholder="Press 's' to search"
		/>
		<NavLink to="/about">About</NavLink>
	</nav>
</div>

<style lang="scss">
	nav {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		max-width: 1280px;
		margin: auto;
		padding: 10px;
		font-weight: 700;
		box-sizing: border-box;

		:global(a) {
			color: var(--text-color-a-alt);
		}
		img {
			height: 32px;
		}

		input[type="text"] {
			border-radius: 5px;
			height: 32px;

			max-height: 32px;
			font-size: 11pt;
			padding: 7px;
			box-sizing: border-box;

			font-family: inherit;
			font-weight: 600;
		}
		input[type="text"] {
			background-color: var(--color-bg-1);
			border: 2px solid var(--color-bg-3);
			color: var(--text-color-h1-alt);
		}

		input[type="text"]:focus {
			border-color: var(--text-color-a-alt);
		}
	}

	.container {
		background-color: var(--color-bg-1);
		width: 100%;
		padding-bottom: 0;
		display: inline-block;
	}
</style>
