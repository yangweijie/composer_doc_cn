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
				<a href="/">Home</a><a class="" href="/doc/00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                            
			</header>
            <div id="main" role="main">
				<ul class="toc">
					<li><a href="#why-aliases-">Why aliases?</a></li>
					<li><a href="#branch-alias">Branch alias</a></li>
					<li><a href="#require-inline-alias">Require inline alias</a></li>
				</ul>
				<h1 id="aliases">Aliases<a href="#aliases" class="anchor">#</a></h1>
				<h2 id="why-aliases-">Why aliases?<a href="#why-aliases-" class="anchor">#</a></h2>
				<p>When you are using a VCS repository, you will only get comparable versions for
					branches that look like versions, such as <code>2.0</code>. For your <code>master</code> branch, you
					will get a <code>dev-master</code> version. For your <code>bugfix</code> branch, you will get a
					<code>dev-bugfix</code> version.</p>
				<p>If your <code>master</code> branch is used to tag releases of the <code>1.0</code> development line,
					i.e. <code>1.0.1</code>, <code>1.0.2</code>, <code>1.0.3</code>, etc., any package depending on it will
					probably require version <code>1.0.*</code>.</p>
				<p>If anyone wants to require the latest <code>dev-master</code>, they have a problem: Other
					packages may require <code>1.0.*</code>, so requiring that dev version will lead to
					conflicts, since <code>dev-master</code> does not match the <code>1.0.*</code> constraint.</p>
				<p>Enter aliases.</p>
				<h2 id="branch-alias">Branch alias<a href="#branch-alias" class="anchor">#</a></h2>
				<p>The <code>dev-master</code> branch is one in your main VCS repo. It is rather common that
					someone will want the latest master dev version. Thus, Composer allows you to
					alias your <code>dev-master</code> branch to a <code>1.0.x-dev</code> version. It is done by
					specifying a <code>branch-alias</code> field under <code>extra</code> in <code>composer.json</code>:</p>
				<pre><code>{
    "extra": {
        "branch-alias": {
            "dev-master": "1.0.x-dev"
        }
    }
}
</code></pre>
				<p>The branch version must begin with <code>dev-</code> (non-comparable version), the alias
					must be a comparable dev version. The <code>branch-alias</code> must be present on the
					branch that it references. For <code>dev-master</code>, you need to commit it on the
					<code>master</code> branch.</p>
				<p>As a result, you can now require <code>1.0.*</code> and it will happily install
					<code>dev-master</code> for you.</p>
				<h2 id="require-inline-alias">Require inline alias<a href="#require-inline-alias" class="anchor">#</a></h2>
				<p>Branch aliases are great for aliasing main development lines. But in order to
					use them you need to have control over the source repository, and you need to
					commit changes to version control.</p>
				<p>This is not really fun when you just want to try a bugfix of some library that
					is a dependency of your local project.</p>
				<p>For this reason, you can alias packages in your <code>require</code> and <code>require-dev</code>
					fields. Let's say you found a bug in the <code>monolog/monolog</code> package. You cloned
					Monolog on GitHub and fixed the issue in a branch named <code>bugfix</code>. Now you want
					to install that version of monolog in your local project.</p>
				<p>You are using <code>symfony/monolog-bundle</code> which requires <code>monolog/monolog</code> version
					<code>1.*</code>. So you need your <code>dev-bugfix</code> to match that constraint.</p>
				<p>Just add this to your project's root <code>composer.json</code>:</p>
				<pre><code>{
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/you/monolog"
        }
    ],
    "require": {
        "symfony/monolog-bundle": "2.0",
        "monolog/monolog": "dev-bugfix as 1.0.x-dev"
    }
}
</code></pre>
				<p>That will fetch the <code>dev-bugfix</code> version of <code>monolog/monolog</code> from your GitHub
					and alias it to <code>1.0.x-dev</code>.</p>
				<blockquote>
					<p><strong>Note:</strong> If a package with inline aliases is required, the alias (right of
						the <code>as</code>) is used as the version constraint. The part left of the <code>as</code> is
						discarded. As a consequence, if A requires B and B requires <code>monolog/monolog</code>
						version <code>dev-bugfix as 1.0.x-dev</code>, installing A will make B require
						<code>1.0.x-dev</code>, which may exist as a branch alias or an actual <code>1.0</code> branch. If
						it does not, it must be re-inline-aliased in A's <code>composer.json</code>.</p>
					<p><strong>Note:</strong> Inline aliasing should be avoided, especially for published
						packages. If you found a bug, try and get your fix merged upstream. This
						helps to avoid issues for users of your package.</p>
				</blockquote>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/articles/aliases.md">fork and edit</a> it!
				</p>
            </div>
            <footer></footer>
        </div>
    </body>
</html>