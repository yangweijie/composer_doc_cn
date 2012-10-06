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
				<a href="/">Home</a><a href="/doc/00-intro.md">Getting Started</a><a href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                            
			</header>
            <div id="main" role="main">
				<ul class="toc">
					<li>
						<a href="#concepts">Concepts</a> 
						<ul>
							<li>
								<a href="#package">Package</a> 
							</li>
							<li>
								<a href="#repository">Repository</a> 
							</li>
						</ul>
                    </li>
					<li>
						<a href="#types">Types</a> 
						<ul>
							<li>
								<a href="#composer">Composer</a> 
								<ul>
									<li>
										<a href="#packages">packages</a> 
									</li>
									<li>
										<a href="#notify">notify</a> 
									</li>
									<li>
										<a href="#includes">includes</a> 
									</li>
									<li>
										<a href="#stream-options">stream options</a> 
									</li>
								</ul>
							</li>
							<li>
								<a href="#vcs">VCS</a> 
							</li>
							<li>
								<a href="#pear">PEAR</a> 
								<ul>
									<li>
										<a href="#custom-channel-alias">Custom channel alias</a> 
									</li>

								</ul>
							</li>
							<li>
								<a href="#package-2">Package</a> 
							</li>
						</ul>
                    </li>
					<li>
						<a href="#hosting-your-own">Hosting your own</a> 
						<ul>
							<li>
								<a href="#packagist">Packagist</a> 
							</li>
							<li>
								<a href="#satis">Satis</a> 
							</li>
						</ul>
                    </li>
					<li>
						<a href="#disabling-packagist">Disabling Packagist</a> 
                    </li>
				</ul>
				<h1 id="repositories">Repositories<a href="#repositories" class="anchor">#</a></h1>
				<p>This chapter will explain the concept of packages and repositories, what kinds
					of repositories are available, and how they work.</p>
				<h2 id="concepts">Concepts<a href="#concepts" class="anchor">#</a></h2>
				<p>Before we look at the different types of repositories that exist, we need to
					understand some of the basic concepts that composer is built on.</p>
				<h3 id="package">Package<a href="#package" class="anchor">#</a></h3>
				<p>Composer is a dependency manager. It installs packages locally. A package is
					essentially just a directory containing something. In this case it is PHP
					code, but in theory it could be anything. And it contains a package
					description which has a name and a version. The name and the version are used
					to identify the package.</p>
				<p>In fact, internally composer sees every version as a separate package. While
					this distinction does not matter when you are using composer, it's quite
					important when you want to change it.</p>
				<p>In addition to the name and the version, there is useful metadata. The information
					most relevant for installation is the source definition, which describes where
					to get the package contents. The package data points to the contents of the
					package. And there are two options here: dist and source.</p>
				<p><strong>Dist:</strong> The dist is a packaged version of the package data. Usually a
					released version, usually a stable release.</p>
				<p><strong>Source:</strong> The source is used for development. This will usually originate
					from a source code repository, such as git. You can fetch this when you want
					to modify the downloaded package.</p>
				<p>Packages can supply either of these, or even both. Depending on certain
					factors, such as user-supplied options and stability of the package, one will
					be preferred.</p>
				<h3 id="repository">Repository<a href="#repository" class="anchor">#</a></h3>
				<p>A repository is a package source. It's a list of packages/versions. Composer
					will look in all your repositories to find the packages your project requires.</p>
				<p>By default only the Packagist repository is registered in Composer. You can
					add more repositories to your project by declaring them in <code>composer.json</code>.</p>
				<p>Repositories are only available to the root package and the repositories
					defined in your dependencies will not be loaded. Read the
					<a href="faqs/why-can't-composer-load-repositories-recursively.md">FAQ entry</a> if you
					want to learn why.</p>
				<h2 id="types">Types<a href="#types" class="anchor">#</a></h2>
				<h3 id="composer">Composer<a href="#composer" class="anchor">#</a></h3>
				<p>The main repository type is the <code>composer</code> repository. It uses a single
					<code>packages.json</code> file that contains all of the package metadata.</p>
				<p>This is also the repository type that packagist uses. To reference a
					<code>composer</code> repository, just supply the path before the <code>packages.json</code> file.
					In case of packagist, that file is located at <code>/packages.json</code>, so the URL of
					the repository would be <code>packagist.org</code>. For <code>example.org/packages.json</code> the
					repository URL would be <code>example.org</code>.</p>
				<h4 id="packages">packages<a href="#packages" class="anchor">#</a></h4>
				<p>The only required field is <code>packages</code>. The JSON structure is as follows:</p>
				<pre><code>{
    "packages": {
        "vendor/package-name": {
            "dev-master": { @composer.json },
            "1.0.x-dev": { @composer.json },
            "0.0.1": { @composer.json },
            "1.0.0": { @composer.json }
        }
    }
}
</code></pre>
				<p>The <code>@composer.json</code> marker would be the contents of the <code>composer.json</code> from
					that package version including as a minimum:</p>
				<ul><li>name</li>
					<li>version</li>
					<li>dist or source</li>
				</ul><p>Here is a minimal package definition:</p>
				<pre><code>{
    "name": "smarty/smarty",
    "version": "3.1.7",
    "dist": {
        "url": "http://www.smarty.net/files/Smarty-3.1.7.zip",
        "type": "zip"
    }
}
</code></pre>
				<p>It may include any of the other fields specified in the <a href="04-schema.md">schema</a>.</p>
				<h4 id="notify">notify<a href="#notify" class="anchor">#</a></h4>
				<p>The <code>notify</code> field allows you to specify an URL template for a URL that will
					be called every time a user installs a package. The URL can be either an
					absolute path (that will use the same domain as the repository) or a fully
					qualified URL.</p>
				<p>An example value:</p>
				<pre><code>{
    "notify": "/downloads/%package%"
}
</code></pre>
				<p>For <code>example.org/packages.json</code> containing a <code>monolog/monolog</code> package, this
					would send a <code>POST</code> request to <code>example.org/downloads/monolog/monolog</code> with
					following parameters:</p>
				<ul><li><strong>version:</strong> The version of the package.</li>
					<li><strong>version_normalized:</strong> The normalized internal representation of the
						version.</li>
				</ul><p>This field is optional.</p>
				<h4 id="includes">includes<a href="#includes" class="anchor">#</a></h4>
				<p>For large repositories it is possible to split the <code>packages.json</code> into
					multiple files. The <code>includes</code> field allows you to reference these additional
					files.</p>
				<p>An example:</p>
				<pre><code>{
    "includes": {
        "packages-2011.json": {
            "sha1": "525a85fb37edd1ad71040d429928c2c0edec9d17"
        },
        "packages-2012-01.json": {
            "sha1": "897cde726f8a3918faf27c803b336da223d400dd"
        },
        "packages-2012-02.json": {
            "sha1": "26f911ad717da26bbcac3f8f435280d13917efa5"
        }
    }
}
</code></pre>
				<p>The SHA-1 sum of the file allows it to be cached and only re-requested if the
					hash changed.</p>
				<p>This field is optional. You probably don't need it for your own custom
					repository.</p>
				<h4 id="stream-options">stream options<a href="#stream-options" class="anchor">#</a></h4>
				<p>The <code>packages.json</code> file is loaded using a PHP stream. You can set extra options
					on that stream using the <code>options</code> parameter. You can set any valid PHP stream
					context option. See <a href="http://nl3.php.net/manual/en/context.php">Context options and parameters</a>
					for more information.</p>
				<h3 id="vcs">VCS<a href="#vcs" class="anchor">#</a></h3>
				<p>VCS stands for version control system. This includes versioning systems like
					git, svn or hg. Composer has a repository type for installing packages from
					these systems.</p>
				<p>There are a few use cases for this. The most common one is maintaining your
					own fork of a third party library. If you are using a certain library for your
					project and you decide to change something in the library, you will want your
					project to use the patched version. If the library is on GitHub (this is the
					case most of the time), you can simply fork it there and push your changes to
					your fork. After that you update the project's <code>composer.json</code>. All you have
					to do is add your fork as a repository and update the version constraint to
					point to your custom branch. For version constraint naming conventions see
					<a href="02-libraries.md">Libraries</a> for more information.</p>
				<p>Example assuming you patched monolog to fix a bug in the <code>bugfix</code> branch:</p>
				<pre><code>{
    "repositories": [
        {
            "type": "vcs",
            "url": "http://github.com/igorw/monolog"
        }
    ],
    "require": {
        "monolog/monolog": "dev-bugfix"
    }
}
</code></pre>
				<p>When you run <code>php composer.phar update</code>, you should get your modified version
					of <code>monolog/monolog</code> instead of the one from packagist.</p>
				<p>Git is not the only version control system supported by the VCS repository.
					The following are supported:</p>
				<ul><li><strong>Git:</strong> <a href="http://git-scm.com">git-scm.com</a></li>
					<li><strong>Subversion:</strong> <a href="http://subversion.apache.org">subversion.apache.org</a></li>
					<li><strong>Mercurial:</strong> <a href="http://mercurial.selenic.com">mercurial.selenic.com</a></li>
				</ul><p>To get packages from these systems you need to have their respective clients
					installed. That can be inconvenient. And for this reason there is special
					support for GitHub and BitBucket that use the APIs provided by these sites, to
					fetch the packages without having to install the version control system. The
					VCS repository provides <code>dist</code>s for them that fetch the packages as zips.</p>
				<ul><li><strong>GitHub:</strong> <a href="https://github.com">github.com</a> (Git)</li>
					<li><strong>BitBucket:</strong> <a href="https://bitbucket.org">bitbucket.org</a> (Git and Mercurial)</li>
				</ul><p>The VCS driver to be used is detected automatically based on the URL. However,
					should you need to specify one for whatever reason, you can use <code>git</code>, <code>svn</code> or
					<code>hg</code> as the repository type instead of <code>vcs</code>.</p>
				<h3 id="pear">PEAR<a href="#pear" class="anchor">#</a></h3>
				<p>It is possible to install packages from any PEAR channel by using the <code>pear</code>
					repository. Composer will prefix all package names with <code>pear-{channelName}/</code> to
					avoid conflicts. All packages are also aliased with prefix <code>pear-{channelAlias}/</code></p>
				<p>Example using <code>pear2.php.net</code>:</p>
				<pre><code>{
    "repositories": [
        {
            "type": "pear",
            "url": "http://pear2.php.net"
        }
    ],
    "require": {
        "pear-pear2.php.net/PEAR2_Text_Markdown": "*",
        "pear-pear2/PEAR2_HTTP_Request": "*"
    }
}
</code></pre>
				<p>In this case the short name of the channel is <code>pear2</code>, so the
					<code>PEAR2_HTTP_Request</code> package name becomes <code>pear-pear2/PEAR2_HTTP_Request</code>.</p>
				<blockquote>
					<p><strong>Note:</strong> The <code>pear</code> repository requires doing quite a few requests per
						package, so this may considerably slow down the installation process.</p>
				</blockquote>
				<h4 id="custom-channel-alias">Custom channel alias<a href="#custom-channel-alias" class="anchor">#</a></h4>
				<p>It is possible to alias all pear channel packages with custom name.</p>
				<p>Example:</p>
				<p>You own private pear repository and going to use composer abilities to bring
					dependencies from vcs or transit to composer repository scheme. Your
					repository list of packages:</p>
				<ul><li>BasePackage, requires nothing</li>
					<li>IntermediatePackage, depends on BasePackage</li>
					<li>TopLevelPackage1 and TopLevelPackage2 both depend on IntermediatePackage.</li>
				</ul><p>For composer it looks like:</p>
				<ul><li>"pear-pear.foobar.repo/IntermediatePackage" depends on "pear-pear.foobar.repo/BasePackage",</li>
					<li>"pear-pear.foobar.repo/TopLevelPackage1" depends on "pear-pear.foobar.repo/IntermediatePackage",</li>
					<li>"pear-pear.foobar.repo/TopLevelPackage2" depends on "pear-pear.foobar.repo/IntermediatePackage"</li>
				</ul><p>When you update one of your packages to composer naming scheme or made it
					available through vcs, your older dependencies would not see new version,
					cause it would be named like "foobar/IntermediatePackage". Specifying 'vendor-
					alias' for pear repository, you will get all its packages aliased with
					composer-like names. Following example would take BasePackage,
					TopLevelPackage1 and TopLevelPackage2 packages from pear repository and
					IntermediatePackage from github repository:</p>
				<pre><code>{
    "repositories": [
        {
            "type": "git",
            "url": "https://github.com/foobar/intermediate.git"
        },
        {
            "type": "pear",
            "url": "http://pear.foobar.repo",
            "vendor-alias": "foobar"
        }
    ],
    "require": {
        "foobar/TopLevelPackage1": "*",
        "foobar/TopLevelPackage2": "*"
    }
}
</code></pre>
				<h3 id="package-2">Package<a href="#package-2" class="anchor">#</a></h3>
				<p>If you want to use a project that does not support composer through any of the
					means above, you still can define the package yourself by using a <code>package</code>
					repository.</p>
				<p>Basically, you define the same information that is included in the <code>composer</code>
					repository's <code>packages.json</code>, but only for a single package. Again, the
					minimum required fields are <code>name</code>, <code>version</code>, and either of <code>dist</code> or
					<code>source</code>.</p>
				<p>Here is an example for the smarty template engine:</p>
				<pre><code>{
    "repositories": [
        {
            "type": "package",
            "package": {
                "name": "smarty/smarty",
                "version": "3.1.7",
                "dist": {
                    "url": "http://www.smarty.net/files/Smarty-3.1.7.zip",
                    "type": "zip"
                },
                "source": {
                    "url": "http://smarty-php.googlecode.com/svn/",
                    "type": "svn",
                    "reference": "tags/Smarty_3_1_7/distribution/"
                },
                "autoload": {
                    "classmap": ["libs/"]
                }
            }
        }
    ],
    "require": {
        "smarty/smarty": "3.1.*"
    }
}
</code></pre>
				<p>Typically you would leave the source part off, as you don't really need it.</p>
				<h2 id="hosting-your-own">Hosting your own<a href="#hosting-your-own" class="anchor">#</a></h2>
				<p>While you will probably want to put your packages on packagist most of the time,
					there are some use cases for hosting your own repository.</p>
				<ul><li><p><strong>Private company packages:</strong> If you are part of a company that uses composer
							for their packages internally, you might want to keep those packages private.</p></li>
					<li><p><strong>Separate ecosystem:</strong> If you have a project which has its own ecosystem,
							and the packages aren't really reusable by the greater PHP community, you
							might want to keep them separate to packagist. An example of this would be
							wordpress plugins.</p></li>
				</ul><p>When hosting your own package repository it is recommended to use a <code>composer</code>
					one. This is type that is native to composer and yields the best performance.</p>
				<p>There are a few tools that can help you create a <code>composer</code> repository.</p>
				<h3 id="packagist">Packagist<a href="#packagist" class="anchor">#</a></h3>
				<p>The underlying application used by packagist is open source. This means that you
					can just install your own copy of packagist, re-brand, and use it. It's really
					quite straight-forward to do. However due to its size and complexity, for most
					small and medium sized companies willing to track a few packages will be better
					off using Satis.</p>
				<p>Packagist is a Symfony2 application, and it is <a href="https://github.com/composer/packagist">available on
						GitHub</a>. It uses composer internally and
					acts as a proxy between VCS repositories and the composer users. It holds a list
					of all VCS packages, periodically re-crawls them, and exposes them as a composer
					repository.</p>
				<p>To set your own copy, simply follow the instructions from the <a href="https://github.com/composer/packagist">packagist
						github repository</a>.</p>
				<h3 id="satis">Satis<a href="#satis" class="anchor">#</a></h3>
				<p>Satis is a static <code>composer</code> repository generator. It is a bit like an ultra-
					lightweight, static file-based version of packagist.</p>
				<p>You give it a <code>composer.json</code> containing repositories, typically VCS and
					package repository definitions. It will fetch all the packages that are
					<code>require</code>d and dump a <code>packages.json</code> that is your <code>composer</code> repository.</p>
				<p>Check <a href="https://github.com/composer/satis">the satis GitHub repository</a> and
					the <a href="articles/handling-private-packages-with-satis.md">Satis article</a> for more
					information.</p>
				<h2 id="disabling-packagist">Disabling Packagist<a href="#disabling-packagist" class="anchor">#</a></h2>
				<p>You can disable the default Packagist repository by adding this to your
					<code>composer.json</code>:</p>
				<pre><code>{
    "repositories": [
        {
            "packagist": false
        }
    ]
}
</code></pre>
				<p class="prev-next">&larr; <a href="04-schema.md">Schema</a>  |  <a href="06-community.md">Community</a> &rarr;</p>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/05-repositories.md">fork and edit</a> it!
				</p>
            </div>
            <footer></footer>
        </div>
    </body>
</html>