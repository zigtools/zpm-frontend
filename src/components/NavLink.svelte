<script>
	import { Link } from "svelte-navigator";
	import { createEventDispatcher } from "svelte";

	const dispatch = createEventDispatcher();

	export let to = "";

	function getProps({ location, href, isPartiallyCurrent, isCurrent }) {
		const isActive =
			href === "/" ? isCurrent : isPartiallyCurrent || isCurrent;

		// The object returned here is spread on the anchor element's attributes
		if (isActive) {
			return { class: "active" };
		}
		return {};
	}

	function clickHandle() {
		dispatch("click");
	}
</script>

<Link on:click={clickHandle} {to} {getProps}>
	<slot />
</Link>

<style>
	:global(a) {
		display: inline-flex;
	}
</style>
