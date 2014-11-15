OsxWineAsio
-----------
This repo is a fork from the mainline wineasio, with the intention to make it build and operate on OSX.  The mainline of wineasio can be found here:

  https://sourceforge.net/projects/wineasio/?source=directory

Hopefully these changes can be merged back into the official mainline wineasio repo at sourceforge, then this repo will go away.  For now I will try to keep it up to date if and when wineasio changes for any reason, but at least this is now up to date with version 0.9.2 of wineasio and I can confirm it builds and operates successfully on OSX.

Prebuilt binary
---------------
The prebuilt binary is available here: https://github.com/steveschow/osxwineasio/releases

Build Dependencies
------------------
Depends on several things in order to build on OSX:

1 - Must have wine installed.  There are several dev oriented binaries, libs
    and includes that are required for building wineasio.  By default this
    Makefile looks for the following include and lib dirs.

    /usr/local/include/wine
    /usr/local/include/wine/windows
    /usr/local/lib/wine

2 - Several binaries need to be in the $PATH, including winegcc, winebuild

3 - You must download steinbergs sdk and copy asio.h into the wineasio dir: https://aur.archlinux.org/packages/steinberg-asio/


TODO
----
- Try out 64bit version

- Try to see if we can make it work using the default float sample data.  Currently have found that produces no audio with JackOSX and had to use ASIOST32INT def in order to get it working.  See main README for explanation.

- see if the change to asio.c is generic enough to be used for all platforms or do ifdefs need to be used for isolating this patch only OSX?

WineApp
-------
http://winebottler.kronenberg.org/downloads

The Author of WineBottler maintains an easy to use pre-built version of wine, which includes all of the libs and includes needed to build wineasio.  This is the easiest way I know to get wine working on osx.  Just download his Wine.app, its all there.

In order to compile wineasio using this version of wine, you'll need to create some symlinks:

    ln -s /Applications/Wine.app/Contents/Resources/include/wine /usr/local/include/wine
    ln -s /Applications/Wine.app/Contents/Resources/lib/wine /usr/local/lib/wine

And make sure wine is in the PATH:

     PATH=$PATH:/Applications/Wine.app/Contents/Resources/bin
     
OSXWINEBUILDER
--------------
https://code.google.com/p/osxwinebuilder/

If you wish to build all the wine sources from scratch, osxwinewbuilder is a very nice way to build and install wine on a system, it
keeps all wine related files isolated from /usr/local.  However if you use
this version of wine, you will need to make sure the wine binaries are in the
PATH and create some sym links under /usr/local that point to some includes
and libs.

Specifically, if osxwinebuilder is installed for example in the following:

    ~/wine/wine-1.7.30

Then create several symlinks:

    ln -s ~/wine/wine-1.7.30/include/wine /usr/local/include/wine
    ln -s ~/wine/wine-1.7.30/lib/wine /usr/local/lib/wine

With the above links and the noted binaries located in the PATH, the Makefile should work the same as if using normal homebrew install of Wine, or other wine installs that place includes and libs under /usr/local

