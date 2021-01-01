<script>
	import copyTextToClipboard from "copy-text-to-clipboard";

	export let tabs;
	let copied = false;
	let selected = Object.keys(tabs)[0];

	function copyCallback(event) {
		copyTextToClipboard(tabs[selected]);
		copied = true;
	}
</script>

<div class="tabs">
	<div class="buttons">
		{#each Object.keys(tabs) as tab}
			<button
				class:selected={tab === selected}
				on:click={(e) => {
					copied = false;
					selected = e.target.innerText;
				}}>{tab}</button>
		{/each}
	</div>

	<div class="block-container">
		<div class="block-content">
			<pre><code class="block">{tabs[selected]}</code></pre>
			<button
				class={copied ? 'checkButton' : 'copyButton'}
				title={copied ? 'Copied to clipboard' : 'Copy to clipboard'}
				on:click={copyCallback}>
				{#if copied}
					<svg
						aria-hidden="true"
						focusable="false"
						height="25"
						viewBox="0 0 512 512"><path
							d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z"
							class="" /></svg>
				{:else}
					<svg
						height="25"
						viewBox="0 0 24 25"
						fill="currentColor"
						xmlns="http://www.w3.org/2000/svg"
						alt="Copy Cargo.toml snippet to clipboard"><path
							d="M18 20h2v3c0 1-1 2-2 2H2c-.998 0-2-1-2-2V5c0-.911.755-1.667 1.667-1.667h5A3.323 3.323 0 0110 0a3.323 3.323 0 013.333 3.333h5C19.245 3.333 20 4.09 20 5v8.333h-2V9H2v14h16v-3zM3 7h14c0-.911-.793-1.667-1.75-1.667H13.5c-.957 0-1.75-.755-1.75-1.666C11.75 2.755 10.957 2 10 2s-1.75.755-1.75 1.667c0 .911-.793 1.666-1.75 1.666H4.75C3.793 5.333 3 6.09 3 7z" />
						<path
							d="M4 19h6v2H4zM12 11H4v2h8zM4 17h4v-2H4zM15 15v-3l-4.5 4.5L15 21v-3l8.027-.032L23 15z" /></svg>
				{/if}
			</button>
		</div>
	</div>
</div>

<style lang="scss">
	.block-container {
		background-color: #222;

		.block-content {
			display: flex;
			flex-direction: row;
			align-items: stretch;
			justify-content: space-between;

			button {
				box-sizing: border-box;
				border: 0px;
				display: block;
				background: #333;
				padding: 8px;

				&.checkButton {
					background: transparent;

					svg {
						fill: #444;
					}
				}

				&.copyButton {
					svg {
						fill: #bbb;
					}

					&:hover {
						background: #444;
						cursor: pointer;
						svg {
							fill: #fff;
						}
					}

					&:active {
						background: #222;
						cursor: pointer;
						svg {
							fill: #fff;
						}
					}
				}
			}
		}
	}

	.block {
		line-height: 100%;
		padding-left: 10px;
		font-size: 12pt;
	}

	.tabs {
		display: flex;
		flex-direction: column;
		width: 100%;

		.buttons {
			display: flex;
			flex-direction: row;

			& > * {
				display: block;

				border: none;
				border-bottom: 2px solid #222;

				width: 100%;
				padding: 10px;

				color: #888;
				text-align: center;
				font-weight: 700;

				cursor: pointer;
				overflow: hidden;
				text-overflow: ellipsis;
				background-color: #111;

				&:hover {
					color: #ccc;
				}

				&.selected {
					background-color: #ffbb4d;
					color: #333;
				}
			}
		}
	}
</style>
