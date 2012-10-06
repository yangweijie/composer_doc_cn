<!DOCTYPE html>
<html class="no-js" lang="zh">
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
				<h1 id="why-are-version-constraints-combining-comparisons-and-wildcards-a-bad-idea-">Why are version constraints combining comparisons and wildcards a bad idea?<a href="#why-are-version-constraints-combining-comparisons-and-wildcards-a-bad-idea-" class="anchor">#</a></h1>
				<p>This is a fairly common mistake people make, defining version constraints in
					their package requires like <code>&gt;=2.*</code> or <code>&gt;=1.1.*</code>.</p>
				<p>If you think about it and what it really means though, you will quickly
					realize that it does not make much sense. If we decompose <code>&gt;=2.*</code>, you
					have two parts:</p>
				<ul><li><code>&gt;=2</code> which says the package should be in version 2.0.0 or above.</li>
					<li><code>2.*</code> which says the package should be between version 2.0.0 (inclusive)
						and 3.0.0 (exclusive).</li>
				</ul><p>As you see, both rules agree on the fact that the package must be &gt;=2.0.0,
					but it is not possible to determine if when you wrote that you were thinking
					of a package in version 3.0.0 or not. Should it match because you asked for
					<code>&gt;=2</code> or should it not match because you asked for a <code>2.*</code>?</p>
				<p>For this reason, Composer just throws an error and says that this is invalid.
					The easy way to fix it is to think about what you really mean, and use only
					one of those rules.</p>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/faqs/why-are-version-constraints-combining-comparisons-and-wildcards-a-bad-idea.md">fork and edit</a> it!
				</p>
            </div>
            <footer></footer>
        </div>
    </body>
</html>