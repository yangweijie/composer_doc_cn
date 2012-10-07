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
							<a href="/">Home</a><a class="" href="/doc/00-intro.md">开始</a><a class="" href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                           
						</header>
						<div id="main" role="main">
							<ul class="toc">
								<li>
									<a href="#installation">安装</a> 
								</li>
								<li>
									<a href="#composer-json-project-setup">composer.json: 项目启动</a> 
									<ul>
										<li>
											<a href="#the-require-key">require 键</a> 
										</li>
										<li>
											<a href="#package-names">包名称</a> 
										</li>
										<li>
											<a href="#package-versions">包的版本</a> 
										</li>
									</ul>
								</li>
								<li>
									<a href="#installing-dependencies">安装依赖项</a> 
								</li>
								<li>
									<a href="#composer-lock-the-lock-file">composer.lock - 锁文件</a> 
								</li>
								<li>
									<a href="#packagist">Packagist</a> 
								</li>
								<li>
									<a href="#autoloading">自动加载</a> 
								</li>
							</ul>
							<h1 id="basic-usage">基本用法<a href="#basic-usage" class="anchor">#</a></h1>
							<h2 id="installation">安装<a href="#installation" class="anchor">#</a></h2>
							<p>你只须下载 <code>composer.phar</code> 可执行文件，就能安装Composer。</p>
							<pre><code>$ curl -s http://getcomposer.org/installer | php</code></pre>
							<p>具体信息，请看 <a href="00-intro.md">安装</a> 章节.</p>
							<p>为了测试Composer是否运行，只要用 <code>php</code>运行PHAR文件:</p>
							<pre><code>$ php composer.phar
							</code></pre>
							<p>这会给你一系列的正确命令。</p>
							<blockquote>
								<p><strong>注意：</strong> 你也可以不下载Composer,仅仅通过使用 <code>--check</code> `--check` 选项在线完成上述测试。使用 <code>--help</code>能获得更多信息：</p>
								<pre><code>$ curl -s http://getcomposer.org/installer | php -- --help</code></pre>
							</blockquote>
							<h2 id="composer-json-project-setup"><code>composer.json</code>: 启动项目<a href="#composer-json-project-setup" class="anchor">#</a></h2>
							<p>你仅需要一个 <code>composer.json</code>文件就可以在你的项目中使用Composer,这个文件描述了你项目的依赖关系，并且包含一些元数据。</p>
							<p><a href="http://json.org/">JSON </a> 格式是一种很容易掌握的格式。它允许你使用嵌套的格式描述数据。</p>
							<h3 id="the-require-key"><code>require</code> 键<a href="#the-require-key" class="anchor">#</a></h3>
							<p>唯一需要你指定的就是 <code>require</code>键，向 <code>composer.json</code>描述你项目的决定项。</p>
<pre><code>{
	"require": {
		"monolog/monolog": "1.0.*"
	}
}
</code></pre>
							<p>正如你所见， <code>require</code> 获得一个从 <strong>package names</strong> (比如这里的 <code>monolog/monolog</code>)
							映射到<strong>package versions</strong> (比如 <code>1.0.*</code>)的对象。</p>
							<h3 id="package-names">包名称<a href="#package-names" class="anchor">#</a></h3>
							<p>这里的包的名称包含开发者名称和项目名称。这地方经常产生冲突，所以加上开发者的名称就是为了防止冲突。
两个互不相干的人都可以开发一个叫做 <code>json</code>的库，它们可能就是以<code>igorw/json</code> 和 <code>seldaek/json</code>命名的。</p>
							<p>这里我们需要的是<code>monolog/monolog</code>,所以开发者的名称和项目名称是相同的。我们建议项目使用唯一的名称命名。
这样的话，以后你还能添加相近的项目到同一名称空间下。如果你维护着一个类库，当你需要将它分解成两个部分时，
这将使问题变得相当简单。</p>
							<h3 id="package-versions">包的版本<a href="#package-versions" class="anchor">#</a></h3>
							<p>我们需要monolog的<code>1.0.*</code> 版，这代表 <code>1.0</code>
							下的任一版本，包含 <code>1.0.0</code>, <code>1.0.2</code> 或者 <code>1.0.20</code>。</p>
							<p>版本号可以使用几种不同方式进行约束。</p>
								<ul>
									<li>
										<p><strong>给定版本号:</strong> 你可以指定包的特定版本号，例如<code>1.0.2</code>。这不是很常用，但是有效。</p>
									</li>
									<li>
										<p><strong>给定范围:</strong> 通过使用比较运算符，你可以指定版本号的范围。有效的运算符有:<code>&gt;</code>, <code>&gt;=</code>, <code>&lt;</code>, <code>&lt;=</code>, <code>!=</code>。
例如<code>&gt;=1.0</code>，你也可以指定多个区间，中间用逗号分隔：
								<code>&gt;=1.0,&lt;2.0</code>。
							</p>
							</li>
							<li>
								<p><strong>通配符：</strong>你可以使用<code>*</code>符号指定一个匹配模式。 <code>1.0.*</code> 相当于<code>&gt;=1.0,&lt;1.1-dev</code>。
								</p>
							</li>
							</ul><h2 id="installing-dependencies">安装依赖项<a href="#installing-dependencies" class="anchor">#</a></h2>
						<p>想要在项目中取得指定的依赖项，只须运行
						<code>composer.phar</code>的<code>install</code>命令。</p>
						<pre><code>$ php composer.phar install</code></pre>
						<p>这将会找到<code>monolog/monolog</code> 的满足指定要求的最新版本，并把它下载到<code>vendor</code>路径下。
将第三方库放在统一的 <code>vendor</code>.路径下，将给你带来便利。比如讲monolog放在<code>vendor/monolog/monolog</code>中。</p>
						<blockquote>
							<p><strong>小贴士:</strong> 如果你使用git管理项目代码，你可以将
							<code>vendor</code> 写进  <code>.gitignore</code>文件中. 你不需要将库代码加到你的repos中。</p>
						</blockquote>
						<p><code>install</code> 命令所做的另一件事是在你项目的根目录下添加了一个叫做<code>composer.lock</code>的文件。</p>
						<h2 id="composer-lock-the-lock-file"><code>composer.lock</code> - - 锁文件<a href="#composer-lock-the-lock-file" class="anchor">#</a></h2>
						<p>在安装了依赖项后，Composer将实际安装的版本号写入<code>composer.lock</code> 文件中，这就将项目的依赖项锁定在这些特定的版本中了。</p>
						<p><strong>提交你项目中的  <code>composer.lock</code> (连同  <code>composer.json</code>) 到版本控制系统中。</strong></p>
						<p>这点很重要，因为<code>install</code> 命令会确认这个锁文件是否存在，如果存在的话，Composer就会安装这里面
指定的版本号下载相应的对应项（忽略<code>composer.json</code>
						中的申明）。这意味着，其他任何人部署项目时
都会下载一样的版本。</p>
						<p>如果没有<code>composer.lock</code>文件的存在，Composer会从<code>composer.json</code>读取依赖项以及各种的版本号，
并生成锁文件。</p>
						<p>这也意味着，任何一个依赖项有更新，你不会自动得到最新版本。想要得到最新版，请用<code>update</code> 命令。
这将取得最新的匹配版本（根据 <code>composer.json</code>中定义的版本号）并且同时更新锁文件。</p>
						<pre><code>$ php composer.phar update
						</code></pre>
						<blockquote>
							<p><strong>注意:</strong> 对于类库，不推荐将锁文件签入版本库,
							请阅读： <a href="02-libraries.md#lock-file">库文件 - 锁文件</a>.</p>
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
						<p class="prev-next">&larr; <a href="00-intro.md">简介</a>  |  <a href="02-libraries.md">版本库</a> &rarr;</p>
						<p class="fork-and-edit">
								找到一个错字?文档有错?只要<a href="http://github.com/composer/composer/edit/master02-libraries.md">fork和edit</a>它!
						</p>
					</div>
					<footer></footer>
				</div>
		</body>
</html>