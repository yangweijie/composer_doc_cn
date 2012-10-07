<!DOCTYPE html>
<html class="no-js">
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
					<li>
						<a href="#setup">Setup</a> 
                    </li>
					<li>
						<a href="#usage">Usage</a> 
						<ul>
							<li>
								<a href="#security">Security</a> 
							</li>

						</ul>
                    </li>
				</ul>
				<h1 id="handling-private-packages-with-satis">Handling private packages with Satis<a href="#handling-private-packages-with-satis" class="anchor">#</a></h1>
				<p>Satis can be used to host the metadata of your company's private packages, or
					your own. It basically acts as a micro-packagist. You can get it from
					<a href="http://github.com/composer/satis">GitHub</a> or install via CLI:
					<code>composer.phar create-project composer/satis</code>.</p>
				<h2 id="setup">Setup<a href="#setup" class="anchor">#</a></h2>
				<p>For example let's assume you have a few packages you want to reuse across your
					company but don't really want to open-source. You would first define a Satis
					configuration file, which is basically a stripped-down version of a
					<code>composer.json</code> file. It contains a few repositories, and then you use the require
					key to say which packages it should dump in the static repository it creates, or
					use require-all to select all of them.</p>
				<p>Here is an example configuration, you see that it holds a few VCS repositories,
					but those could be any types of <a href="../05-repositories.md">repositories</a>. Then it
					uses <code>"require-all": true</code> which selects all versions of all packages in the
					repositories you defined.</p>
				<pre><code>{
    "name": "My Repository",
    "homepage": "http://packages.example.org",
    "repositories": [
        { "type": "vcs", "url": "http://github.com/mycompany/privaterepo" },
        { "type": "vcs", "url": "http://svn.example.org/private/repo" },
        { "type": "vcs", "url": "http://github.com/mycompany/privaterepo2" }
    ],
    "require-all": true
}
</code></pre>
				<p>If you want to cherry pick which packages you want, you can list all the packages
					you want to have in your satis repository inside the classic composer <code>require</code> key,
					using a <code>"*"</code> constraint to make sure all versions are selected, or another
					constraint if you want really specific versions.</p>
				<pre><code>{
    "repositories": [
        { "type": "vcs", "url": "http://github.com/mycompany/privaterepo" },
        { "type": "vcs", "url": "http://svn.example.org/private/repo" },
        { "type": "vcs", "url": "http://github.com/mycompany/privaterepo2" }
    ],
    "require": {
        "company/package": "*",
        "company/package2": "*",
        "company/package3": "2.0.0"
    }
}
</code></pre>
				<p>Once you did this, you just run <code>php bin/satis build &lt;configuration file&gt; &lt;build dir&gt;</code>.
					For example <code>php bin/satis build config.json web/</code> would read the <code>config.json</code>
					file and build a static repository inside the <code>web/</code> directory.</p>
				<p>When you ironed out that process, what you would typically do is run this
					command as a cron job on a server. It would then update all your package info
					much like Packagist does.</p>
				<p>Note that if your private packages are hosted on GitHub, your server should have
					an ssh key that gives it access to those packages, and then you should add
					the <code>--no-interaction</code> (or <code>-n</code>) flag to the command to make sure it falls back
					to ssh key authentication instead of prompting for a password. This is also a
					good trick for continuous integration servers.</p>
				<p>Set up a virtual-host that points to that <code>web/</code> directory, let's say it is
					<code>packages.example.org</code>.</p>
				<h2 id="usage">Usage<a href="#usage" class="anchor">#</a></h2>
				<p>In your projects all you need to add now is your own composer repository using
					the <code>packages.example.org</code> as URL, then you can require your private packages and
					everything should work smoothly. You don't need to copy all your repositories
					in every project anymore. Only that one unique repository that will update
					itself.</p>
				<pre><code>{
    "repositories": [ { "type": "composer", "url": "http://packages.example.org/" } ],
    "require": {
        "company/package": "1.2.0",
        "company/package2": "1.5.2",
        "company/package3": "dev-master"
    }
}
</code></pre>
				<h3 id="security">Security<a href="#security" class="anchor">#</a></h3>
				<p>To secure your private repository you can host it over SSH or SSL using a client
					certificate. In your project you can use the <code>options</code> parameter to specify the
					connection options for the server.</p>
				<p>Example using a custom repository using SSH (requires the SSH2 PECL extension):</p>
				<pre><code>{
    "repositories": [
        {
            "type": "composer",
            "url": "ssh2.sftp://example.org",
            "options": {
                "ssh2": {
                    "username": "composer",
                    "pubkey_file": "/home/composer/.ssh/id_rsa.pub",
                    "privkey_file": "/home/composer/.ssh/id_rsa"
                }
            }
        }
    ]
}
</code></pre>
				<p>Example using HTTP over SSL using a client certificate:</p>
				<pre><code>{
    "repositories": [
        {
            "type": "composer",
            "url": "https://example.org",
            "options": {
                "ssl": {
                    "cert_file": "/home/composer/.ssl/composer.pem",
                }
            }
        }
    ]
}
</code></pre>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/articles/handling-private-packages-with-satis.md">fork and edit</a> it!
				</p>
            </div>
            <footer></footer>
        </div>
    </body>
</html>