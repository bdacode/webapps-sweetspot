# INITIAL SET UP

To run the build, you'll need to install some node modules.
Run the following in the top-level directory of the project:

    npm install

grunt now requires that you install grunt-cli globally
to be able to use grunt from the command line. To install
grunt-cli do:

    npm install -g grunt-cli

Note that if you want to install the application to a Tizen device
as a wgt file, you will also need to install the sdb tool first.
This is available for various platforms from
http://download.tizen.org/tools/latest-release/.

Configure your package manager to use the appropriate repo from the
ones available and install sdb, e.g. for Fedora 17:

    $ REPO=http://download.tizen.org/tools/latest-release/Fedora_17/tools.repo
    $ sudo yum-config-manager --add-repo $REPO
    $ sudo yum install sdb

# WHERE'S THE APP?

There are a few options for running the application:

*   Open app/index.html in a browser (there's no requirement to
    run a build before you can run the app).

*   Serve the app from a standard web server. First, run:

        grunt dist

    Then copy the content of the build/app/ directory to a web folder
    for your server (e.g. an Apache htdocs directory).

*   Install/reinstall to an attached Tizen device via sdb by running:

        grunt wgt-install

    This installs an optimised version of the app (minified HTML,
    minified and concatenated CSS and JS).

*   Install an SDK-specific version of the app (no minification or
    concatenation) with:

        grunt sdk-install

*   Build the files for the Chrome extension with:

        grunt crx

    then load the build/crx directory as an unpacked extension in Chrome
    developer mode. (The build can't currently make full .crx packages.)

*   On Linux, use make to install the app to /usr/share/. If you are
    using the Chromium browser, you can use the Makefile as is; if not, edit the
    Makefile so the BROWSER= variable is set to the name of your Chrome
    binary (e.g. google-chrome instead of chromium-browser).

    Then do

        sudo make install

    to install the application. On Linux desktops which support the
    freedesktop.org specs, this will add the application to the standard
    application launcher.

# PACKAGING

The application can be packaged into a wgt (zip) file using the grunt
command:

    grunt wgt

This will generate a package in the build/ directory.

It can also be packaged into an SDK wgt file (with uncompressed JS,
CSS, and HTML) using:

    grunt sdk

Note that in both cases, the files comprising the packages are
first copied into the build/wgt and build/sdk directories respectively.

# GUIDE FOR MS WINDOWS USERS AND TIZEN IDE

Here are some steps to help people wishing to generate code for use in the Tizen IDE on Microsoft Windows.

1. install git
1. get admin shell
1. click start
1. in ‘search’ type ‘command’ - don’t hit return/enter
1. ‘command prompt’ appears under ‘programs’ - right click on it and select ‘run as administrator’ - click ‘yes’ if it asks for confirmation
1. install grunt - type ‘npm install -g grunt’
1. install bower - type ‘npm install -g bower’
1. close admin shell
1. right click on desktop and select ‘git bash’
1. change directory to where you want your projects to go (or don’t, if Desktop is ok)
1. clone the repository, eg ‘git clone https://github.com/01org/webapps-annex.git’
1. cd webapps-annex
1. npm install
1. bower install
1. grunt sdk
1. the project is now built in build/sdk and can be imported into the IDE
1. launch Tizen IDE
1. File->New->Tizen Web Project
1. select all the files in the project and delete them
1. File->Import…->General->File System Next
1. “From directory” <- the build/sdk directory
1. “Into folder” <- the project you created in the IDE
1. Finish
