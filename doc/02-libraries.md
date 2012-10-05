<!DOCTYPE html>
<html class="no-js" lang="en">
	<head>
		<meta charset="utf-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
		<title>Composer</title>
		<meta name="description" content="Dependency Management for PHP">
		<meta name="viewport" content="width=device-width,initial-scale=1">
		<link rel="stylesheet" href="css/style.css">
		<script src="js/libs/modernizr-2.0.6.min.js"></script>
	</head>
	<body>
		<div id="container">
			<header>
				<a href="/">Home</a><a class="" href="00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>
			</header>
			<div id="main" role="main">
				<ul class="toc">
					<li>
						<a href="#every-project-is-a-package">Every project is a package</a> 
					</li>
					<li>
						<a href="#specifying-the-version">Specifying the version</a> 
						<ul>
							<li>
								<a href="#tags">Tags</a> 
							</li>
							<li>
								<a href="#branches">Branches</a> 
							</li>
							<li>
								<a href="#aliases">Aliases</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#lock-file">Lock file</a> 
					</li>
					<li>
						<a href="#light-weight-distribution-packages">Light-weight distribution packages</a> 
					</li>
					<li>
						<a href="#publishing-to-a-vcs">Publishing to a VCS</a> 
					</li>
					<li>
						<a href="#publishing-to-packagist">Publishing to packagist</a> 
					</li>
				</ul>
				<h1 id="libraries">Libraries<a href="#libraries" class="anchor">#</a></h1>
				<p>This chapter will tell you how to make your library installable through composer.</p>
				<h2 id="every-project-is-a-package">
					Every project is a package<a href="#every-project-is-a-package" class="anchor">#</a>
				</h2>
				<p>As soon as you have a <code>composer.json</code> in a directory, that directory is a
					package. When you add a <code>require</code> to a project, you are making a package that
					depends on other packages. The only difference between your project and
					libraries is that your project is a package without a name.</p>
				<p>In order to make that package installable you need to give it a name. You do
					this by adding a <code>name</code> to <code>composer.json</code>:</p>
				<pre><code>{
								"name": "acme/hello-world",
								"require": {
										"monolog/monolog": "1.0.*"
								}
						}
						</code></pre>
				<p>In this case the project name is <code>acme/hello-world</code>, where <code>acme</code> is the
					vendor name. Supplying a vendor name is mandatory.</p>
				<blockquote>
					<p><strong>Note:</strong> If you don't know what to use as a vendor name, your GitHub
						username is usually a good bet. While package names are case insensitive, the
						convention is all lowercase and dashes for word separation.</p>
				</blockquote>
				<h2 id="specifying-the-version">Specifying the version<a href="#specifying-the-version" class="anchor">#</a></h2>
				<p>You need to specify the package's version some way. When you publish your
					package on Packagist, it is able to infer the version from the VCS (git, svn,
					hg) information, so in that case you do not have to specify it, and it is
					recommended not to. See <a href="#tags">tags</a> and <a href="#branches">branches</a> to see how
					version numbers are extracted from these.</p>
				<p>If you are creating packages by hand and really have to specify it explicitly,
					you can just add a <code>version</code> field:</p>
				<pre><code>{
								"version": "1.0.0"
						}
						</code></pre>
				<h3 id="tags">Tags<a href="#tags" class="anchor">#</a></h3>
				<p>For every tag that looks like a version, a package version of that tag will be
					created. It should match 'X.Y.Z' or 'vX.Y.Z', with an optional suffix for RC,
					beta, alpha or patch.</p>
				<p>Here are a few examples of valid tag names:</p>
				<pre><code>1.0.0
						v1.0.0
						1.10.5-RC1
						v4.4.4beta2
						v2.0.0-alpha
						v2.0.4-p1
						</code></pre>
				<blockquote>
					<p><strong>Note:</strong> If you specify an explicit version in <code>composer.json</code>, the tag name must match the specified version.</p>
				</blockquote>
				<h3 id="branches">Branches<a href="#branches" class="anchor">#</a></h3>
				<p>For every branch, a package development version will be created. If the branch
					name looks like a version, the version will be <code>{branchname}-dev</code>. For example
					a branch <code>2.0</code> will get a version <code>2.0.x-dev</code> (the <code>.x</code> is added for technical
					reasons, to make sure it is recognized as a branch, a <code>2.0.x</code> branch would also
					be valid and be turned into <code>2.0.x-dev</code> as well. If the branch does not look
					like a version, it will be <code>dev-{branchname}</code>. <code>master</code> results in a
					<code>dev-master</code> version.</p>
				<p>Here are some examples of version branch names:</p>
				<pre><code>1.x
1.0 (equals 1.0.x)
1.1.x
</code></pre>
				<blockquote>
					<p><strong>Note:</strong> When you install a dev version, it will install it from source.</p>
				</blockquote>
				<h3 id="aliases">Aliases<a href="#aliases" class="anchor">#</a></h3>
				<p>It is possible alias branch names to versions. For example, you could alias
					<code>dev-master</code> to <code>1.0.x-dev</code>, which would allow you to require <code>1.0.x-dev</code> in all
					the packages.</p>
				<p>See <a href="articles/aliases.md">Aliases</a> for more information.</p>
				<h2 id="lock-file">Lock file<a href="#lock-file" class="anchor">#</a></h2>
				<p>For your library you may commit the <code>composer.lock</code> file if you want to. This
					can help your team to always test against the same dependency versions.
					However, this lock file will not have any effect on other projects that depend
					on it. It only has an effect on the main project.</p>
				<p>If you do not want to commit the lock file and you are using git, add it to
					the <code>.gitignore</code>.</p>
				<h2 id="light-weight-distribution-packages">Light-weight distribution packages<a href="#light-weight-distribution-packages" class="anchor">#</a></h2>
				<p>Including the tests and other useless information like .travis.yml in
					distributed packages is not a good idea.</p>
				<p>The <code>.gitattributes</code> file is a git specific file like <code>.gitignore</code> also living
					at the root directory of your library. It overrides local and global
					configuration (<code>.git/config</code> and <code>~/.gitconfig</code> respectively) when present and
					tracked by git.</p>
				<p>Use <code>.gitattributes</code> to prevent unwanted files from bloating the zip
					distribution packages.</p>
				<pre><code>// .gitattributes
Tests/ export-ignore
phpunit.xml.dist export-ignore
Resources export-ignore
.travis.yml export-ignore
</code></pre>
				<p>Test it by inspecting the zip file generated manually:</p>
				<pre><code>git archive branchName --format zip -o file.zip
</code></pre>
				<blockquote>
					<p><strong>Note:</strong> Files would be still tracked by git just not included in the
						distribution. This will only work for GitHub packages installed from
						dist (i.e. tagged releases) for now.</p>
				</blockquote>
				<h2 id="publishing-to-a-vcs">Publishing to a VCS<a href="#publishing-to-a-vcs" class="anchor">#</a></h2>
				<p>Once you have a vcs repository (version control system, e.g. git) containing a
					<code>composer.json</code> file, your library is already composer-installable. In this
					example we will publish the <code>acme/hello-world</code> library on GitHub under
					<code>github.com/composer/hello-world</code>.</p>
				<p>Now, To test installing the <code>acme/hello-world</code> package, we create a new
					project locally. We will call it <code>acme/blog</code>. This blog will depend on
					<code>acme/hello-world</code>, which in turn depends on <code>monolog/monolog</code>. We can
					accomplish this by creating a new <code>blog</code> directory somewhere, containing a
					<code>composer.json</code>:</p>
				<pre><code>{
		"name": "acme/blog",
		"require": {
				"acme/hello-world": "dev-master"
		}
}
</code></pre>
				<p>The name is not needed in this case, since we don't want to publish the blog
					as a library. It is added here to clarify which <code>composer.json</code> is being
					described.</p>
				<p>Now we need to tell the blog app where to find the <code>hello-world</code> dependency.
					We do this by adding a package repository specification to the blog's
					<code>composer.json</code>:</p>
				<pre><code>{
		"name": "acme/blog",
		"repositories": [
				{
						"type": "vcs",
						"url": "https://github.com/composer/hello-world"
				}
		],
		"require": {
				"acme/hello-world": "dev-master"
		}
}
</code></pre>
				<p>For more details on how package repositories work and what other types are
					available, see <a href="05-repositories.md">Repositories</a>.</p>
				<p>That's all. You can now install the dependencies by running composer's
					<code>install</code> command!</p>
				<p><strong>Recap:</strong> Any git/svn/hg repository containing a <code>composer.json</code> can be added
					to your project by specifying the package repository and declaring the
					dependency in the <code>require</code> field.</p>
				<h2 id="publishing-to-packagist">Publishing to packagist<a href="#publishing-to-packagist" class="anchor">#</a></h2>
				<p>Alright, so now you can publish packages. But specifying the vcs repository
					every time is cumbersome. You don't want to force all your users to do that.</p>
				<p>The other thing that you may have noticed is that we did not specify a package
					repository for <code>monolog/monolog</code>. How did that work? The answer is packagist.</p>
				<p><a href="http://packagist.org/">Packagist</a> is the main package repository for
					composer, and it is enabled by default. Anything that is published on
					packagist is available automatically through composer. Since monolog
					<a href="http://packagist.org/packages/monolog/monolog">is on packagist</a>, we can depend
					on it without having to specify any additional repositories.</p>
				<p>If we wanted to share <code>hello-world</code> with the world, we would publish it on
					packagist as well. Doing so is really easy.</p>
				<p>You simply hit the big "Submit Package" button and sign up. Then you submit
					the URL to your VCS repository, at which point packagist will start crawling
					it. Once it is done, your package will be available to anyone.</p>
				<p class="prev-next">&larr; <a href="01-basic-usage.md">Basic usage</a> |  <a href="03-cli.md">Command-line interface</a> &rarr;</p>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master02-libraries.md">fork and edit</a> it!
				</p>
			</div> 
			<footer></footer>
		</div>
	</body>
</html>