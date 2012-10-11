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
						<strong>--prefer-source:</strong>有两种下载一个包的途径: <code>source</code>
						and <code>dist</code>. 对于稳定版本的composer将会默认使用<code>dist</code>.
						<code>source</code>是一个版本控制库的源.如果<code>--prefer-source</code>启用了, 如果有的话composer将会从<code>source</code>安装.这是很有用的如果你想给项目做一个bugfix和直接从依赖中获取一个本地git clone.
					</li>
					<li><strong>--dry-run:</strong>如果你想要演示一个安装过程但实际上不是真的安装一个包,你可以使用<code>--dry-run</code>. 这个将模拟安装并显示什么将会发生.</li>
					<li><strong>--dev:</strong> 默认的composer将只会安装要求的包.通过传这个选项你也可以安装
						<code>require-dev</code>提供的包.</li>
					<li><strong>--no-scripts:</strong>跳过执行<code>composer.json</code>中定义脚本.</li>
				</ul>
				<h2 id="update">update<a href="#update" class="anchor">#</a></h2>
				<p>为了获取最新的依赖版本并且去更新
					<code>composer.lock</code> 文件,你应该用<code>update</code>命令.</p>
				<pre><code>$ php composer.phar update
</code></pre>
				<p>这个将会解决所有项目的依赖关系然后把精确的版本写入到<code>composer.lock</code>.</p>
				<p>如果你只是想升级一些包并不是全部,你可以全列出他们:</p>
				<pre><code>$ php composer.phar update vendor/package vendor/package2
</code></pre>
				<h3 id="options-3">选项<a href="#options-3" class="anchor">#</a></h3>
				<ul>
					<li><strong>--prefer-source:</strong> 安装包从可用<code>source</code>.</li>
					<li><strong>--dry-run:</strong>模拟命令实际不做任何事 .</li>
					<li><strong>--dev:</strong> 安装在<code>require-dev</code>中列出的包.</li>
					<li><strong>--no-scripts:</strong>跳过执行<code>composer.json</code>中定义脚本.</li>
				</ul>
				<h2 id="require">require<a href="#require" class="anchor">#</a></h2>
				<p>The <code>require</code>命令从当前目录中添加新的包到<code>composer.json</code>文件中.</p>
				<pre><code>$ php composer.phar require
</code></pre>
				<p>在添加/修改要求,修改过的要求将会被安装或更新.</p>
				<p>如果你不想交互的方式选择要求,你可以在命令中传递它们.</p>
				<pre><code>$ php composer.phar require vendor/package:2.* vendor/package2:dev-master
</code></pre>
				<h3 id="options-4">选项<a href="#options-4" class="anchor">#</a></h3>
				<ul>
					<li><strong>--prefer-source:</strong>安装包从可用<code>source</code>.</li>
					<li><strong>--dev:</strong> 添加包到<code>require-dev</code>.</li>
				</ul>
				<h2 id="search">search<a href="#search" class="anchor">#</a></h2>
				<p>search命令允许你在项目包版本库中搜索. 通常这个将只会在packagist. 你可以简单传递你想搜索的模式.</p>
				<pre><code>$ php composer.phar search monolog
</code></pre>
				<p>你也可搜索多个通过传递多个参数.</p>
				<h2 id="show">show<a href="#show" class="anchor">#</a></h2>
				<p>要列出所有可用包,你可以使用<code>show</code>命令.</p>
				<pre><code>$ php composer.phar show
</code></pre>
				<p>如果你想要查看一个包的所有细节,你可以传递包的名称.</p>
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
				<p>你可以甚至传递包版本,这样它会告诉你那个指定版本的细节.</p>
				<pre><code>$ php composer.phar show monolog/monolog 1.0.2
</code></pre>
				<h3 id="options-5">选项<a href="#options-5" class="anchor">#</a></h3>
				<ul>
					<li><strong>--installed:</strong>将会列出已装的包.</li>
					<li><strong>--platform:</strong> Will list only platform packages (php &amp; extensions).</li>
				</ul>
				<h2 id="depends">depends<a href="#depends" class="anchor">#</a></h2>
				<p><code>depends</code>命令告诉你一个确定包依赖哪些其他的包.你可以指定链接类型(<code>require</code>, <code>require-dev</code>)
					在列表中应当包含的.默认的两个都是用.</p>
				<pre><code>$ php composer.phar depends --link-type=require monolog/monolog
nrk/monolog-fluent
poc/poc
propel/propel
symfony/monolog-bridge
symfony/symfony
</code></pre>
				<h3 id="options-6">选项<a href="#options-6" class="anchor">#</a></h3>
				<ul>
					<li><strong>--link-type:</strong> 匹配的链接类型,可被指定多个.</li>
				</ul>
				<h2 id="validate">validate<a href="#validate" class="anchor">#</a></h2>
				<p>你应当一直运行<code>validate</code>命令在你提交
					<code>composer.json</code>文件,和在你标签一个发布.他将会检测是否你的
					<code>composer.json</code>合法.</p>
				<pre><code>$ php composer.phar validate
</code></pre>
				<h2 id="self-update">self-update<a href="#self-update" class="anchor">#</a></h2>
				<p>要升级composer自身到最新的版本,只要运行<code>self-update</code>
					命令.它将会替换你的<code>composer.phar</code>为最新版本.</p>
				<pre><code>$ php composer.phar self-update
</code></pre>
				<p>如果你已经安装了composer为你整个系统(see <a href="00-intro.md#globally">全局安装</a>),
					你不得不安装以<code>root</code>权限运行命令</p>
				<pre><code>$ sudo composer self-update
</code></pre>
				<h2 id="create-project">create-project<a href="#create-project" class="anchor">#</a></h2>
				<p>你可以用Composer来创建新的项目通过一个已存在的包.
					有几个用此的应用:</p>
				<ol>
					<li>你可以部署应用包.</li>
					<li>举个例子你可以检出任何包并且开发补丁包.</li>
					<li>多人开发的项目可以使用此特性加速应用开发的初始化.</li>
				</ol>
				<p>要使用composer创建一个新项目你可以使用"create-project"命令.
					传一个包名称,还有创建项目的目录. 你可以提供一个版本作为第3个参数,否则使用最新版.</p>
				<p>目录不存在的话,安装时会自动被创建.</p>
				<pre><code>php composer.phar create-project doctrine/orm path 2.2.0
</code></pre>
				<p>默认命令检测packagist.org上的包.</p>
				<h3 id="options-7">Options<a href="#options-7" class="anchor">#</a></h3>
				<ul><li><strong>--repository-url:</strong> 提供一个定制的版本库来搜索包,
						将会替换packagist. 既可以是一个HTTP URL指向一个<code>composer</code>版本库,或者一个路径指向一个本地<code>packages.json</code>文件.</li>
					<li><strong>--prefer-source:</strong> 从版本控制中获取开发版代码.</li>
					<li><strong>--dev:</strong> 安装列在<code>require-dev</code>中的包.</li>
				</ul><h2 id="dump-autoload">dump-autoload<a href="#dump-autoload" class="anchor">#</a></h2>
				<p>如果你需要个更新autoloader因为一个类映射包内有新的类了,你可以使用"dump-autoload"来完成那个而不是使用安装或者更新.（ps：以下未理解就不翻译了）</p>
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
				<p>要获得更多某个命令的详细信息就用<code>help</code>.</p>
				<pre><code>$ php composer.phar help install
</code></pre>
				<h2 id="environment-variables">环境变量<a href="#environment-variables" class="anchor">#</a></h2>
				<p>你可以设置一些环境变量覆盖一些配置.
					尽可能的情况下推荐指定这些配置在<code>composer.json</code><code>config</code>
					部分而不是设置环境变量.值得注意的是env vars（环境变量）
					总是优先覆盖指定在<code>composer.json</code>中的值.</p>
				<h3 id="composer">COMPOSER<a href="#composer" class="anchor">#</a></h3>
				<p>通过指定<code>COMPOSER</code> 环境变量可以指定<code>composer.json</code>文件名为其他的.</p>
				<p>举个例子:</p>
				<pre><code>$ COMPOSER=composer-other.json php composer.phar install
</code></pre>
				<h3 id="composer-root-version">COMPOSER_ROOT_VERSION<a href="#composer-root-version" class="anchor">#</a></h3>
				<p>通过设置这个变量你可以指定root包的版本,如果它不能通过VCS猜到还有没有在<code>composer.json</code>指定.</p>
				<h3 id="composer-vendor-dir">COMPOSER_VENDOR_DIR<a href="#composer-vendor-dir" class="anchor">#</a></h3>
				<p>通过设置这个变量你可以使composer安装依赖到一个目录而不是总是<code>vendor</code>.</p>
				<h3 id="composer-bin-dir">COMPOSER_BIN_DIR<a href="#composer-bin-dir" class="anchor">#</a></h3>
				<p>通过设置这个选项你可以改变<code>bin</code> (<a href="articles/vendor-bins.md">Vendor Bins</a>)
					目录到其他的目录而不是<code>vendor/bin</code>.</p>
				<h3 id="http-proxy-or-http-proxy">http_proxy or HTTP_PROXY<a href="#http-proxy-or-http-proxy" class="anchor">#</a></h3>
				<p>如果你整用HTTP proxy访问composer你可以使用基本的
					<code>http_proxy</code>或<code>HTTP_PROXY</code>环境变量.简单的设置它为你的代理的URL.
					许多操作系统已经为你设好了这个变量.</p>
				<p>最好使用<code>http_proxy</code> (小写)甚至2个都定义因为一些工具比如git或curl将只是用小写的<code>http_proxy</code>版本.
					相反你可以指定git proxy通过
					<code>git config --global http.proxy &lt;proxy url&gt;</code>.</p>
				<h3 id="composer-home">COMPOSER_HOME<a href="#composer-home" class="anchor">#</a></h3>
				<p><code>COMPOSER_HOME</code>变量允许你改变composer home目录.它是一个隐藏的全局(该机器上所有用户) 所有项目共享的目录.</p>
				<p>默认的它指向到<code>/home/&lt;user&gt;/.composer</code> 在 *nix,
					<code>/Users/&lt;user&gt;/.composer</code> 在OSX and
					<code>C:\Users\&lt;user&gt;\AppData\Roaming\Composer</code> 在Windows.</p>
				<h4 id="composer-home-config-json">COMPOSER_HOME/config.json<a href="#composer-home-config-json" class="anchor">#</a></h4>
				<p>你可以放一个<code>config.json</code>文件到<code>COMPOSER_HOME</code> 指向的位置. Composer 将会把它和你的项目的<code>composer.json</code>合并当你运行<code>install</code>和<code>update</code>命令时.</p>
				<p>该文件允许你为用户的项目设置<a href="04-schema.md#config">配置</a>和<a href="05-repositories.md">版本库</a>.</p>
				<p>在全局配置和<em>local</em>配置冲突时,项目中的<em>local</em>配置<code>composer.json</code> 总是赢.</p>
				<h3 id="composer-process-timeout">COMPOSER_PROCESS_TIMEOUT<a href="#composer-process-timeout" class="anchor">#</a></h3>
				<p>这个环境变量控制着composer等待命令(比如git命令)的时间后完成执行.默认值是300秒 (5分钟).</p>
				<p class="prev-next">&larr; <a href="02-libraries.md">库</a>  |  <a href="04-schema.md">Schema</a> &rarr;</p>
				<p class="fork-and-edit">
					找到一个错字?文档有错?只要<a href="http://github.com/composer/composer/edit/master02-libraries.md">fork和edit</a>它!
				</p>
			</div>
			<footer></footer>
		</div>
	</body>
</html>