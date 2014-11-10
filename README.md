Depends on several things in order to build

1 - Must have wine installed.  There are several dev oriented binaries, libs
    and includes that are required for building wineasio.  By default this
    Makefile looks for the following include and lib dirs.

    /usr/local/include/wine
    /usr/local/include/wine/windows

    /usr/local/lib/wine

    Several binaries need to be in the path, including winegcc, winebuild

2 - have to download steinbergs asio.h file

3 - Use Makefile.osx to build wineasio:

    make -f Makefile.osx


TODO
----

- Try out 64bit version

- Need to make this more generic so that it can potentially be merged back
  into the wineasio mainline.  
   
    - Detect MacOS and include the patched changes to asio.c with ifdefs
    - detect MacOS and include the -DASIOST32INT macro in the Makefiles
    - have the makefile refer to locations where wine is installed normally
      rather then using the build location as I have done for my system, or
      have a way to configure it either way easily, but the default should
      probably be the wine installed way.

OSXWINEBUILDER
--------------

osxwinewbuilder is a very nice way to build and install wine on a system, it
keeps all wine related files isolated from /usr/local.  However if you use
this version of wine, you will need to make sure the wine binaries are in the
PATh and create some sym links under /usr/local that point to some includes
and libs.

Specifically, if osxwinebuilder is installed for example in the following:

    ~/wine/wine-1.7.30

Then create several symlinks:

    ln -s ~/wine/wine-1.7.30/include/wine /usr/local/include/wine
    ln -s ~/wine/wine-1.7.30/lib /usr/local/lib/wine

With the above links and binaries in the path, the Makefile should work the same as if using normal homebrew install of Wine, o other wine installs that place includes and libs under /usr/local
