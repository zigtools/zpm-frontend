<div class="about-page">
	<h2>About</h2>

	<h3>What is zpm?</h3>

	<p>zpm is a package manager backend and frontend for Zig. You can learn more about zpm's API <a href="https://github.com/zigtools/zpm-server">here</a>.</p>

	<h3>How can I add packages?</h3>

	<p>You can add packages by adding them to <a href="https://github.com/ziglibs/repository">this repo</a>. Simply clone the repository and run <code>zig build add</code> or follow the format set out in the <code>packages</code> directory. Then, file a PR.</p>

	<h3>How can I integrate zpm with my package mananger or frontend?</h3>

	<p>You can integrate zpm with your package manager or frontend by using the zpm HTTPS API, which is available <a href="https://zpm.random-projects.net/api/">here</a>.</p>
</div>

<style lang="scss">
	.about-page {
		position: relative;

		padding: 20px;
	}
	
	h2 {
		margin: 0;

		font-size: 40pt;
	}
</style>
