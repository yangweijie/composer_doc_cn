<!DOCTYPE html>
<html class="no-js">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">

        <title>Composer</title>
        <meta name="description" content="Dependency Management for PHP">
        <meta name="viewport" content="width=device-width,initial-scale=1">

        <link rel="stylesheet" href="/css/style.css?v=5">

        <script src="/js/modernizr-2.0.6.min.js"></script>
    </head>

    <body>
        <div id="container">
            <header>
				<a href="/">Home</a><a class="" href="/doc/00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                            </header>
            <div id="main" role="main">
				<ul class="toc">
					<li>
						<a href="#json-schema">JSON schema</a> 
                    </li>
					<li>
						<a href="#root-package">Root Package</a> 
                    </li>
					<li>
						<a href="#properties">Properties</a> 
						<ul>
							<li>
								<a href="#name">name</a> 
							</li>
							<li>
								<a href="#description">description</a> 
							</li>
							<li>
								<a href="#version">version</a> 
							</li>
							<li>
								<a href="#type">type</a> 
							</li>
							<li>
								<a href="#keywords">keywords</a> 
							</li>
							<li>
								<a href="#homepage">homepage</a> 
							</li>
							<li>
								<a href="#time">time</a> 
							</li>
							<li>
								<a href="#license">license</a> 
							</li>
							<li>
								<a href="#authors">authors</a> 
							</li>
							<li>
								<a href="#support">support</a> 
							</li>
							<li>
								<a href="#package-links">Package links</a> 
								<ul>
									<li>
										<a href="#require">require</a> 
									</li>
									<li>
										<a href="#require-dev">require-dev </a> (root-only)
									</li>
									<li>
										<a href="#conflict">conflict</a> 
									</li>
									<li>
										<a href="#replace">replace</a> 
									</li>
									<li>
										<a href="#provide">provide</a> 
									</li>

								</ul>
							</li>
							<li>
								<a href="#suggest">suggest</a> 
							</li>
							<li>
								<a href="#autoload">autoload</a> 
							</li>
							<li>
								<a href="#include-path">include-path</a> 
							</li>
							<li>
								<a href="#target-dir">target-dir</a> 
							</li>
							<li>
								<a href="#minimum-stability">minimum-stability </a> (root-only)
							</li>
							<li>
								<a href="#repositories">repositories </a> (root-only)
							</li>
							<li>
								<a href="#config">config </a> (root-only)
							</li>
							<li>
								<a href="#scripts">scripts </a> (root-only)
							</li>
							<li>
								<a href="#extra">extra</a> 
							</li>
							<li>
								<a href="#bin">bin</a> 
							</li>

						</ul>
                    </li>

				</ul>
				<h1 id="composer-json">composer.json<a href="#composer-json" class="anchor">#</a></h1>

				<p>This chapter will explain all of the fields available in <code>composer.json</code>.</p>

				<h2 id="json-schema">JSON schema<a href="#json-schema" class="anchor">#</a></h2>

				<p>We have a <a href="http://json-schema.org">JSON schema</a> that documents the format and
					can also be used to validate your <code>composer.json</code>. In fact, it is used by the
					<code>validate</code> command. You can find it at:
					<a href="https://github.com/composer/composer/blob/master/res/composer-schema.json"><code>res/composer-schema.json</code></a>.</p>

				<h2 id="root-package">Root Package<a href="#root-package" class="anchor">#</a></h2>

				<p>The root package is the package defined by the <code>composer.json</code> at the root of
					your project. It is the main <code>composer.json</code> that defines your project
					requirements.</p>

				<p>Certain fields only apply when in the root package context. One example of
					this is the <code>config</code> field. Only the root package can define configuration.
					The config of dependencies is ignored. This makes the <code>config</code> field
					<code>root-only</code>.</p>

				<p>If you clone one of those dependencies to work on it, then that package is the
					root package. The <code>composer.json</code> is identical, but the context is different.</p>

				<blockquote>
					<p><strong>Note:</strong> A package can be the root package or not, depending on the context.
						For example, if your project depends on the <code>monolog</code> library, your project
						is the root package. However, if you clone <code>monolog</code> from GitHub in order to
						fix a bug in it, then <code>monolog</code> is the root package.</p>
				</blockquote>

				<h2 id="properties">Properties<a href="#properties" class="anchor">#</a></h2>

				<h3 id="name">name<a href="#name" class="anchor">#</a></h3>

				<p>The name of the package. It consists of vendor name and project name,
					separated by <code>/</code>.</p>

				<p>Examples:</p>

				<ul><li>monolog/monolog</li>
					<li>igorw/event-source</li>
				</ul><p>Required for published packages (libraries).</p>

				<h3 id="description">description<a href="#description" class="anchor">#</a></h3>

				<p>A short description of the package. Usually this is just one line long.</p>

				<p>Required for published packages (libraries).</p>

				<h3 id="version">version<a href="#version" class="anchor">#</a></h3>

				<p>The version of the package.</p>

				<p>This must follow the format of <code>X.Y.Z</code> with an optional suffix of <code>-dev</code>,
					<code>-alphaN</code>, <code>-betaN</code> or <code>-RCN</code>.</p>

				<p>Examples:</p>

				<pre><code>1.0.0
1.0.2
1.1.0
0.2.5
1.0.0-dev
1.0.0-alpha3
1.0.0-beta2
1.0.0-RC5
</code></pre>

				<p>Optional if the package repository can infer the version from somewhere, such
					as the VCS tag name in the VCS repository. In that case it is also recommended
					to omit it.</p>

				<blockquote>
					<p><strong>Note:</strong> Packagist uses VCS repositories, so the statement above is very
						much true for Packagist as well. Specifying the version yourself will
						most likely end up creating problems at some point due to human error.</p>
				</blockquote>

				<h3 id="type">type<a href="#type" class="anchor">#</a></h3>

				<p>The type of the package. It defaults to <code>library</code>.</p>

				<p>Package types are used for custom installation logic. If you have a package
					that needs some special logic, you can define a custom type. This could be a
					<code>symfony-bundle</code>, a <code>wordpress-plugin</code> or a <code>typo3-module</code>. These types will
					all be specific to certain projects, and they will need to provide an
					installer capable of installing packages of that type.</p>

				<p>Out of the box, composer supports three types:</p>

				<ul><li><strong>library:</strong> This is the default. It will simply copy the files to <code>vendor</code>.</li>
					<li><strong>metapackage:</strong> An empty package that contains requirements and will trigger
						their installation, but contains no files and will not write anything to the
						filesystem. As such, it does not require a dist or source key to be
						installable.</li>
					<li><strong>composer-installer:</strong> A package of type <code>composer-installer</code> provides an
						installer for other packages that have a custom type. Read more in the
						<a href="articles/custom-installers.md">dedicated article</a>.</li>
				</ul><p>Only use a custom type if you need custom logic during installation. It is
					recommended to omit this field and have it just default to <code>library</code>.</p>

				<h3 id="keywords">keywords<a href="#keywords" class="anchor">#</a></h3>

				<p>An array of keywords that the package is related to. These can be used for
					searching and filtering.</p>

				<p>Examples:</p>

				<pre><code>logging
events
database
redis
templating
</code></pre>

				<p>Optional.</p>

				<h3 id="homepage">homepage<a href="#homepage" class="anchor">#</a></h3>

				<p>An URL to the website of the project.</p>

				<p>Optional.</p>

				<h3 id="time">time<a href="#time" class="anchor">#</a></h3>

				<p>Release date of the version.</p>

				<p>Must be in <code>YYYY-MM-DD</code> or <code>YYYY-MM-DD HH:MM:SS</code> format.</p>

				<p>Optional.</p>

				<h3 id="license">license<a href="#license" class="anchor">#</a></h3>

				<p>The license of the package. This can be either a string or an array of strings.</p>

				<p>The recommended notation for the most common licenses is (alphabetical):</p>

				<pre><code>Apache-2.0
BSD-2-Clause
BSD-3-Clause
BSD-4-Clause
GPL-2.0
GPL-2.0+
GPL-3.0
GPL-3.0+
LGPL-2.1
LGPL-2.1+
LGPL-3.0
LGPL-3.0+
MIT
</code></pre>

				<p>Optional, but it is highly recommended to supply this. More identifiers are
					listed at the <a href="http://www.spdx.org/licenses/">SPDX Open Source License Registry</a>.</p>

				<p>An Example:</p>

				<pre><code>{
    "license": "MIT"
}
</code></pre>

				<p>For a package, when there is a choice between licenses ("disjunctive license"),
					multiple can be specified as array.</p>

				<p>An Example for disjunctive licenses:</p>

				<pre><code>{
    "license": [
       "LGPL-2.1",
       "GPL-3.0+"
    ]
}
</code></pre>

				<p>Alternatively they can be separated with "or" and enclosed in parenthesis;</p>

				<pre><code>{
    "license": "(LGPL-2.1 or GPL-3.0+)"
}
</code></pre>

				<p>Similarly when multiple licenses need to be applied ("conjunctive license"),
					they should be separated with "and" and enclosed in parenthesis.</p>

				<h3 id="authors">authors<a href="#authors" class="anchor">#</a></h3>

				<p>The authors of the package. This is an array of objects.</p>

				<p>Each author object can have following properties:</p>

				<ul><li><strong>name:</strong> The author's name. Usually his real name.</li>
					<li><strong>email:</strong> The author's email address.</li>
					<li><strong>homepage:</strong> An URL to the author's website.</li>
					<li><strong>role:</strong> The authors' role in the project (e.g. developer or translator)</li>
				</ul><p>An example:</p>

				<pre><code>{
    "authors": [
        {
            "name": "Nils Adermann",
            "email": "naderman@naderman.de",
            "homepage": "http://www.naderman.de",
            "role": "Developer"
        },
        {
            "name": "Jordi Boggiano",
            "email": "j.boggiano@seld.be",
            "homepage": "http://seld.be",
            "role": "Developer"
        }
    ]
}
</code></pre>

				<p>Optional, but highly recommended.</p>

				<h3 id="support">support<a href="#support" class="anchor">#</a></h3>

				<p>Various information to get support about the project.</p>

				<p>Support information includes the following:</p>

				<ul><li><strong>email:</strong> Email address for support.</li>
					<li><strong>issues:</strong> URL to the Issue Tracker.</li>
					<li><strong>forum:</strong> URL to the Forum.</li>
					<li><strong>wiki:</strong> URL to the Wiki.</li>
					<li><strong>irc:</strong> IRC channel for support, as irc://server/channel.</li>
					<li><strong>source:</strong> URL to browse or download the sources.</li>
				</ul><p>An example:</p>

				<pre><code>{
    "support": {
        "email": "support@example.org",
        "irc": "irc://irc.freenode.org/composer"
    }
}
</code></pre>

				<p>Optional.</p>

				<h3 id="package-links">Package links<a href="#package-links" class="anchor">#</a></h3>

				<p>All of the following take an object which maps package names to
					<a href="01-basic-usage.md#package-versions">version constraints</a>.</p>

				<p>Example:</p>

				<pre><code>{
    "require": {
        "monolog/monolog": "1.0.*"
    }
}
</code></pre>

				<p>All links are optional fields.</p>

				<p><code>require</code> and <code>require-dev</code> additionally support stability flags (root-only).
					These allow you to further restrict or expand the stability of a package beyond
					the scope of the <a href="#minimum-stability">minimum-stability</a> setting. You can apply
					them to a constraint, or just apply them to an empty constraint if you want to
					allow unstable packages of a dependency's dependency for example.</p>

				<p>Example:</p>

				<pre><code>{
    "require": {
        "monolog/monolog": "1.0.*@beta",
        "acme/foo": "@dev"
    }
}
</code></pre>

				<p><code>require</code> and <code>require-dev</code> additionally support explicit references (i.e.
					commit) for dev versions to make sure they are blocked to a given state, even
					when you run update. These only work if you explicitly require a dev version
					and append the reference with <code>#&lt;ref&gt;</code>. Note that while this is convenient at
					times, it should not really be how you use packages in the long term. You
					should always try to switch to tagged releases as soon as you can, especially
					if the project you work on will not be touched for a while.</p>

				<p>Example:</p>

				<pre><code>{
    "require": {
        "monolog/monolog": "dev-master#2eb0c0978d290a1c45346a1955188929cb4e5db7",
        "acme/foo": "1.0.x-dev#abc123"
    }
}
</code></pre>

				<h4 id="require">require<a href="#require" class="anchor">#</a></h4>

				<p>Lists packages required by this package. The package will not be installed
					unless those requirements can be met.</p>

				<h4 id="require-dev">require-dev <span>(root-only)</span><a href="#require-dev" class="anchor">#</a></h4>

				<p>Lists packages required for developing this package, or running
					tests, etc. The dev requirements of the root package only will be installed
					if <code>install</code> or <code>update</code> is ran with <code>--dev</code>.</p>

				<p>Packages listed here and their dependencies can not overrule the resolution
					found with the packages listed in require. This is even true if a different
					version of a package would be installable and solve the conflict. The reason
					is that <code>install --dev</code> produces the exact same state as just <code>install</code>, apart
					from the additional dev packages.</p>

				<p>If you run into such a conflict, you can specify the conflicting package in
					the require section and require the right version number to resolve the
					conflict.</p>

				<h4 id="conflict">conflict<a href="#conflict" class="anchor">#</a></h4>

				<p>Lists packages that conflict with this version of this package. They
					will not be allowed to be installed together with your package.</p>

				<h4 id="replace">replace<a href="#replace" class="anchor">#</a></h4>

				<p>Lists packages that are replaced by this package. This allows you to fork a
					package, publish it under a different name with its own version numbers, while
					packages requiring the original package continue to work with your fork because
					it replaces the original package.</p>

				<p>This is also useful for packages that contain sub-packages, for example the main
					symfony/symfony package contains all the Symfony Components which are also
					available as individual packages. If you require the main package it will
					automatically fulfill any requirement of one of the individual components,
					since it replaces them.</p>

				<p>Caution is advised when using replace for the sub-package purpose explained
					above. You should then typically only replace using <code>self.version</code> as a version
					constraint, to make sure the main package only replaces the sub-packages of
					that exact version, and not any other version, which would be incorrect.</p>

				<h4 id="provide">provide<a href="#provide" class="anchor">#</a></h4>

				<p>List of other packages that are provided by this package. This is mostly
					useful for common interfaces. A package could depend on some virtual
					<code>logger</code> package, any library that implements this logger interface would
					simply list it in <code>provide</code>.</p>

				<h3 id="suggest">suggest<a href="#suggest" class="anchor">#</a></h3>

				<p>Suggested packages that can enhance or work well with this package. These are
					just informational and are displayed after the package is installed, to give
					your users a hint that they could add more packages, even though they are not
					strictly required.</p>

				<p>The format is like package links above, except that the values are free text
					and not version constraints.</p>

				<p>Example:</p>

				<pre><code>{
    "suggest": {
        "monolog/monolog": "Allows more advanced logging of the application flow"
    }
}
</code></pre>

				<h3 id="autoload">autoload<a href="#autoload" class="anchor">#</a></h3>

				<p>Autoload mapping for a PHP autoloader.</p>

				<p>Currently <a href="https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md">PSR-0</a>
					autoloading, classmap generation and files are supported. PSR-0 is the recommended way though
					since it offers greater flexibility (no need to regenerate the autoloader when you add
					classes).</p>

				<p>Under the <code>psr-0</code> key you define a mapping from namespaces to paths, relative to the
					package root. Note that this also supports the PEAR-style non-namespaced convention.</p>

				<p>The PSR-0 references are all combined, during install/update, into a single key =&gt; value
					array which may be found in the generated file <code>vendor/composer/autoload_namespaces.php</code>.</p>

				<p>Example:</p>

				<pre><code>{
    "autoload": {
        "psr-0": {
            "Monolog": "src/",
            "Vendor\\Namespace": "src/",
            "Pear_Style": "src/"
        }
    }
}
</code></pre>

				<p>If you need to search for a same prefix in multiple directories,
					you can specify them as an array as such:</p>

				<pre><code>{
    "autoload": {
        "psr-0": { "Monolog": ["src/", "lib/"] }
    }
}
</code></pre>

				<p>The PSR-0 style is not limited to namespace declarations only but may be
					specified right down to the class level. This can be useful for libraries with
					only one class in the global namespace. If the php source file is also located
					in the root of the package, for example, it may be declared like this:</p>

				<pre><code>{
    "autoload": {
        "psr-0": { "UniqueGlobalClass": "" }
    }
}
</code></pre>

				<p>If you want to have a fallback directory where any namespace can be, you can
					use an empty prefix like:</p>

				<pre><code>{
    "autoload": {
        "psr-0": { "": "src/" }
    }
}
</code></pre>

				<p>The <code>classmap</code> references are all combined, during install/update, into a single
					key =&gt; value array which may be found in the generated file
					<code>vendor/composer/autoload_classmap.php</code>.</p>

				<p>You can use the classmap generation support to define autoloading for all libraries
					that do not follow PSR-0. To configure this you specify all directories or files
					to search for classes.</p>

				<p>Example:</p>

				<pre><code>{
    "autoload": {
        "classmap": ["src/", "lib/", "Something.php"]
    }
}
</code></pre>

				<p>If you want to require certain files explicitly on every request then you can use
					the 'files' autoloading mechanism. This is useful if your package includes PHP functions
					that cannot be autoloaded by PHP.</p>

				<p>Example:</p>

				<pre><code>{
    "autoload": {
        "files": ["src/MyLibrary/functions.php"]
    }
}
</code></pre>

				<h3 id="include-path">include-path<a href="#include-path" class="anchor">#</a></h3>

				<blockquote>
					<p><strong>DEPRECATED</strong>: This is only present to support legacy projects, and all new code
						should preferably use autoloading. As such it is a deprecated practice, but the
						feature itself will not likely disappear from Composer.</p>
				</blockquote>

				<p>A list of paths which should get appended to PHP's <code>include_path</code>.</p>

				<p>Example:</p>

				<pre><code>{
    "include-path": ["lib/"]
}
</code></pre>

				<p>Optional.</p>

				<h3 id="target-dir">target-dir<a href="#target-dir" class="anchor">#</a></h3>

				<p>Defines the installation target.</p>

				<p>In case the package root is below the namespace declaration you cannot
					autoload properly. <code>target-dir</code> solves this problem.</p>

				<p>An example is Symfony. There are individual packages for the components. The
					Yaml component is under <code>Symfony\Component\Yaml</code>. The package root is that
					<code>Yaml</code> directory. To make autoloading possible, we need to make sure that it
					is not installed into <code>vendor/symfony/yaml</code>, but instead into
					<code>vendor/symfony/yaml/Symfony/Component/Yaml</code>, so that the autoloader can load
					it from <code>vendor/symfony/yaml</code>.</p>

				<p>To do that, <code>autoload</code> and <code>target-dir</code> are defined as follows:</p>

				<pre><code>{
    "autoload": {
        "psr-0": { "Symfony\\Component\\Yaml": "" }
    },
    "target-dir": "Symfony/Component/Yaml"
}
</code></pre>

				<p>Optional.</p>

				<h3 id="minimum-stability">minimum-stability <span>(root-only)</span><a href="#minimum-stability" class="anchor">#</a></h3>

				<p>This defines the default behavior for filtering packages by stability. This
					defaults to <code>stable</code>, so if you rely on a <code>dev</code> package, you should specify
					it in your file to avoid surprises.</p>

				<p>All versions of each package are checked for stability, and those that are less
					stable than the <code>minimum-stability</code> setting will be ignored when resolving
					your project dependencies. Specific changes to the stability requirements of
					a given package can be done in <code>require</code> or <code>require-dev</code> (see
					<a href="#package-links">package links</a>).</p>

				<p>Available options (in order of stability) are <code>dev</code>, <code>alpha</code>, <code>beta</code>, <code>RC</code>,
					and <code>stable</code>.</p>

				<h3 id="repositories">repositories <span>(root-only)</span><a href="#repositories" class="anchor">#</a></h3>

				<p>Custom package repositories to use.</p>

				<p>By default composer just uses the packagist repository. By specifying
					repositories you can get packages from elsewhere.</p>

				<p>Repositories are not resolved recursively. You can only add them to your main
					<code>composer.json</code>. Repository declarations of dependencies' <code>composer.json</code>s are
					ignored.</p>

				<p>The following repository types are supported:</p>

				<ul><li><strong>composer:</strong> A composer repository is simply a <code>packages.json</code> file served
						via the network (HTTP, FTP, SSH), that contains a list of <code>composer.json</code>
						objects with additional <code>dist</code> and/or <code>source</code> information. The <code>packages.json</code>
						file is loaded using a PHP stream. You can set extra options on that stream
						using the <code>options</code> parameter.</li>
					<li><strong>vcs:</strong> The version control system repository can fetch packages from git,
						svn and hg repositories.</li>
					<li><strong>pear:</strong> With this you can import any pear repository into your composer
						project.</li>
					<li><strong>package:</strong> If you depend on a project that does not have any support for
						composer whatsoever you can define the package inline using a <code>package</code>
						repository. You basically just inline the <code>composer.json</code> object.</li>
				</ul><p>For more information on any of these, see <a href="05-repositories.md">Repositories</a>.</p>

				<p>Example:</p>

				<pre><code>{
    "repositories": [
        {
            "type": "composer",
            "url": "http://packages.example.com"
        },
        {
            "type": "composer",
            "url": "https://packages.example.com",
            "options": {
                "ssl": {
                    "verify_peer": "true"
                }
            }
        },
        {
            "type": "vcs",
            "url": "https://github.com/Seldaek/monolog"
        },
        {
            "type": "pear",
            "url": "http://pear2.php.net"
        },
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
                }
            }
        }
    ]
}
</code></pre>

				<blockquote>
					<p><strong>Note:</strong> Order is significant here. When looking for a package, Composer
						will look from the first to the last repository, and pick the first match.
						By default Packagist is added last which means that custom repositories can
						override packages from it.</p>
				</blockquote>

				<h3 id="config">config <span>(root-only)</span><a href="#config" class="anchor">#</a></h3>

				<p>A set of configuration options. It is only used for projects.</p>

				<p>The following options are supported:</p>

				<ul><li><strong>vendor-dir:</strong> Defaults to <code>vendor</code>. You can install dependencies into a
						different directory if you want to.</li>
					<li><strong>bin-dir:</strong> Defaults to <code>vendor/bin</code>. If a project includes binaries, they
						will be symlinked into this directory.</li>
					<li><strong>process-timeout:</strong> Defaults to <code>300</code>. The duration processes like git clones
						can run before Composer assumes they died out. You may need to make this
						higher if you have a slow connection or huge vendors.</li>
					<li><strong>github-protocols:</strong> Defaults to <code>["git", "https", "http"]</code>. A list of
						protocols to use for github.com clones, in priority order. Use this if you are
						behind a proxy or have somehow bad performances with the git protocol.</li>
					<li><strong>notify-on-install:</strong> Defaults to <code>true</code>. Composer allows repositories to
						define a notification URL, so that they get notified whenever a package from
						that repository is installed. This option allows you to disable that behaviour.</li>
				</ul><p>Example:</p>

				<pre><code>{
    "config": {
        "bin-dir": "bin"
    }
}
</code></pre>

				<h3 id="scripts">scripts <span>(root-only)</span><a href="#scripts" class="anchor">#</a></h3>

				<p>Composer allows you to hook into various parts of the installation process
					through the use of scripts.</p>

				<p>See <a href="articles/scripts.md">Scripts</a> for events details and examples.</p>

				<h3 id="extra">extra<a href="#extra" class="anchor">#</a></h3>

				<p>Arbitrary extra data for consumption by <code>scripts</code>.</p>

				<p>This can be virtually anything. To access it from within a script event
					handler, you can do:</p>

				<pre><code>$extra = $event-&gt;getComposer()-&gt;getPackage()-&gt;getExtra();
</code></pre>

				<p>Optional.</p>

				<h3 id="bin">bin<a href="#bin" class="anchor">#</a></h3>

				<p>A set of files that should be treated as binaries and symlinked into the <code>bin-dir</code>
					(from config).</p>

				<p>See <a href="articles/vendor-bins.md">Vendor Bins</a> for more details.</p>

				<p>Optional.</p>

				<p class="prev-next">&larr; <a href="03-cli.md">Command-line interface</a>  |  <a href="05-repositories.md">Repositories</a> &rarr;</p>

				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/04-schema.md">fork and edit</a> it!
				</p>
            </div>
            <footer>
			</footer>
        </div>


        <script>
			var _gaq = [['_setAccount', 'UA-26723099-2'], ['_trackPageview']];
			(function(d, t) {
				var g = d.createElement(t), s = d.getElementsByTagName(t)[0];
				g.async = 1;
				g.src = ('https:' == location.protocol ? '//ssl' : '//www') + '.google-analytics.com/ga.js';
				s.parentNode.insertBefore(g, s)
			}(document, 'script'));
        </script>
    </body>
</html>