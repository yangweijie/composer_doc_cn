<!DOCTYPE html>
<html class="no-js" lang="zh">
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
				<a href="/">Home</a><a class="active" href="/doc/00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                           
			 </header>
			<div id="main" role="main">
				<ul class="toc">
					<li>
						<a href="#dependency-management">Dependency management</a> 
					</li>
					<li>
						<a href="#declaring-dependencies">Declaring dependencies</a> 
					</li>
					<li>
						<a href="#installation">Installation</a> 
						<ul>
							<li>
								<a href="#downloading-the-composer-executable">Downloading the Composer Executable</a> 
								<ul>
									<li>
										<a href="#locally">Locally</a> 
									</li>
									<li>
										<a href="#globally">Globally</a> 
									</li>
								</ul>
							</li>
							<li>
								<a href="#using-composer">Using Composer</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#autoloading">Autoloading</a> 
					</li>
				</ul>
				<h1 id="introduction">Introduction<a href="#introduction" class="anchor">#</a></h1>
				<p>Composer is a tool for dependency management in PHP. It allows you to declare
				the dependent libraries your project needs and it will install them in your
				project for you.</p>
				<h2 id="dependency-management">Dependency management<a href="#dependency-management" class="anchor">#</a></h2>
				<p>Composer is not a package manager. Yes, it deals with "packages" or libraries, but
				it manages them on a per-project basis, installing them in a directory (e.g. <code>vendor</code>)
				inside your project. By default it will never install anything globally. Thus,
				it is a dependency manager.</p>
				<p>This idea is not new and Composer is strongly inspired by node's <a href="http://npmjs.org/">npm</a>
				and ruby's <a href="http://gembundler.com/">bundler</a>. But there has not been such a tool
				for PHP.</p>
				<p>The problem that Composer solves is this:</p>
				<p>a) You have a project that depends on a number of libraries.</p>
				<p>b) Some of those libraries depend on other libraries .</p>
				<p>c) You declare the things you depend on</p>
				<p>d) Composer finds out which versions of which packages need to be installed, and
				   installs them (meaning it downloads them into your project).</p>
				<h2 id="declaring-dependencies">Declaring dependencies<a href="#declaring-dependencies" class="anchor">#</a></h2>
				<p>Let's say you are creating a project, and you need a library that does logging.
				You decide to use <a href="https://github.com/Seldaek/monolog">monolog</a>. In order to
				add it to your project, all you need to do is create a <code>composer.json</code> file
				which describes the project's dependencies.</p>
				<pre><code>{
					"require": {
						"monolog/monolog": "1.0.*"
					}
				}
				</code></pre>
				<p>We are simply stating that our project requires some <code>monolog/monolog</code> package,
				any version beginning with <code>1.0</code>.</p>
				<h2 id="installation">Installation<a href="#installation" class="anchor">#</a></h2>
				<h3 id="downloading-the-composer-executable">Downloading the Composer Executable<a href="#downloading-the-composer-executable" class="anchor">#</a></h3>
				<h4 id="locally">Locally<a href="#locally" class="anchor">#</a></h4>
				<p>To actually get Composer, we need to do two things. The first one is installing
				Composer (again, this mean downloading it into your project):</p>
				<pre><code>$ curl -s https://getcomposer.org/installer | php
				</code></pre>
				<p>This will just check a few PHP settings and then download <code>composer.phar</code> to
				your working directory. This file is the Composer binary. It is a PHAR (PHP
				archive), which is an archive format for PHP which can be run on the command
				line, amongst other things.</p>
				<p>You can install Composer to a specific directory by using the <code>--install-dir</code>
				option and providing a target directory (it can be an absolute or relative path):</p>
				<pre><code>$ curl -s https://getcomposer.org/installer | php -- --install-dir=bin
				</code></pre>
				<h4 id="globally">Globally<a href="#globally" class="anchor">#</a></h4>
				<p>You can place this file anywhere you wish. If you put it in your <code>PATH</code>,
				you can access it globally. On unixy systems you can even make it
				executable and invoke it without <code>php</code>.</p>
				<p>You can run these commands to easily access <code>composer</code> from anywhere on your system:</p>
				<pre><code>$ curl -s https://getcomposer.org/installer | php
				$ sudo mv composer.phar /usr/local/bin/composer
				</code></pre>
				<p>Then, just run <code>composer</code> in order to run composer</p>
				<h3 id="using-composer">Using Composer<a href="#using-composer" class="anchor">#</a></h3>
				<p>Next, run the <code>install</code> command to resolve and download dependencies:</p>
				<pre><code>$ php composer.phar install
				</code></pre>
				<p>This will download monolog into the <code>vendor/monolog/monolog</code> directory.</p>
				<h2 id="autoloading">Autoloading<a href="#autoloading" class="anchor">#</a></h2>
				<p>Besides downloading the library, Composer also prepares an autoload file that's
				capable of autoloading all of the classes in any of the libraries that it
				downloads. To use it, just add the following line to your code's bootstrap
				process:</p>
				<pre><code>require 'vendor/autoload.php';
				</code></pre>
				<p>Woh! Now start using monolog! To keep learning more about Composer, keep
				reading the "Basic Usage" chapter.</p>
				<p class="prev-next"><a href="01-basic-usage.md">Basic Usage</a> &rarr;</p>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/00-intro.md">fork and edit</a> it!
				</p>
			</div>
			<footer></footer>
		</div>
	</body>
</html>