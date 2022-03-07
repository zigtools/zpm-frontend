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
	export let baseUrl;
	marked.setOptions({
		baseUrl,
	});
</script>

<div class="md" bind:this={mdDiv}>
	{@html domPurify.sanitize(marked(md), {})}
</div>

<style lang="scss">
	.md {
		overflow: auto;
		border: 2px solid var(--color-border-1);
		background-color: var(--color-bg-0);
		border-radius: 5px;
		padding: 20px;

		:global(pre) {
			background-color: var(--code-block-background);
			border: var(--code-block-border);
			padding: 20px;
			border-radius: 5px;
			font-size: 10pt;
		}
	}

	:global(.md) {
		line-height: 2;
	}
</style>
