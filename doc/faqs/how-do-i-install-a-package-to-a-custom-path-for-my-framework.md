<!DOCTYPE html>
<html class="no-js" lang="zh">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
        <title>Composer</title>
        <meta name="description" content="Dependency Management for PHP">
        <meta name="viewport" content="width=device-width,initial-scale=1">
        <link rel="stylesheet" href="../css/style.css">
        <script src="../js/modernizr-2.0.6.min.js"></script>
    </head>
    <body>
        <div id="container">
            <header>
				<a href="/">Home</a><a class="" href="../doc/00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                            
			</header>
            <div id="main" role="main">
				<ul class="toc"></ul>
				<h1 id="how-do-i-install-a-package-to-a-custom-path-for-my-framework-">How do I install a package to a custom path for my framework?<a href="#how-do-i-install-a-package-to-a-custom-path-for-my-framework-" class="anchor">#</a></h1>
				<p>Each framework may have one or many different required package installation
					paths. Composer can be configured to install packages to a folder other than
					the default <code>vendor</code> folder by using
					<a href="https://github.com/composer/installers">composer/installers</a>.</p>
				<p>If you are a <strong>package author</strong> and want your package installed to a custom
					directory, simply require <code>composer/installers</code> and set the appropriate <code>type</code>.
					This is common if your package is intended for a specific framework such as
					CakePHP, Drupal or WordPress. Here is an example composer.json file for a
					WordPress theme:</p>

				<pre><code>{
    "name": "you/themename",
    "type": "wordpress-theme",
    "require": {
        "composer/installers": "*"
    }
}
</code></pre>
				<p>Now when your theme is installed with Composer it will be placed into
					<code>wp-content/themes/themename/</code> folder. Check the
					<a href="https://github.com/composer/installers#current-supported-types">current supported types</a>
					for your package.</p>
				<p>As a <strong>package consumer</strong> you can set or override the install path for a package
					that requires composer/installers by configuring the <code>installer-paths</code> extra. A
					useful example would be for a Drupal multisite setup where the package should be
					installed into your sites subdirectory. Here we are overriding the install path
					for a module that uses composer/installers:</p>
				<pre><code>{
    "extra": {
        "installer-paths": {
            "sites/example.com/modules/{$name}": ["vendor/package"]
        }
    }
}
</code></pre>
				<p>Now the package would be installed to your folder location, rather than the default
					composer/installers determined location.</p>
				<blockquote>
					<p><strong>Note:</strong> You cannot use this to change the path of any package. This is only
						applicable to packages that require <code>composer/installers</code> and use a custom type
						that it handles.</p>
				</blockquote>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/faqs/how-do-i-install-a-package-to-a-custom-path-for-my-framework.md">fork and edit</a> it!
				</p>
            </div>
            <footer>
			</footer>
        </div>
    </body>
</html>