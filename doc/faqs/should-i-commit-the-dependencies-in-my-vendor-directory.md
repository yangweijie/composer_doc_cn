<!DOCTYPE html>
<html class="no-js" lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
        <title>Composer</title>
        <meta name="description" content="Dependency Management for PHP">
        <meta name="viewport" content="width=device-width,initial-scale=1">
        <link rel="stylesheet" href="../css/style.css?v=5">
        <script src="../js/libs/modernizr-2.0.6.min.js"></script>
    </head>
    <body>
        <div id="container">
            <header>
				<a href="/">Home</a><a class="" href="../doc/00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                            
			</header>
            <div id="main" role="main">
				<ul class="toc"></ul>
				<h1 id="should-i-commit-the-dependencies-in-my-vendor-directory-">Should I commit the dependencies in my vendor directory?<a href="#should-i-commit-the-dependencies-in-my-vendor-directory-" class="anchor">#</a></h1>
				<p>The general recommendation is <strong>no</strong>. The vendor directory (or wherever your
					dependencies are installed) should be added to <code>.gitignore</code>/<code>svn:ignore</code>/etc.</p>
				<p>The best practice is to then have all the developers use Composer to install
					the dependencies. Similarly, the build server, CI, deployment tools etc should
					be adapted to run Composer as part of their project bootstrapping.</p>
				<p>While it can be tempting to commit it in some environment, it leads to a few
					problems:</p>
				<ul><li>Large VCS repository size and diffs when you update code.</li>
					<li>Duplication of the history of all your dependencies in your own VCS.</li>
					<li>Adding dependencies installed via git to a git repo will show them as
						submodules. This is problematic because they are not real submodules, and you
						will run into issues.</li>
				</ul><p>If you really feel like you must do this, you have two options:</p>
				<ul><li>Limit yourself to installing tagged releases (no dev versions), so that you
						only get zipped installs, and avoid problems with the git "submodules".</li>
					<li>Remove the .git directory of every dependency after the installation, then
						you can add them to your git repo. You can do that with <code>rm -rf vendor/**/.git</code>
						but this means you will have to delete those dependencies from disk before
						running composer update.</li>
				</ul>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/faqs/should-i-commit-the-dependencies-in-my-vendor-directory.md">fork and edit</a> it!
				</p>
            </div>
            <footer></footer>
        </div>
    </body>
</html>