<script>
	import marked from "marked";
	import domPurify from "dompurify";

	export let md;
</script>

<div class="md">
	{@html domPurify.sanitize(marked(md), {})}
</div>

<style lang="scss">
	:global(.md) {
		line-height: 2;
	}
</style>
