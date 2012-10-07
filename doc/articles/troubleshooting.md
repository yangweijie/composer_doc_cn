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
				<ul class="toc">
				</ul>
				<h1 id="memory-limit-errors">Memory limit errors<a href="#memory-limit-errors" class="anchor">#</a></h1>
				<p>If composer shows memory errors on some commands:</p>
				<pre><code>PHP Fatal error:  Allowed memory size of XXXXXX bytes exhausted &lt;...&gt;
</code></pre>
				<p>The <code>memory_limit</code> ini value should be increased.</p>
				<blockquote>
					<p><strong>Note:</strong> Composer internally increases the memory_limit to 512M.
						It is a good idea to create an issue for composer if you get memory errors.</p>
				</blockquote>
				<p>Get current value:</p>
				<pre><code>php -r "echo ini_get('memory_limit').PHP_EOL;"
</code></pre>
				<p>Increase limit with <code>php.ini</code> for a <code>CLI SAPI</code> (ex. <code>/etc/php5/cli/php.ini</code> for Debian-like systems):</p>
				<pre><code>; Use -1 for unlimited or define explicit value like 512M
memory_limit = -1
</code></pre>
				<p>Or with command line arguments:</p>
				<pre><code>php -d memory_limit=-1 composer.phar &lt;...&gt;
</code></pre>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/articles/troubleshooting.md">fork and edit</a> it!
				</p>
            </div>
            <footer></footer>
        </div>
    </body>
</html>