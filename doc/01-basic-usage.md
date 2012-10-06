<!DOCTYPE html>
<html class="no-js" lang="zh">
		<head>
			<meta charset="utf-8">
			<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
			<title>Composer</title>
			<meta name="description" content="Dependency Management for PHP">
			<meta name="viewport" content="width=device-width,initial-scale=1">
			<link rel="stylesheet" href="css/style.css">
			<script src="js/modernizr-2.0.6.min.js"></script>
		</head>
		<body>
				<div id="container">
						<header>
							<a href="/">Home</a><a class="" href="/doc/00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                           
						</header>
						<div id="main" role="main">
							<ul class="toc">
								<li>
									<a href="#installation">Installation</a> 
								</li>
								<li>
									<a href="#composer-json-project-setup">composer.json: Project Setup</a> 
									<ul>
										<li>
											<a href="#the-require-key">The require Key</a> 
										</li>
										<li>
											<a href="#package-names">Package Names</a> 
										</li>
										<li>
											<a href="#package-versions">Package Versions</a> 
										</li>
									</ul>
								</li>
								<li>
									<a href="#installing-dependencies">Installing Dependencies</a> 
								</li>
								<li>
									<a href="#composer-lock-the-lock-file">composer.lock - The Lock File</a> 
								</li>
								<li>
									<a href="#packagist">Packagist</a> 
								</li>
								<li>
									<a href="#autoloading">Autoloading</a> 
								</li>
							</ul>
							<h1 id="basic-usage">Basic usage<a href="#basic-usage" class="anchor">#</a></h1>
							<h2 id="installation">Installation<a href="#installation" class="anchor">#</a></h2>
							<p>To install Composer, you just need to download the <code>composer.phar</code> executable.</p>
							<pre><code>$ curl -s http://getcomposer.org/installer | php
							</code></pre>
							<p>For the details, see the <a href="00-intro.md">Introduction</a> chapter.</p>
							<p>To check if Composer is working, just run the PHAR through <code>php</code>:</p>
							<pre><code>$ php composer.phar
							</code></pre>
							<p>This should give you a list of available commands.</p>
							<blockquote>
								<p><strong>Note:</strong> You can also perform the checks only without downloading Composer
		by using the <code>--check</code> option. For more information, just use <code>--help</code>.</p>
								<pre><code>$ curl -s http://getcomposer.org/installer | php -- --help
								</code></pre>
							</blockquote>
							<h2 id="composer-json-project-setup"><code>composer.json</code>: Project Setup<a href="#composer-json-project-setup" class="anchor">#</a></h2>
							<p>To start using Composer in your project, all you need is a <code>composer.json</code>
file. This file describes the dependencies of your project and may contain
other metadata as well.</p>
							<p>The <a href="http://json.org/">JSON format</a> is quite easy to write. It allows you to
define nested structures.</p>
							<h3 id="the-require-key">The <code>require</code> Key<a href="#the-require-key" class="anchor">#</a></h3>
							<p>The first (and often only) thing you specify in <code>composer.json</code> is the
<code>require</code> key. You're simply telling Composer which packages your project
depends on.
							</p>
<pre><code>{
		"require": {
				"monolog/monolog": "1.0.*"
		}
}
</code></pre>
							<p>As you can see, <code>require</code> takes an object that maps <strong>package names</strong> (e.g. <code>monolog/monolog</code>)
							to <strong>package versions</strong> (e.g. <code>1.0.*</code>).</p>
							<h3 id="package-names">Package Names<a href="#package-names" class="anchor">#</a></h3>
							<p>The package name consists of a vendor name and the project's name. Often these
							will be identical - the vendor name just exists to prevent naming clashes. It allows
							two different people to create a library named <code>json</code>, which would then just be
							named <code>igorw/json</code> and <code>seldaek/json</code>.</p>
							<p>Here we are requiring <code>monolog/monolog</code>, so the vendor name is the same as the
							project's name. For projects with a unique name this is recommended. It also
							allows adding more related projects under the same namespace later on. If you
							are maintaining a library, this would make it really easy to split it up into
							smaller decoupled parts.</p>
							<h3 id="package-versions">Package Versions<a href="#package-versions" class="anchor">#</a></h3>
							<p>We are requiring version <code>1.0.*</code> of monolog. This means any version in the <code>1.0</code>
							development branch. It would match <code>1.0.0</code>, <code>1.0.2</code> or <code>1.0.20</code>.</p>
							<p>Version constraints can be specified in a few different ways.</p>
								<ul>
									<li>
										<p><strong>Exact version:</strong> You can specify the exact version of a package, for
								example <code>1.0.2</code>. This is not used very often, but can be useful.</p>
									</li>
									<li>
										<p><strong>Range:</strong> By using comparison operators you can specify ranges of valid
								versions. Valid operators are <code>&gt;</code>, <code>&gt;=</code>, <code>&lt;</code>, <code>&lt;=</code>, <code>!=</code>. An example range
								would be <code>&gt;=1.0</code>. You can define multiple ranges, separated by a comma:
								<code>&gt;=1.0,&lt;2.0</code>.
							</p>
							</li>
							<li>
								<p><strong>Wildcard:</strong> You can specify a pattern with a <code>*</code> wildcard. <code>1.0.*</code> is the
	equivalent of <code>&gt;=1.0,&lt;1.1-dev</code>.
								</p>
							</li>
							</ul><h2 id="installing-dependencies">Installing Dependencies<a href="#installing-dependencies" class="anchor">#</a></h2>
						<p>To fetch the defined dependencies into your local project, just run the
						<code>install</code> command of <code>composer.phar</code>.</p>
						<pre><code>$ php composer.phar install
						</code></pre>
						<p>This will find the latest version of <code>monolog/monolog</code> that matches the
						supplied version constraint and download it into the <code>vendor</code> directory.
						It's a convention to put third party code into a directory named <code>vendor</code>.
						In case of monolog it will put it into <code>vendor/monolog/monolog</code>.</p>
						<blockquote>
							<p><strong>Tip:</strong> If you are using git for your project, you probably want to add
							<code>vendor</code> into your <code>.gitignore</code>. You really don't want to add all of that
							code to your repository.</p>
						</blockquote>
						<p>Another thing that the <code>install</code> command does is it adds a <code>composer.lock</code>
						file into your project root.</p>
						<h2 id="composer-lock-the-lock-file"><code>composer.lock</code> - The Lock File<a href="#composer-lock-the-lock-file" class="anchor">#</a></h2>
						<p>After installing the dependencies, Composer writes the list of the exact
						versions it installed into a <code>composer.lock</code> file. This locks the project
						to those specific versions.</p>
						<p><strong>Commit your application's <code>composer.lock</code> (along with <code>composer.json</code>) into version control.</strong></p>
						<p>This is important because the <code>install</code> command checks if a lock file is present,
						and if it is, it downloads the versions specified there (regardless of what <code>composer.json</code>
						says). This means that anyone who sets up the project will download the exact
						same version of the dependencies.</p>
						<p>If no <code>composer.lock</code> file exists, Composer will read the dependencies and
						versions from <code>composer.json</code> and  create the lock file.</p>
						<p>This means that if any of the dependencies get a new version, you won't get the updates
						automatically. To update to the new version, use <code>update</code> command. This will fetch
						the latest matching versions (according to your <code>composer.json</code> file) and also update
						the lock file with the new version.</p>
						<pre><code>$ php composer.phar update
						</code></pre>
						<blockquote>
							<p><strong>Note:</strong> For libraries it is not necessarily recommended to commit the lock file,
							see also: <a href="02-libraries.md#lock-file">Libraries - Lock file</a>.</p>
						</blockquote>
						<h2 id="packagist">Packagist<a href="#packagist" class="anchor">#</a></h2>
						<p><a href="http://packagist.org/">Packagist</a> is the main Composer repository. A Composer
						repository is basically a package source: a place where you can get packages
						from. Packagist aims to be the central repository that everybody uses. This
						means that you can automatically <code>require</code> any package that is available
						there.</p>
						<p>If you go to the <a href="http://packagist.org/">packagist website</a> (packagist.org),
						you can browse and search for packages.</p>
						<p>Any open source project using Composer should publish their packages on
						packagist. A library doesn't need to be on packagist to be used by Composer,
						but it makes life quite a bit simpler.</p>
						<h2 id="autoloading">Autoloading<a href="#autoloading" class="anchor">#</a></h2>
						<p>For libraries that specify autoload information, Composer generates a
						<code>vendor/autoload.php</code> file. You can simply include this file and you
						will get autoloading for free.</p>
						<pre><code>require 'vendor/autoload.php';
						</code></pre>
						<p>This makes it really easy to use third party code. For example: If your
						project depends on monolog, you can just start using classes from it, and they
						will be autoloaded.</p>
						<pre><code>$log = new Monolog\Logger('name');
						$log-&gt;pushHandler(new Monolog\Handler\StreamHandler('app.log', Monolog\Logger::WARNING));
						$log-&gt;addWarning('Foo');
						</code></pre>
						<p>You can even add your own code to the autoloader by adding an <code>autoload</code> field
						to <code>composer.json</code>.</p>
						<pre><code>{
								"autoload": {
										"psr-0": {"Acme": "src/"}
								}
						}
						</code></pre>
						<p>Composer will register a
						<a href="https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md">PSR-0</a>
						autoloader for the <code>Acme</code> namespace.</p>
						<p>You define a mapping from namespaces to directories. The <code>src</code> directory would
						be in your project root, on the same level as <code>vendor</code> directory is. An example
						filename would be <code>src/Acme/Foo.php</code> containing an <code>Acme\Foo</code> class.</p>
						<p>After adding the <code>autoload</code> field, you have to re-run <code>install</code> to re-generate
						the <code>vendor/autoload.php</code> file.</p>
						<p>Including that file will also return the autoloader instance, so you can store
						the return value of the include call in a variable and add more namespaces.
						This can be useful for autoloading classes in a test suite, for example.</p>
						<pre><code>$loader = require 'vendor/autoload.php';
						$loader-&gt;add('Acme\Test', __DIR__);
						</code></pre>
						<p>In addition to PSR-0 autoloading, classmap is also supported. This allows
						classes to be autoloaded even if they do not conform to PSR-0. See the
						<a href="04-schema.md#autoload">autoload reference</a> for more details.</p>
						<blockquote>
							<p><strong>Note:</strong> Composer provides its own autoloader. If you don't want to use
							that one, you can just include <code>vendor/composer/autoload_namespaces.php</code>,
							which returns an associative array mapping namespaces to directories.</p>
						</blockquote>
						<p class="prev-next">&larr; <a href="00-intro.md">Intro</a>  |  <a href="02-libraries.md">Libraries</a> &rarr;</p>
						<p class="fork-and-edit">
								Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/01-basic-usage.md">fork and edit</a> it!
						</p>
					</div>
					<footer></footer>
				</div>
		</body>
</html>