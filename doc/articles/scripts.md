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
					<li>
						<a href="#what-is-a-script-">What is a script?</a> 
                    </li>
					<li>
						<a href="#event-types">Event types</a> 
                    </li>
					<li>
						<a href="#defining-scripts">Defining scripts</a> 
                    </li>
				</ul>
				<h1 id="scripts">Scripts<a href="#scripts" class="anchor">#</a></h1>
				<h2 id="what-is-a-script-">What is a script?<a href="#what-is-a-script-" class="anchor">#</a></h2>
				<p>A script is a callback (defined as a static method) that will be called
					when the event it listens on is triggered.</p>
				<p><strong>Scripts are only executed on the root package, not on the dependencies
						that are installed.</strong></p>
				<h2 id="event-types">Event types<a href="#event-types" class="anchor">#</a></h2>
				<ul><li><strong>pre-install-cmd</strong>: occurs before the install command is executed.</li>
					<li><strong>post-install-cmd</strong>: occurs after the install command is executed.</li>
					<li><strong>pre-update-cmd</strong>: occurs before the update command is executed.</li>
					<li><strong>post-update-cmd</strong>: occurs after the update command is executed.</li>
					<li><strong>pre-package-install</strong>: occurs before a package is installed.</li>
					<li><strong>post-package-install</strong>: occurs after a package is installed.</li>
					<li><strong>pre-package-update</strong>: occurs before a package is updated.</li>
					<li><strong>post-package-update</strong>: occurs after a package is updated.</li>
					<li><strong>pre-package-uninstall</strong>: occurs before a package has been uninstalled.</li>
					<li><strong>post-package-uninstall</strong>: occurs after a package has been uninstalled.</li>
				</ul><h2 id="defining-scripts">Defining scripts<a href="#defining-scripts" class="anchor">#</a></h2>
				<p>Scripts are defined by adding the <code>scripts</code> key to a project's <code>composer.json</code>.</p>
				<p>They are specified as an array of classes and static method names.</p>
				<p>The classes used as scripts must be autoloadable via Composer's autoload
					functionality.</p>
				<p>Script definition example:</p>
				<pre><code>{
    "scripts": {
        "post-update-cmd": "MyVendor\\MyClass::postUpdate",
        "post-package-install": [
            "MyVendor\\MyClass::postPackageInstall"
        ]
    }
}
</code></pre>
				<p>The event handler receives a <code>Composer\Script\Event</code> object as an argument,
					which gives you access to the <code>Composer\Composer</code> instance through the
					<code>getComposer</code> method.</p>
				<p>Using the previous example, here's an event listener example :</p>
				<pre><code>&lt;?php

namespace MyVendor;

use Composer\Script\Event;

class MyClass
{
    public static function postUpdate(Event $event)
    {
        $composer = $event-&gt;getComposer();
        // do stuff
    }

    public static function postPackageInstall(Event $event)
    {
        $installedPackage = $event-&gt;getOperation()-&gt;getPackage();
        // do stuff
    }
}
</code></pre>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/articles/scripts.md">fork and edit</a> it!
				</p>
            </div>
            <footer></footer>
        </div>
    </body>
</html>