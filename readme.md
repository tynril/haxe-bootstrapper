Haxe Bootstrapper
=================

This Ant-based bootstrapper allows you to set up an up-to-date, bleeding edge Haxe and Neko development environment on your computer, by executing a single, dependency-less script. The tool will download the latest *nightly-build* of **Haxe**, as well as the *latest release* of the **Neko VM**, and set those up inside the directory where the bootstrapper lies.

Your user environment will also be properly configured, creating the necessary variables and enabling system-wide access to Haxe and Neko.

It will also configure the directory that `haxelib` (the library management tool that comes with Haxe) uses to store your libraries, allowing you to easily upgrade your Haxe installation by simply **re-running the script**.

Which platforms are supported?
------------------------------

The script is designed to work on **Windows** and **Mac OS X**.

It was tested on the following platforms:

*   Windows 7 
*   MacOS X 10.6
*   MacOS X 10.7 (uses 10.6 builds)

How to make it work?
--------------------

You need [Apache Ant](http://ant.apache.org/) to run the script. This tool can be freely downloaded, or installed automatically by some OS (`sudo apt-get install ant`). The full installation guide is provided by Apache [here](http://ant.apache.org/manual/install.html). Also, Ant relies on Java to run, which means you'll need Java runtimes as well.

Once you have Ant properly set-up, simply clone this repository where you want to install your Haxe environment, and run:
> `ant -f bootstrapper.xml`

And that's it, you're done. You might need to start a new command-line prompt or terminal to access the Haxe and Neko binaries, because the environment variables defined by the script might not be propagated to the terminal you used to run the script itself.

On MacOS X, you might be prompted for a password. This is your `sudo` password, and it is asked so the Bootstrapper can create symbolic links of Haxe in your `/usr/bin` directory.

What happens exactly?
---------------------

The bootstrapper does the following operations, in that order:

1. It will check that your operating system is supported.
2. It will download the latest nightly build of Haxe (as found [in the official nightly builds page](http://haxe.cmt.tc/)) and extract it in an `haxe` directory created where the script is being run.
3. It will set the `HAXEPATH` and `HAXE_LIBRARY_PATH` environment variables to point to that directory and to the `std` directory it contains, respectively, using `setx` on Windows, and `launchctl setenv` on MacOS X.
4. It will download the latest release of NekoVM (as found [on the download page of NekoVM](http://nekovm.org/download)) and extract it in a `neko` directory created where the script is being run.
5. It will set the `NEKOPATH` environment variable to point to that directory, using the same tools as before.
6. On MacOS X, it will create a symbolic link on `/etc/lib/libneko.dylib`, pointing to the `libneko.dylib` file in the directory where Neko was uncompressed.
7. It will build `haxelib` and `haxedoc` from their sources, and copy the executables to the `haxe` directory.
8. It will configure `haxelib` to use a `libs` directory created at the same level as the `haxe` and `neko` directories to store the libraries you'll download.
9. It'll add all Haxe and Neko executables (namely `haxe`, `haxelib`, `haxedoc`, `neko`, `nekoc`, `nekoml` and `nekotools`) to your binaries environment. That is being done by appending `%HAXEPATH%;%NEKOPATH%` to your (user) `PATH` environment variable on Windows, and by creating symlinks for all those files in `/usr/bin` on MacOS X.
