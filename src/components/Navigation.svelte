<script>
	import NavLink from "./NavLink.svelte";
	import { searchQuery } from "../stores.js";

	let inputRef;

	function onSearchInput(e) {
		searchQuery.set(e.target.value);
	}

	function handleKeydown(e) {
		if (e.key == "s" && document.activeElement != inputRef) {
			inputRef.focus();
			e.preventDefault();
		}
	}
</script>

<svelte:window on:keydown={handleKeydown} />

<div class="container">
	<nav>
		<NavLink to="/">
			<img src="img/zpm.svg" alt="logo" />
		</NavLink>
		<div class="items">
			<input
				bind:this={inputRef}
				type="text"
				placeholder="Press 's' to search"
				on:input={onSearchInput} />
			<NavLink to="/about">About</NavLink>
		</div>
	</nav>
</div>

<style lang="scss">
	nav {
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
			background-color: #222;
			border: 2px solid #333;
			color: #bbb;
		}

		input[type="text"]:focus {
			border-color: #88f;
		}
	}

	.container {
		background-color: #222;
		width: 100%;
		padding-bottom: 0;
		display: inline-block;
	}

	nav {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		max-width: 1280px;
		margin: auto;
		padding: 20px;
		box-sizing: border-box;
	}

	:global(nav .items > *) {
		font-weight: 700;
		margin-left: 20px;
	}
</style>
