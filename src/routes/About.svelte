<div class="about-page">
	<h2>About</h2>

	<p>On this site you can find community-maintained packages for the <a href="https://ziglang.org/">Zig language</a>. The packages are managed via a <a href="https://github.com/ziglibs/repository">GitHub repository</a>.</p>

	<h3>What is zpm?</h3>

	<p>zpm is a multi-component project consisting of <a href="https://github.com/ziglibs/repository">the package repository</a>, a <a href="https://github.com/zigtools/zpm">command line tool</a>, an <a href="https://github.com/zigtools/zpm-server">API server</a> and <a href="https://github.com/zigtools/zpm-frontend">this website</a>.</p>
	<p>Together, these components form a loosly coupled package manager where each component can be replaced or extended by others without interferring with the other components.</p>
	<p>You can learn more about zpm's API <a href="https://github.com/zigtools/zpm-server">here</a>.</p> 

	<h3>How can I add packages?</h3>

	<p>You can add packages by adding them to <a href="https://github.com/ziglibs/repository">this repo</a>. Simply clone the repository and run <code>zig build add</code> or follow the format set out in the <code>packages</code> directory. Then, file a PR. It is adviced to verify your changes with <code>zig build verify</code> before filing a PR. This runs some sanity and consistency checks on the repository, checking if everything is valid.</p>

	<h3>What package managers are available?</h3>

	<p>Currently, only <a href="https://github.com/mattnite/zkg/">zkg</a> can install packages from the repository. There are plans to make <a href="https://github.com/zigtools/zpm">zpm</a> also support package installation via CLI.<p>
	<p>If you don't want to use a tool, you can also just create a flat copy in your project or add the packages as a <a href="https://git-scm.com/book/en/v2/Git-Tools-Submodules">git submodule</a>.</p>

	<h3>How can I integrate zpm with my package mananger or frontend?</h3>

	<p>You can integrate zpm with your package manager or frontend by using the zpm HTTPS API, which is available <a href="https://zpm.random-projects.net/api/">here</a>. Packages are currently provided via any <code>git</code> supported protocol and can be added as a submodule, flat copy or any other way.</p>
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
