Depends on several things in order to build on OSX

1 - Must have wine installed.  There are several dev oriented binaries, libs
    and includes that are required for building wineasio.  By default this
    Makefile looks for the following include and lib dirs.

    /usr/local/include/wine
    /usr/local/include/wine/windows
    /usr/local/lib/wine

Several binaries need to be in the path, including winegcc, winebuild

2 - have to download steinbergs asio.h file: https://aur.archlinux.org/packages/steinberg-asio/

3 - Use Makefile.osx to build wineasio:

    make -f Makefile.osx


TODO
----

- Try out 64bit version

- Need to make this more generic so that it can potentially be merged back
  into the wineasio mainline which is found here: https://sourceforge.net/projects/wineasio/?source=directory
   
    - Detect MacOS and include the patched changes to asio.c with ifdefs


OSXWINEBUILDER
--------------
https://code.google.com/p/osxwinebuilder/

osxwinewbuilder is a very nice way to build and install wine on a system, it
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

