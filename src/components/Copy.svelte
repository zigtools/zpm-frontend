<script>
	import copyTextToClipboard from "copy-text-to-clipboard";

	export let data;
	let copied = false;

	function copyCallback(event) {
		copyTextToClipboard(data);
		copied = true;
	}
</script>

<div>
	<button
		class={copied ? "checkButton" : "copyButton"}
		title={copied ? "Copied to clipboard" : "Copy to clipboard"}
		on:click={copyCallback}
	>
		{#if copied}
			<svg
				aria-hidden="true"
				focusable="false"
				height="20"
				viewBox="0 0 512 512"
				><path
					d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z"
					class=""
				/></svg
			>
		{:else}
			<svg
				height="20"
				viewBox="0 0 24 25"
				fill="currentColor"
				xmlns="http://www.w3.org/2000/svg"
				alt="Copy Cargo.toml snippet to clipboard"
				><path
					d="M18 20h2v3c0 1-1 2-2 2H2c-.998 0-2-1-2-2V5c0-.911.755-1.667 1.667-1.667h5A3.323 3.323 0 0110 0a3.323 3.323 0 013.333 3.333h5C19.245 3.333 20 4.09 20 5v8.333h-2V9H2v14h16v-3zM3 7h14c0-.911-.793-1.667-1.75-1.667H13.5c-.957 0-1.75-.755-1.75-1.666C11.75 2.755 10.957 2 10 2s-1.75.755-1.75 1.667c0 .911-.793 1.666-1.75 1.666H4.75C3.793 5.333 3 6.09 3 7z"
				/>
				<path
					d="M4 19h6v2H4zM12 11H4v2h8zM4 17h4v-2H4zM15 15v-3l-4.5 4.5L15 21v-3l8.027-.032L23 15z"
				/></svg
			>
		{/if}
	</button>
</div>

<style lang="scss">
	button {
		box-sizing: border-box;
		border: var(--code-block-border);
		border-radius: 4px;
		display: block;
		padding: 4px;

		&.checkButton {
			background: transparent;

			svg {
				fill: var(--text-color-h1);
			}
		}

		&.copyButton {
			background: transparent;

			svg {
				fill: var(--text-color-h1);
			}

			&:hover {
				cursor: pointer;
				svg {
					fill: var(--text-color-a);
				}
			}
		}
	}
</style>
