<!DOCTYPE html>
<html class="no-js" lang="en">
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
				<a href="/">Home</a><a class="" href="00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>
			</header>
			<div id="main" role="main">
				<ul class="toc">
					<li>
						<a href="#every-project-is-a-package">每个项目是个包(package)</a> 
					</li>
					<li>
						<a href="#specifying-the-version">指定版本</a> 
						<ul>
							<li>
								<a href="#tags">标签</a> 
							</li>
							<li>
								<a href="#branches">分支</a> 
							</li>
							<li>
								<a href="#aliases">别名</a> 
							</li>
						</ul>
					</li>
					<li>
						<a href="#lock-file">文件锁</a> 
					</li>
					<li>
						<a href="#light-weight-distribution-packages">轻型发布包</a> 
					</li>
					<li>
						<a href="#publishing-to-a-vcs">发布到一个VCS</a> 
					</li>
					<li>
						<a href="#publishing-to-packagist">发布到packagist</a> 
					</li>
				</ul>
				<h1 id="libraries">库<a href="#libraries" class="anchor">#</a></h1>
				<p>本章节将告诉你如何通过composer使你的库可安装。</p>
				<h2 id="every-project-is-a-package">
					每个项目是个包<a href="#every-project-is-a-package" class="anchor">#</a>
				</h2>
				<p>只要你有一个 <code>composer.json</code>在一个目录里,那个目录就是一个包。当你添加一个<code>require</code>到一个项目,你正在做一个依赖其他包的包. 你的项目和库之间的唯一区别是你的项目是一个没有名字的包.</p>
				<p>为了使那个包可安装你需要给它一个名字.你可以做到通过添加一个<code>name</code>到<code>composer.json</code>:</p>
				<pre><code>{
	"name": "acme/hello-world",
	"require": {
		"monolog/monolog": "1.0.*"
	}
}
</code></pre>
				<p>在这个例子里项目名是<code>acme/hello-world</code>, 那里<code>acme</code>是vendor名字.必须提供一个vendor名字.</p>
				<blockquote>
					<p><strong>注意:</strong>如果你不知道用什么作为一个vendor名字, 你的GitHub
						用户名通常是一个不错的选择. 尽管包名字是区分大小写的,惯例是所有字母小写单词之间用破折号隔开(-).</p>
				</blockquote>
				<h2 id="specifying-the-version">指定版本<a href="#specifying-the-version" class="anchor">#</a></h2>
				<p>您需要指定包的版本. 当你在Packagist上发布包时,它能从版本控制系统VCS (git, svn,
					hg) 推断版本信息,因此在那种情况下你不需要指定它并且也不推荐指定.看<a href="#tags">标签</a>和<a href="#branches">分支</a>看看如何从这些中提取版本号的.</p>
				<p>如果你手动创建一个包，
					你可以添加一个<code>version</code>字段:</p>
				<pre><code>{
	"version": "1.0.0"
}
</code></pre>
				<h3 id="tags">标签<a href="#tags" class="anchor">#</a></h3>
				<p>对于每个看上去像一个版本的标签, 那个标签的包版本将被创建. 它应当符合'X.Y.Z'或'vX.Y.Z', 有时可以有一个后缀如RC,
					beta, alpha or patch.</p>
				<p>下面是一些合法标签的名字:</p>
				<pre><code>1.0.0
v1.0.0
1.10.5-RC1
v4.4.4beta2
v2.0.0-alpha
v2.0.4-p1
</code></pre>
				<blockquote>
					<p><strong>注意:</strong>如果你指定一个明确的版本在<code>composer.json</code>中,标签名必须符合指定版本的格式.</p>
				</blockquote>
				<h3 id="branches">分支<a href="#branches" class="anchor">#</a></h3>
				<p>对于每个分支,一个包的开发版本将被创建.如果分支名看上去像一个版本,版本将会是<code>{branchname}-dev</code>. 举个例子，
					一个<code>2.0</code>分支将会获得一个<code>2.0.x-dev</code>版本 (<code>.x</code> 是技术原因添加的,来保证被识别为一个分支,一个<code>2.0.x</code>分支也是合法的并且同时将被转换到<code>2.0.x-dev</code>. 如果分支看上去不像一个版本,它将会是<code>dev-{branchname}</code>. <code>master</code> 结果是
					<code>dev-master</code>版本.</p>
				<p>下面是一些版本分支名字的示列:</p>
				<pre><code>1.x
1.0 (equals 1.0.x)
1.1.x
</code></pre>
				<blockquote>
					<p><strong>注意:</strong> 当你安装了一个开发版本，它会从源代码安装.</p>
				</blockquote>
				<h3 id="aliases">别名<a href="#aliases" class="anchor">#</a></h3>
				<p>可以给分支对应版本定别名.举个例子,你可以别名
					<code>dev-master</code>到<code>1.0.x-dev</code>, 这样允许你require 包含<code>1.0.x-dev</code> 在包中.</p>
				<p>看<a href="articles/aliases.md">Aliases</a>了解更多信息.</p>
				<h2 id="lock-file">文件锁<a href="#lock-file" class="anchor">#</a></h2>
				<p>你可以给你的库提交<code>composer.lock</code> 文件如果你想的话.这个可以帮助你的团队永远测试统一恶搞版本依赖.然而这个文件对于其他依赖此文件的项目不起作用.它只作用于主项目.</p>
				<p>如果你不想提交它并且在使用git,添加它到<code>.gitignore</code>.</p>
				<h2 id="light-weight-distribution-packages">轻型发布包<a href="#light-weight-distribution-packages" class="anchor">#</a></h2>
				<p>包含测试和其他无用信息像.travis.yml在分布式不是一个好主意.</p>
				<p><code>.gitattributes</code>文件是一个git指定文件像<code>.gitignore</code>也位于你的库的根目录. 它覆写本地和全局配置(<code>.git/config</code>和<code>~/.gitconfig</code>) 当git表示和跟踪时.</p>
				<p>使用<code>.gitattributes</code>来阻止不想要的文件来增加zip分发包的体积.</p>
				<pre><code>// .gitattributes
Tests/ export-ignore
phpunit.xml.dist export-ignore
Resources export-ignore
.travis.yml export-ignore
</code></pre>
				<p>通过检查手动生成的zip包来测试:</p>
				<pre><code>git archive branchName --format zip -o file.zip
</code></pre>
				<blockquote>
					<p><strong>注意:</strong> 文件将仍会被git跟踪只是不会被包含在发布中. 现在这个将只在GitHub的包安装自dist (i.e. 标记未发布) 中有效.</p>
				</blockquote>
				<h2 id="publishing-to-a-vcs">发布到一个VCS<a href="#publishing-to-a-vcs" class="anchor">#</a></h2>
				<p>一旦你有一个vcs版本库(版本控制系统version control system, e.g. git)包含一个<code>composer.json</code> 文件, 你的库就已经是一个composer-installable （composer-可安装）. 在这个例子里我们将发布<code>acme/hello-world</code>在GitHub上的库位于
					<code>github.com/composer/hello-world</code>.</p>
				<p>现在,为了测试安装<code>acme/hello-world</code>包,我们创建一个新的本地项目.我们把它叫做<code>acme/blog</code>. 这个博客将依赖<code>acme/hello-world</code>, 它同时依赖于<code>monolog/monolog</code>. 我们将完成这个通过创建一个新的<code>blog</code>目录在某个地方, 包含一个<code>composer.json</code>:</p>
				<pre><code>{
	"name": "acme/blog",
	"require": {
		"acme/hello-world": "dev-master"
	}
}
</code></pre>
				<p>name不是必须的在这个例子中,因为我们不想发布blog作为一个库.这里添加它澄清<code>composer.json</code>正在描述的。</p>
				<p>现在我们需要告诉blog应用去找到<code>hello-world</code>依赖.
					我们通过添加一个包版本库指定源到blog's<code>composer.json</code>:</p>
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
				<p>要了解更多细节关于如何包版本库工作和还有哪些可用的其他type见<a href="05-repositories.md">版本库</a>.</p>
				<p>完了.你现在可以安装依赖通过运行composer的<code>install</code> 命令!</p>
				<p><strong>概括:</strong>任何git/svn/hg 版本库包含一个<code>composer.json</code>可以被添加到你的项目通过指定包版本库和在<code>require</code>字段声明依赖关系.</p>
				<h2 id="publishing-to-packagist">发布到packagist<a href="#publishing-to-packagist" class="anchor">#</a></h2>
				<p>好了, 迄今为止你可以发布包了.但是每次指定vcs版本库是笨重的.你不会想强制你的用户那么做的.</p>
				<p>另外一件事你也许注意到的是我们没有指定一个包版本库给<code>monolog/monolog</code>.那它怎么找到并工作的呢?答案是packagist.</p>
				<p><a href="http://packagist.org/">Packagist</a>是主要包版本库给composer,并且是默认启用的.任何发布到
					packagist是可以通过composer自动获取的. 因此monolog
					<a href="http://packagist.org/packages/monolog/monolog">是在packagist里</a>,我们可以依赖它而不需要再指定任何版本库.</p>
				<p>如果我们想和世界分享<code>hello-world</code>,我们也可以发布到packagist.要那么做很简单.</p>
				<p>你简单点击那个大大的"Submit Package"按钮并且注册.然后你提交你的VCS版本库的url, packagist将抓取他通过这个链接.一旦这个完成了,你的包将对所有人可用.</p>
				<p class="prev-next">&larr; <a href="01-basic-usage.md">基本用途</a> |  <a href="03-cli.md">命令行交互</a> &rarr;</p>
				<p class="fork-and-edit">
					找到一个错字?文档有错?只要<a href="http://github.com/composer/composer/edit/master02-libraries.md">fork和edit</a>它!
				</p>
			</div> 
			<footer></footer>
		</div>
	</body>
</html>