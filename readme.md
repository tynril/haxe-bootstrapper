Haxe Bootstrapper
=================

This Ant-based bootstrapper allows you to set up an up-to-date, bleeding edge Haxe and Neko development environment on your computer, by executing a single, dependency-less script. The tool will download the latest *nightly-build* of **Haxe**, as well as the *latest release* of the **Neko VM**, and set those up inside the directory where the bootstrapper lies.

Your user-based environment will also be properly configured, adding the necessary `HAXEPATH` and `NEKOPATH` environment variables to your configuration, and appending those to your `PATH`.

It will also configure the directory that `haxelib` (the library management tool that comes with Haxe) uses to store your libraries, allowing you to easily upgrade your Haxe installation by simply **re-running the script**.

How to make it work?
--------------------

You need [Apache Ant](http://ant.apache.org/) to run the script. This tool can be freely downloaded, or installed automatically by some OS (`sudo apt-get install ant`). The full installation guide is provided by Apache [here](http://ant.apache.org/manual/install.html). Also, Ant relies on Java to run, which means you'll need Java runtimes as well.

Once you have Ant properly set-up, simply clone this repository where you want to install your Haxe environment, and run:
> `ant -f bootstrapper.xml`

And that's it, you're done.
