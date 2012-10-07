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
				<a href="/">Home</a><a class="" href="../doc/00-intro.md">Getting Started</a><a class="" href="/download/">Download</a><a class="active" href="/doc/">Documentation</a><a class="last" href="http://packagist.org/">Browse Packages</a>                            </header>
            <div id="main" role="main">
				<ul class="toc">
					<li><a href="#synopsis">Synopsis</a></li>
					<li><a href="#calling-a-custom-installer">Calling a Custom Installer</a></li>
					<li>
						<a href="#creating-an-installer">Creating an Installer</a> 
						<ul>
							<li><a href="#composer-json">composer.json</a></li>
							<li><a href="#the-custom-installer-class">The Custom Installer class</a></li>
						</ul>
                    </li>
				</ul>
				<h1 id="setting-up-and-using-custom-installers">Setting up and using custom installers<a href="#setting-up-and-using-custom-installers" class="anchor">#</a></h1>
				<h2 id="synopsis">Synopsis<a href="#synopsis" class="anchor">#</a></h2>
				<p>At times it may be necessary for a package to require additional actions during
					installation, such as installing packages outside of the default <code>vendor</code>
					library.</p>
				<p>In these cases you could consider creating a Custom Installer to handle your
					specific logic.</p>
				<h2 id="calling-a-custom-installer">Calling a Custom Installer<a href="#calling-a-custom-installer" class="anchor">#</a></h2>
				<p>Suppose that your project already has a Custom Installer for specific modules
					then invoking that installer is a matter of defining the correct <a href="../04-schema.md#type">type</a> in
					your package file.</p>
				<blockquote>
					<p><em>See the next chapter for an instruction how to create Custom Installers.</em></p>
				</blockquote>
				<p>Every Custom Installer defines which <a href="../04-schema.md#type">type</a> string it will recognize. Once
					recognized it will completely override the default installer and only apply its
					own logic.</p>
				<p>An example use-case would be:</p>
				<blockquote>
					<p>phpDocumentor features Templates that need to be installed outside of the
						default /vendor folder structure. As such they have chosen to adopt the
						<code>phpdocumentor-template</code> <a href="../04-schema.md#type">type</a> and create a Custom Installer to send
						these templates to the correct folder.</p>
				</blockquote>
				<p>An example composer.json of such a template package would be:</p>
				<pre><code>{
    "name": "phpdocumentor/template-responsive",
    "type": "phpdocumentor-template",
    "require": {
        "phpdocumentor/template-installer": "*"
    }
}
</code></pre>
				<blockquote>
					<p><strong>IMPORTANT</strong>: to make sure that the template installer is present at the
						time the template package is installed, template packages should require
						the installer package.</p>
				</blockquote>
				<h2 id="creating-an-installer">Creating an Installer<a href="#creating-an-installer" class="anchor">#</a></h2>
				<p>A Custom Installer is defined as a class that implements the
					<a href="https://github.com/composer/composer/blob/master/src/Composer/Installer/InstallerInterface.php"><code>Composer\Installer\InstallerInterface</code></a> and is contained in a Composer
					package that has the <a href="../04-schema.md#type">type</a> <code>composer-installer</code>.</p>
				<p>A basic Installer would thus compose of two files:</p>
				<ol><li>the package file: composer.json</li>
					<li>The Installer class, i.e.: <code>Composer\Installer\MyInstaller.php</code></li>
				</ol><blockquote>
					<p><strong>NOTE</strong>: <em>The namespace does not need to be <code>Composer\Installer</code>, it must
							only implement the right interface.</em></p>
				</blockquote>
				<h3 id="composer-json">composer.json<a href="#composer-json" class="anchor">#</a></h3>
				<p>The package file is the same as any other package file but with the following
					requirements:</p>
				<ol><li>the <a href="../04-schema.md#type">type</a> attribute must be <code>composer-installer</code>.</li>
					<li>the <a href="../04-schema.md#extra">extra</a> attribute must contain an element <code>class</code> defining the
						class name of the installer (including namespace). If a package contains
						multiple installers this can be array of class names.</li>
				</ol><p>Example:</p>
				<pre><code>{
    "name": "phpdocumentor/template-installer",
    "type": "composer-installer",
    "license": "MIT",
    "autoload": {
        "psr-0": {"phpDocumentor\\Composer": "src/"}
    },
    "extra": {
        "class": "phpDocumentor\\Composer\\TemplateInstaller"
    }
}
</code></pre>
				<h3 id="the-custom-installer-class">The Custom Installer class<a href="#the-custom-installer-class" class="anchor">#</a></h3>
				<p>The class that executes the custom installation should implement the
					<a href="https://github.com/composer/composer/blob/master/src/Composer/Installer/InstallerInterface.php"><code>Composer\Installer\InstallerInterface</code></a> (or extend another installer that
					implements that interface).</p>
				<p>The class may be placed in any location and have any name, as long as it is
					autoloadable and matches the <code>extra.class</code> element in the package definition.
					It will also define the <a href="../04-schema.md#type">type</a> string as it will be recognized by packages
					that will use this installer in the <code>supports()</code> method.</p>
				<blockquote>
					<p><strong>NOTE</strong>: <em>choose your <a href="../04-schema.md#type">type</a> name carefully, it is recommended to follow
							the format: <code>vendor-type</code></em>. For example: <code>phpdocumentor-template</code>.</p>
				</blockquote>
				<p>The InstallerInterface class defines the following methods (please see the
					source for the exact signature):</p>
				<ul><li><strong>supports()</strong>, here you test whether the passed <a href="../04-schema.md#type">type</a> matches the name
						that you declared for this installer (see the example).</li>
					<li><strong>isInstalled()</strong>, determines whether a supported package is installed or not.</li>
					<li><strong>install()</strong>, here you can determine the actions that need to be executed
						upon installation.</li>
					<li><strong>update()</strong>, here you define the behavior that is required when Composer is
						invoked with the update argument.</li>
					<li><strong>uninstall()</strong>, here you can determine the actions that need to be executed
						when the package needs to be removed.</li>
					<li><strong>getInstallPath()</strong>, this method should return the location where the
						package is to be installed, <em>relative from the location of composer.json.</em></li>
				</ul><p>Example:</p>
				<pre><code>namespace phpDocumentor\Composer;

use Composer\Package\PackageInterface;
use Composer\Installer\LibraryInstaller;

class TemplateInstaller extends LibraryInstaller
{
    /**
     * {@inheritDoc}
     */
    public function getInstallPath(PackageInterface $package)
    {
        $prefix = substr($package-&gt;getPrettyName(), 0, 23);
        if ('phpdocumentor/template-' !== $prefix) {
            throw new \InvalidArgumentException(
                'Unable to install template, phpdocumentor templates '
                .'should always start their package name with '
                .'"phpdocumentor/template-"'
            );
        }

        return 'data/templates/'.substr($package-&gt;getPrettyName(), 23);
    }

    /**
     * {@inheritDoc}
     */
    public function supports($packageType)
    {
        return 'phpdocumentor-template' === $packageType;
    }
}
</code></pre>
				<p>The example demonstrates that it is quite simple to extend the
					<a href="https://github.com/composer/composer/blob/master/src/Composer/Installer/LibraryInstaller.php"><code>Composer\Installer\LibraryInstaller</code></a> class to strip a prefix
					(<code>phpdocumentor/template-</code>) and use the remaining part to assemble a completely
					different installation path.</p>
				<blockquote>
					<p><em>Instead of being installed in <code>/vendor</code> any package installed using this
							Installer will be put in the <code>/data/templates/&lt;stripped name&gt;</code> folder.</em></p>
				</blockquote>
				<p class="fork-and-edit">
					Found a typo? Something is wrong in this documentation? Just <a href="http://github.com/composer/composer/edit/master/doc/articles/custom-installers.md">fork and edit</a> it!
				</p>
            </div>
            <footer></footer>
        </div>
    </body>
</html>