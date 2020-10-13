<script>
	export let tabs;

	let selected = Object.keys(tabs)[0];
</script>

<div class="tabs">
	<div>
		{#each Object.keys(tabs) as tab}
			<button class:selected={tab === selected} on:click={e => {selected = e.target.innerText}}>{tab}</button>
		{/each}
	</div>
	<div>
		<h2>{selected}</h2>

		<pre><code class="block">{tabs[selected]}</code></pre>
	</div>
</div>

<style lang="scss">
	.tabs {
		display: flex;

		width: 100%;

		&>*:first-child {
			border-right: 2px solid #ececec;
			
			width: 20%;
			height: 100%;
			
			&>* {
				display: block;
				
				border: none;
				border-bottom: 2px solid #ececec;
				
				width: 100%;
				
				padding: 10px;
				
				color: #cacaca;
				text-align: center;
				font-weight: 700;
				
				cursor: pointer;
				overflow: hidden;
				text-overflow: ellipsis;
				background-color: white;
				
				&:hover, &.selected {
					color: #333;
				}
			}
		}
		
		&>*:last-child {
			width: 80%;
			
			padding: 20px;
			
			overflow: auto;

			&>h2 {
				margin-top: 0;
			}
		}
	}
</style>
