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
						<a href="#dependency-management">依赖处理</a> 
					</li>
					<li>
						<a href="#declaring-dependencies">声明依赖关系</a> 
					</li>
					<li>
						<a href="#installation">安装</a> 
						<ul>
							<li>
								<a href="#downloading-the-composer-executable">下载Composer</a> 
								<ul>
									<li>
										<a href="#locally">局部性安装</a> 
									</li>
									<li>
										<a href="#globally">全局性安装</a> 
									</li>
								</ul>
							</li>
							<li>
								<a href="#using-composer">使用 Composer</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#autoloading">自动加载</a> 
					</li>
				</ul>
				<h1 id="introduction">说明<a href="#introduction" class="anchor">#</a></h1>
				<p>Composer 是一个PHP的依赖处理工具。它允许你申明项目所依赖的代码库，然后为你安装他们。</p>
				<h2 id="dependency-management">依赖处理<a href="#dependency-management" class="anchor">#</a></h2>
				<p>Composer 不是包管理程序.虽然它处理包或者库，但是它急于项目之上处理它们，将它们安装在你项目的路径（比如 'vendor'）下。默认的，它不会全局地安装。因此它是一个依赖处理程序。</p>
				<p>这种想法不是新奇的，Composer 受到 node's <a href="http://npmjs.org/">npm</a>
				和 ruby's <a href="http://gembundler.com/">bundler</a>的鼓舞。 但是PHP却没有类似的工具。</p>
				<p>Composer 处理如下问题：</p>
				<p>a) 你的项目基于多个代码库</p>
				<p>b) 这些代码库又依赖于其他库文件</p>
				<p>c) 你只须说明你依赖什么</p>
				<p>d) Composer 会找出某个库的某个版本需要被安装，并且安装它们（或者说，将它们下载到你的项目中）</p>
				<h2 id="declaring-dependencies">声明依赖关系<a href="#declaring-dependencies" class="anchor">#</a></h2>
				<p>让我们假设你正在创建一个项目，并且你需要一个库帮你处理打印log信息，然后你决定 使用 <a href="https://github.com/Seldaek/monolog">monolog</a>。为了将它加入到你的项目中去， 你要做的仅仅是创建一个 <code>composer.json</code> 文件，里面对说明了项目的依赖性。</p>
<pre><code>{
    "require": {
        "monolog/monolog": "1.0.*"
    }
}
</code></pre>
				<p>我们简单的称述了我们项目需要 版本大于 1.0 的 <code>monolog/monolog</code>包</p>
				<h2 id="installation">安装<a href="#installation" class="anchor">#</a></h2>
				<h3 id="downloading-the-composer-executable">下载Composer<a href="#downloading-the-composer-executable" class="anchor">#</a></h3>
				<h4 id="locally">局部性安装<a href="#locally" class="anchor">#</a></h4>
				<p>为了获得Composer的帮助，我们需要完成两件事情。第一件是安装Composer (再次说一下，要做的仅仅是将它下载进你的项目中)</p>
				<pre><code>$ curl -s https://getcomposer.org/installer | php</code></pre>
				<p>这操作仅仅确认一些PHP的设置，然后下载 <code>composer.phar</code> 到你的工作目录。这个就是Composer库。 这是个PHAR格式文件（PHP 文件），它可以帮助用户在命令行下完成一些操作。</p>
				<p>你可以使用 <code>--install-dir</code>
				选项附上目标路径（绝对路径或者相当路径均可）选择Composer的安装路径：</p>
				<pre><code>$ curl -s https://getcomposer.org/installer | php -- --install-dir=bin</code></pre>
				<h4 id="globally">全局性安装<a href="#globally" class="anchor">#</a></h4>
				<p>你可以将上述文件置于你想要的任何位置。不过如果你选择将它放在系统  <code>PATH</code>路径下， 你就可以全局的调用它。在类Unix系统中，你甚至可以在使用时不加 <code>php</code>前缀.</p>
				<p>运行一下命令，你将轻松的使得 <code>composer</code> 可以全局调用：</p>
				<pre><code>$ curl -s https://getcomposer.org/installer | php
$ sudo mv composer.phar /usr/local/bin/composer</code></pre>
				<p>接下来，只须输入 <code>composer</code> 就可以运行 composer了</p>
				<h3 id="using-composer">使用 Composer<a href="#using-composer" class="anchor">#</a></h3>
				<p>然后，运行 <code>install</code> 命令解决库的依赖关系：</p>
				<pre><code>$ php composer.phar install</code></pre>
				<p>这将会下载 monolog 到 <code>vendor/monolog/monolog</code> vendor/monolog/monolog 路径下。</p>
				<h2 id="autoloading">自动加载<a href="#autoloading" class="anchor">#</a></h2>
				<p>除了将库文件下载下来之外，Composer还为你准备了一个自动加载文件帮你加载代码库中的类。 使用它只须在你的引导文件中加入如下代码：</p>
				<pre><code>require 'vendor/autoload.php';</code></pre>
				<p>哇唔! 现在就可以使用 monolog 了! 请继续学习Composer的更多内容，请继续阅读 "Basic Usage" 章节。</p>
				<p class="prev-next"><a href="01-basic-usage.md">Basic Usage</a> &rarr;</p>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/00-intro.md">fork and edit</a> it!
				</p>
			</div>
			<footer></footer>
		</div>
	</body>
</html>