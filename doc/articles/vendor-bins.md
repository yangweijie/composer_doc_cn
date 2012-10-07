<!DOCTYPE html>
<html class="no-js" lang="en">
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
				<a href="/">Home</a><a class="" href="/doc/00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                            
			</header>
            <div id="main" role="main">
				<ul class="toc">
					<li>
						<a href="#what-is-a-bin-">What is a bin?</a> 
                    </li>
					<li>
						<a href="#how-is-it-defined-">How is it defined?</a> 
                    </li>
					<li>
						<a href="#what-does-defining-a-bin-in-composer-json-do-">What does defining a bin in composer.json do?</a> 
                    </li>
					<li>
						<a href="#what-happens-when-composer-is-run-on-a-composer-json-that-defines-bins-">What happens when Composer is run on a composer.json that defines bins?</a> 
                    </li>
					<li>
						<a href="#what-happens-when-composer-is-run-on-a-composer-json-that-has-dependencies-with-bins-listed-">What happens when Composer is run on a composer.json that has dependencies with bins listed?</a> 
                    </li>
					<li>
						<a href="#what-about-windows-and-bat-files-">What about Windows and .bat files?</a> 
                    </li>
					<li>
						<a href="#can-vendor-bins-be-installed-somewhere-other-than-vendor-bin-">Can vendor bins be installed somewhere other than vendor/bin?</a> 
                    </li>
				</ul>
				<h1 id="bin-and-vendor-bin">bin and vendor/bin<a href="#bin-and-vendor-bin" class="anchor">#</a></h1>
				<h2 id="what-is-a-bin-">What is a bin?<a href="#what-is-a-bin-" class="anchor">#</a></h2>
				<p>Any command line script that a Composer package would like to pass along
					to a user who installs the package should be listed as a bin.</p>
				<p>If a package contains other scripts that are not needed by the package
					users (like build or compile scripts) that code should not be listed
					as a bin.</p>
				<h2 id="how-is-it-defined-">How is it defined?<a href="#how-is-it-defined-" class="anchor">#</a></h2>
				<p>It is defined by adding the <code>bin</code> key to a project's <code>composer.json</code>.
					It is specified as an array of files so multiple bins can be added
					for any given project.</p>
				<pre><code>{
    "bin": ["bin/my-script", "bin/my-other-script"]
}
</code></pre>
				<h2 id="what-does-defining-a-bin-in-composer-json-do-">What does defining a bin in composer.json do?<a href="#what-does-defining-a-bin-in-composer-json-do-" class="anchor">#</a></h2>
				<p>It instructs Composer to install the package's bins to <code>vendor/bin</code>
					for any project that <strong>depends</strong> on that project.</p>
				<p>This is a convenient way to expose useful scripts that would
					otherwise be hidden deep in the <code>vendor/</code> directory.</p>
				<h2 id="what-happens-when-composer-is-run-on-a-composer-json-that-defines-bins-">What happens when Composer is run on a composer.json that defines bins?<a href="#what-happens-when-composer-is-run-on-a-composer-json-that-defines-bins-" class="anchor">#</a></h2>
				<p>For the bins that a package defines directly, nothing happens.</p>
				<h2 id="what-happens-when-composer-is-run-on-a-composer-json-that-has-dependencies-with-bins-listed-">What happens when Composer is run on a composer.json that has dependencies with bins listed?<a href="#what-happens-when-composer-is-run-on-a-composer-json-that-has-dependencies-with-bins-listed-" class="anchor">#</a></h2>
				<p>Composer looks for the bins defined in all of the dependencies. A
					symlink is created from each dependency's bins to <code>vendor/bin</code>.</p>
				<p>Say package <code>my-vendor/project-a</code> has bins setup like this:</p>
				<pre><code>{
    "name": "my-vendor/project-a",
    "bin": ["bin/project-a-bin"]
}
</code></pre>
				<p>Running <code>composer install</code> for this <code>composer.json</code> will not do
					anything with <code>bin/project-a-bin</code>.</p>
				<p>Say project <code>my-vendor/project-b</code> has requirements setup like this:</p>
				<pre><code>{
    "name": "my-vendor/project-b",
    "requires": {
        "my-vendor/project-a": "*"
    }
}
</code></pre>
				<p>Running <code>composer install</code> for this <code>composer.json</code> will look at
					all of project-b's dependencies and install them to <code>vendor/bin</code>.</p>
				<p>In this case, Composer will make <code>vendor/my-vendor/project-a/bin/project-a-bin</code>
					available as <code>vendor/bin/project-a-bin</code>. On a Unix-like platform
					this is accomplished by creating a symlink.</p>
				<h2 id="what-about-windows-and-bat-files-">What about Windows and .bat files?<a href="#what-about-windows-and-bat-files-" class="anchor">#</a></h2>
				<p>Packages managed entirely by Composer do not <em>need</em> to contain any
					<code>.bat</code> files for Windows compatibility. Composer handles installation
					of bins in a special way when run in a Windows environment:</p>
				<ul><li>A <code>.bat</code> files is generated automatically to reference the bin</li>
					<li>A Unix-style proxy file with the same name as the bin is generated
						automatically (useful for Cygwin or Git Bash)</li>
				</ul><p>Packages that need to support workflows that may not include Composer
					are welcome to maintain custom <code>.bat</code> files. In this case, the package
					should <strong>not</strong> list the <code>.bat</code> file as a bin as it is not needed.</p>
				<h2 id="can-vendor-bins-be-installed-somewhere-other-than-vendor-bin-">Can vendor bins be installed somewhere other than vendor/bin?<a href="#can-vendor-bins-be-installed-somewhere-other-than-vendor-bin-" class="anchor">#</a></h2>
				<p>Yes, there are two ways that an alternate vendor bin location can be specified.</p>
				<ul><li>Setting the <code>bin-dir</code> configuration setting in <code>composer.json</code></li>
					<li>Setting the environment variable <code>COMPOSER_BIN_DIR</code></li>
				</ul><p>An example of the former looks like this:</p>
				<pre><code>{
    "config": {
        "bin-dir": "scripts"
    }
}
</code></pre>
				<p>Running <code>composer install</code> for this <code>composer.json</code> will result in
					all of the vendor bins being installed in <code>scripts/</code> instead of
					<code>vendor/bin/</code>.</p>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/articles/vendor-bins.md">fork and edit</a> it!
				</p>
            </div>
            <footer></footer>
        </div>
    </body>
</html>