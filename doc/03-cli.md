<!DOCTYPE html>
<html class="no-js">
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
				<a href="/">Home</a><a class="" href="00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>
			</header>
			<div id="main" role="main">
				<ul class="toc">
					<li>
						<a href="#init">init</a> 
						<ul>
							<li>
								<a href="#options">选项</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#install">install</a> 
						<ul>
							<li>
								<a href="#options-2">选项</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#update">update</a> 
						<ul>
							<li>
								<a href="#options-3">选项</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#require">require</a> 
						<ul>
							<li>
								<a href="#options-4">选项</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#search">search</a> 
					</li>
					<li>
						<a href="#show">show</a> 
						<ul>
							<li>
								<a href="#options-5">选项</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#depends">depends</a> 
						<ul>
							<li>
								<a href="#options-6">选项</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#validate">validate</a> 
					</li>
					<li>
						<a href="#self-update">self-update</a> 
					</li>
					<li>
						<a href="#create-project">create-project</a> 
						<ul>
							<li>
								<a href="#options-7">选项</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#dump-autoload">dump-autoload</a> 
						<ul>
							<li>
								<a href="#options-8">选项</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#help">help</a> 
					</li>
					<li>
						<a href="#environment-variables">Environment variables</a> 
						<ul>
							<li>
								<a href="#composer">COMPOSER</a> 
							</li>
							<li>
								<a href="#composer-root-version">COMPOSER_ROOT_VERSION</a> 
							</li>
							<li>
								<a href="#composer-vendor-dir">COMPOSER_VENDOR_DIR</a> 
							</li>
							<li>
								<a href="#composer-bin-dir">COMPOSER_BIN_DIR</a> 
							</li>
							<li>
								<a href="#http-proxy-or-http-proxy">http_proxy or HTTP_PROXY</a> 
							</li>
							<li>
								<a href="#composer-home">COMPOSER_HOME</a> 
								<ul>
									<li>
										<a href="#composer-home-config-json">COMPOSER_HOME/config.json</a> 
									</li>
								</ul>
							</li>
							<li>
								<a href="#composer-process-timeout">COMPOSER_PROCESS_TIMEOUT</a> 
							</li>
						</ul>
					</li>
				</ul>
				<h1 id="command-line-interface">命令行交互<a href="#command-line-interface" class="anchor">#</a></h1>
				<p>你已经学了如何使用命令行交互来完成一些事.本章节说明了所有可用命令的文档.</p>
				<h2 id="init">init<a href="#init" class="anchor">#</a></h2>
				<p>在<a href="02-libraries.md">版本库</a>章节中我们看了如何亲自创建一个
					<code>composer.json</code>.这里也有一个<code>init</code>命令可用更容易做到.</p>
				<p>当你运行命令它会交互的让你填上对应的字段,有时会智能的使用一些默认值.</p>
				<pre><code>$ php composer.phar init
</code></pre>
				<h3 id="options">Options<a href="#options" class="anchor">#</a></h3>
				<ul><li><strong>--no-interaction:</strong> (<strong>-n</strong>)运行命令以非交互模式.
						剩下的那些选项只有在这个模式里才会起作用.</li>
					<li><strong>--name:</strong>包的名字.</li>
					<li><strong>--description:</strong>包描述.</li>
					<li><strong>--author:</strong>包作者.</li>
					<li><strong>--homepage:</strong>包主页.</li>
					<li><strong>--require:</strong> 要引入的有版本约束的包.应当符合以下格式<code>foo/bar:1.0.0</code>.</li>
					<li><strong>--require-dev:</strong>开发版要求,见<strong>--require</strong>.</li>
				</ul><h2 id="install">install<a href="#install" class="anchor">#</a></h2>
				<p>The <code>install</code>命令读取<code>composer.json</code>文件在当前目录,解决了依赖关系,并且安装他们到<code>vendor</code>.</p>
				<pre><code>$ php composer.phar install
</code></pre>
				<p>如果当前目录里有一个<code>composer.lock</code>文件,他将会使用使用确切的版本而不是解析它们.这个保证了每个人使用库得到同样的版本依赖.</p>
				<p>如果没有<code>composer.lock</code>文件,composer将会在解决依赖后创建一个.</p>
				<h3 id="options-2">Options<a href="#options-2" class="anchor">#</a></h3>
				<ul>
					<li>
						<strong>--prefer-source:</strong> There are two ways of downloading a package: <code>source</code>
						and <code>dist</code>. For stable versions composer will use the <code>dist</code> by default.
						The <code>source</code> is a version control repository. If <code>--prefer-source</code> is
						enabled, composer will install from <code>source</code> if there is one. This is
						useful if you want to make a bugfix to a project and get a local git
						clone of the dependency directly.
					</li>
					<li><strong>--dry-run:</strong> If you want to run through an installation without actually
						installing a package, you can use <code>--dry-run</code>. This will simulate the
						installation and show you what would happen.</li>
					<li><strong>--dev:</strong> By default composer will only install required packages. By
						passing this option you can also make it install packages referenced by
						<code>require-dev</code>.</li>
					<li><strong>--no-scripts:</strong> Skips execution of scripts defined in <code>composer.json</code>.</li>
				</ul>
				<h2 id="update">update<a href="#update" class="anchor">#</a></h2>
				<p>In order to get the latest versions of the dependencies and to update the
					<code>composer.lock</code> file, you should use the <code>update</code> command.</p>
				<pre><code>$ php composer.phar update
</code></pre>
				<p>This will resolve all dependencies of the project and write the exact versions
					into <code>composer.lock</code>.</p>
				<p>If you just want to update a few packages and not all, you can list them as such:</p>
				<pre><code>$ php composer.phar update vendor/package vendor/package2
</code></pre>
				<h3 id="options-3">Options<a href="#options-3" class="anchor">#</a></h3>
				<ul>
					<li><strong>--prefer-source:</strong> Install packages from <code>source</code> when available.</li>
					<li><strong>--dry-run:</strong> Simulate the command without actually doing anything.</li>
					<li><strong>--dev:</strong> Install packages listed in <code>require-dev</code>.</li>
					<li><strong>--no-scripts:</strong> Skips execution of scripts defined in <code>composer.json</code>.</li>
				</ul>
				<h2 id="require">require<a href="#require" class="anchor">#</a></h2>
				<p>The <code>require</code> command adds new packages to the <code>composer.json</code> file from
					the current directory.</p>
				<pre><code>$ php composer.phar require
</code></pre>
				<p>After adding/changing the requirements, the modified requirements will be
					installed or updated.</p>
				<p>If you do not want to choose requirements interactively, you can just pass them
					to the command.</p>
				<pre><code>$ php composer.phar require vendor/package:2.* vendor/package2:dev-master
</code></pre>
				<h3 id="options-4">Options<a href="#options-4" class="anchor">#</a></h3>
				<ul>
					<li><strong>--prefer-source:</strong> Install packages from <code>source</code> when available.</li>
					<li><strong>--dev:</strong> Add packages to <code>require-dev</code>.</li>
				</ul>
				<h2 id="search">search<a href="#search" class="anchor">#</a></h2>
				<p>The search command allows you to search through the current project's package
					repositories. Usually this will be just packagist. You simply pass it the
					terms you want to search for.</p>
				<pre><code>$ php composer.phar search monolog
</code></pre>
				<p>You can also search for more than one term by passing multiple arguments.</p>
				<h2 id="show">show<a href="#show" class="anchor">#</a></h2>
				<p>To list all of the available packages, you can use the <code>show</code> command.</p>
				<pre><code>$ php composer.phar show
</code></pre>
				<p>If you want to see the details of a certain package, you can pass the package
					name.</p>
				<pre><code>$ php composer.phar show monolog/monolog
name     : monolog/monolog
versions : master-dev, 1.0.2, 1.0.1, 1.0.0, 1.0.0-RC1
type     : library
names    : monolog/monolog
source   : [git] http://github.com/Seldaek/monolog.git 3d4e60d0cbc4b888fe5ad223d77964428b1978da
dist     : [zip] http://github.com/Seldaek/monolog/zipball/3d4e60d0cbc4b888fe5ad223d77964428b1978da 3d4e60d0cbc4b888fe5ad223d77964428b1978da
license  : MIT

autoload
psr-0
Monolog : src/

requires
php &gt;=5.3.0
</code></pre>
				<p>You can even pass the package version, which will tell you the details of that
					specific version.</p>
				<pre><code>$ php composer.phar show monolog/monolog 1.0.2
</code></pre>
				<h3 id="options-5">Options<a href="#options-5" class="anchor">#</a></h3>
				<ul>
					<li><strong>--installed:</strong> Will list the packages that are installed.</li>
					<li><strong>--platform:</strong> Will list only platform packages (php &amp; extensions).</li>
				</ul>
				<h2 id="depends">depends<a href="#depends" class="anchor">#</a></h2>
				<p>The <code>depends</code> command tells you which other packages depend on a certain
					package. You can specify which link types (<code>require</code>, <code>require-dev</code>)
					should be included in the listing. By default both are used.</p>
				<pre><code>$ php composer.phar depends --link-type=require monolog/monolog
nrk/monolog-fluent
poc/poc
propel/propel
symfony/monolog-bridge
symfony/symfony
</code></pre>
				<h3 id="options-6">Options<a href="#options-6" class="anchor">#</a></h3>
				<ul>
					<li><strong>--link-type:</strong> The link types to match on, can be specified multiple
						times.</li>
				</ul>
				<h2 id="validate">validate<a href="#validate" class="anchor">#</a></h2>
				<p>You should always run the <code>validate</code> command before you commit your
					<code>composer.json</code> file, and before you tag a release. It will check if your
					<code>composer.json</code> is valid.</p>
				<pre><code>$ php composer.phar validate
</code></pre>
				<h2 id="self-update">self-update<a href="#self-update" class="anchor">#</a></h2>
				<p>To update composer itself to the latest version, just run the <code>self-update</code>
					command. It will replace your <code>composer.phar</code> with the latest version.</p>
				<pre><code>$ php composer.phar self-update
</code></pre>
				<p>If you have installed composer for your entire system (see <a href="00-intro.md#globally">global installation</a>),
					you have to run the command with <code>root</code> privileges</p>
				<pre><code>$ sudo composer self-update
</code></pre>
				<h2 id="create-project">create-project<a href="#create-project" class="anchor">#</a></h2>
				<p>You can use Composer to create new projects from an existing package.
					There are several applications for this:</p>
				<ol>
					<li>You can deploy application packages.</li>
					<li>You can check out any package and start developing on patches for example.</li>
					<li>Projects with multiple developers can use this feature to bootstrap the
						initial application for development.</li>
				</ol>
				<p>To create a new project using composer you can use the "create-project" command.
					Pass it a package name, and the directory to create the project in. You can also
					provide a version as third argument, otherwise the latest version is used.</p>
				<p>The directory is not allowed to exist, it will be created during installation.</p>
				<pre><code>php composer.phar create-project doctrine/orm path 2.2.0
</code></pre>
				<p>By default the command checks for the packages on packagist.org.</p>
				<h3 id="options-7">Options<a href="#options-7" class="anchor">#</a></h3>
				<ul><li><strong>--repository-url:</strong> Provide a custom repository to search for the package,
						which will be used instead of packagist. Can be either an HTTP URL pointing
						to a <code>composer</code> repository, or a path to a local <code>packages.json</code> file.</li>
					<li><strong>--prefer-source:</strong> Get a development version of the code checked out
						from version control.</li>
					<li><strong>--dev:</strong> Install packages listed in <code>require-dev</code>.</li>
				</ul><h2 id="dump-autoload">dump-autoload<a href="#dump-autoload" class="anchor">#</a></h2>
				<p>If you need to update the autoloader because of new classes in a classmap
					package for example, you can use "dump-autoload" to do that without having to
					go through an install or update.</p>
				<p>Additionally, it can dump an optimized autoloader that converts PSR-0 packages
					into classmap ones for performance reasons. In large applications with many
					classes, the autoloader can take up a substantial portion of every request's
					time. Using classmaps for everything is less convenient in development, but
					using this option you can still use PSR-0 for convenience and classmaps for
					performance.</p>
				<h3 id="options-8">Options<a href="#options-8" class="anchor">#</a></h3>
				<ul><li><strong>--optimize:</strong> Convert PSR-0 autoloading to classmap to get a faster
						autoloader. This is recommended especially for production, but can take
						a bit of time to run so it is currently not done by default.</li>
				</ul><h2 id="help">help<a href="#help" class="anchor">#</a></h2>
				<p>To get more information about a certain command, just use <code>help</code>.</p>
				<pre><code>$ php composer.phar help install
</code></pre>
				<h2 id="environment-variables">Environment variables<a href="#environment-variables" class="anchor">#</a></h2>
				<p>You can set a number of environment variables that override certain settings.
					Whenever possible it is recommended to specify these settings in the <code>config</code>
					section of <code>composer.json</code> instead. It is worth noting that that the env vars
					will always take precedence over the values specified in <code>composer.json</code>.</p>
				<h3 id="composer">COMPOSER<a href="#composer" class="anchor">#</a></h3>
				<p>By setting the <code>COMPOSER</code> env variable it is possible to set the filename of
					<code>composer.json</code> to something else.</p>
				<p>For example:</p>
				<pre><code>$ COMPOSER=composer-other.json php composer.phar install
</code></pre>
				<h3 id="composer-root-version">COMPOSER_ROOT_VERSION<a href="#composer-root-version" class="anchor">#</a></h3>
				<p>By setting this var you can specify the version of the root package, if it can
					not be guessed from VCS info and is not present in <code>composer.json</code>.</p>
				<h3 id="composer-vendor-dir">COMPOSER_VENDOR_DIR<a href="#composer-vendor-dir" class="anchor">#</a></h3>
				<p>By setting this var you can make composer install the dependencies into a
					directory other than <code>vendor</code>.</p>
				<h3 id="composer-bin-dir">COMPOSER_BIN_DIR<a href="#composer-bin-dir" class="anchor">#</a></h3>
				<p>By setting this option you can change the <code>bin</code> (<a href="articles/vendor-bins.md">Vendor Bins</a>)
					directory to something other than <code>vendor/bin</code>.</p>
				<h3 id="http-proxy-or-http-proxy">http_proxy or HTTP_PROXY<a href="#http-proxy-or-http-proxy" class="anchor">#</a></h3>
				<p>If you are using composer from behind an HTTP proxy, you can use the standard
					<code>http_proxy</code> or <code>HTTP_PROXY</code> env vars. Simply set it to the URL of your proxy.
					Many operating systems already set this variable for you.</p>
				<p>Using <code>http_proxy</code> (lowercased) or even defining both might be preferable since
					some tools like git or curl will only use the lower-cased <code>http_proxy</code> version.
					Alternatively you can also define the git proxy using
					<code>git config --global http.proxy &lt;proxy url&gt;</code>.</p>
				<h3 id="composer-home">COMPOSER_HOME<a href="#composer-home" class="anchor">#</a></h3>
				<p>The <code>COMPOSER_HOME</code> var allows you to change the composer home directory. This
					is a hidden, global (per-user on the machine) directory that is shared between
					all projects.</p>
				<p>By default it points to <code>/home/&lt;user&gt;/.composer</code> on *nix,
					<code>/Users/&lt;user&gt;/.composer</code> on OSX and
					<code>C:\Users\&lt;user&gt;\AppData\Roaming\Composer</code> on Windows.</p>
				<h4 id="composer-home-config-json">COMPOSER_HOME/config.json<a href="#composer-home-config-json" class="anchor">#</a></h4>
				<p>You may put a <code>config.json</code> file into the location which <code>COMPOSER_HOME</code> points
					to. Composer will merge this configuration with your project's <code>composer.json</code>
					when you run the <code>install</code> and <code>update</code> commands.</p>
				<p>This file allows you to set <a href="04-schema.md#config">configuration</a> and
					<a href="05-repositories.md">repositories</a> for the user's projects.</p>
				<p>In case global configuration matches <em>local</em> configuration, the <em>local</em>
					configuration in the project's <code>composer.json</code> always wins.</p>
				<h3 id="composer-process-timeout">COMPOSER_PROCESS_TIMEOUT<a href="#composer-process-timeout" class="anchor">#</a></h3>
				<p>This env var controls the time composer waits for commands (such as git
					commands) to finish executing. The default value is 300 seconds (5 minutes).</p>
				<p class="prev-next">&larr; <a href="02-libraries.md">Libraries</a>  |  <a href="04-schema.md">Schema</a> &rarr;</p>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/03-cli.md">fork and edit</a> it!
				</p>
			</div>
			<footer></footer>
		</div>
	</body>
</html>