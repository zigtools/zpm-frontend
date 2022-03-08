<div class="about-page">
	<h2>About</h2>

	<p>
		On this site you can find community-maintained packages for the
		<a href="https://ziglang.org/">Zig language</a>
		. The packages are managed via a
		<a href="https://github.com/ziglibs/repository">GitHub repository</a>
		.
	</p>

	<h3>What is zig.pm?</h3>

	<p>
		zig.pm is a multi-component project consisting of
		<a href="https://github.com/ziglibs/repository">a package repository</a>
		,
		<a href="https://github.com/zigtools/zpm-frontend">this website</a>
		and
		<a href="https://github.com/ziglibs/package-collector/">the scraper</a>
		.
	</p>
	<p>
		Together, these components form a meta package index that tries to fetch
		package meta data from all available resources to allow easy discovery
		of zig packages.
	</p>

	<h3>How can I add packages?</h3>

	<p>
		You can add packages by adding them to
		<a href="https://github.com/ziglibs/repository">this repo</a>
		. Simply clone the repository and run
		<code>zig build add</code>
		or follow the format set out in the
		<code>packages</code>
		directory. Then, file a PR. It is adviced to verify your changes with
		<code>zig build verify</code>
		before filing a PR. This runs some sanity and consistency checks on the
		repository, checking if everything is valid.
	</p>
	<p>
		Another option is using one of the package managers
		<a href="https://aquila.red/">aquila.red</a>
		or
		<a href="https://aquila.red/">gyro</a>
		to publish your package.
	</p>
	<p>
		The last option is to add the topic
		<a href="https://github.com/topic/zig-package">
			<code>zig-package</code>
		</a>
		to your
		<a href="https://github.com/">GitHub</a>
		repository. All repositories with this topic will be displayed here as
		well.
	</p>

	<h3>How can I integrate zig.pm with my package mananger or frontend?</h3>

	<p>
		You can integrate zig.pm with your package manager or frontend by using
		the zig.pm HTTPS API, which is available at
		<a href="https://zig.pm/api/">https://zig.pm/api/</a>
		or
		<a href="https://zig.pm/api/">https://zig.pm/api/</a>
		. Packages are currently provided via any
		<code>git</code>
		supported protocol and can be added as a submodule, flat copy or any
		other way.
	</p>
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
