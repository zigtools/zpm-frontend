<script>
	import { onMount } from "svelte";
	import marked from "marked";
	import domPurify from "dompurify";
	import highlight from "../highlight.pack.js";

	let mdDiv;

	onMount(() => {
		[...mdDiv.querySelectorAll("pre code")].map((_) =>
			highlight.highlightBlock(_)
		);
	});

	export let md;
</script>

<div class="md" bind:this={mdDiv}>
	{@html domPurify.sanitize(marked(md), {})}
</div>

<style lang="scss">
	.md {
		border: 2px solid #222;
		border-radius: 5px;
		padding: 20px;

		:global(pre) {
			background-color: #222;
			padding: 20px;
			border-radius: 5px;
			font-size: 10pt;
		}
	}

	:global(.md) {
		line-height: 2;
	}
</style>
