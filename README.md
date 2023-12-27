# GRA

GRA (Guess RetroArch) is a simple script to select the core to use for content in RetroArch without you having to use the -L/\--librero command-line option.

This way, you can specify that e.g. your file manager open .7z and .zip files in GRA and it will correctly detect the core.

In fact, this script was adapted from the menu code I was already using in Midnight Commander (moved partly so that the menu file won't be so bloated).

It should work with most (if not all) Bourn and Korn shells.

## USAGE

`gra [-a] [`*rom-file*`] [`*options*`]`

If `-a` is used, *gra* will automatically select a core (which may or may not work for the ROM) instead of opting the user to chose one.

The order of the arguments is important.  If the *rom-file* argument isn't a file, GRA will just pass the arguments directly to $RETROARCH (see ENVIRONMENT VARIABLES).

The ROM file can be contained in a .zip or .7z file, as long as the build of RetroArch you have supports them.  GRA itself doesn't check for whether $RETROARCH has support for these files.

## REQUIREMENTS

You will have to have a shell scripting environment installed.  On most OSes, you should already have one.  On Windows, you'll need Cygwin, MSYS2, or similar.

This hasn't been tested on Windows or Mac, so YMMV.  I have tested the basic Windows logic with WINE, though.

Apart from obviously needing RetroArch (though, it should work with Ludo too), you'll also need [the info files](http://buildbot.libretro.com/assets/frontend/info.zip) for the cores (the info files are only way it knows what file types a core supports).

## ENVIRONMENT VARIABLES

* RETROARCH: The RetroArch executable to use.
* LIBRETRO_DIRECTORY: The directory containing the cores and the info files for the cores.
* coresdir: the directory containing the cores. Overrides LIBRETRO_DIRECTORY.
* infodir: the directory containing the info files for the cores. Overrides LIBRETRO_DIRECTORY.

Those have reasonable defaults that should work, but you can override them in your shell's environment file or whatever.

## NOTABLE CHANGES FROM THE MIDNIGHT COMMANDER SCRIPT

* I added basic support for OSX and Windows, but these are untested.  Users of those OSes will have to do it.
* I made it more POSIX-compliant and it works in all of the shells I've tried.
* I replaced `test` with brackets, like is done in most shell scripts.  I don't know whether that's more widely supported or if people just prefer the C-ish syntactic sugar.
* I added gettext functionality, but nothing has been translated yet.

## COMPATIBILITY

It works with all the shells I've tried, including:

1. bash - default on most Linux distributions, Cygwin, MinGW, Mac OSX, etc.
2. dash - default on Debian, Ubuntu, and some other Linux distributions.  Based on NetBSD ash.
3. ksh - default on Solaris (if your PATH is set up correctly to use [POSIX-compliant tools](https://docs.oracle.com/cd/E88353_01/html/E37853/standards-7.html#REFMAN7standards-7)) and seemingly on newer versions of Mac OS X.

Not all features are available with all shells, though.

## TODO

* Read the user's retroarch.cfg file so that `$coresdir` and `$infodir` will be unnecessary.
* Create a few translations.
* Makefile to install everything.
* Simplify everything by requiring shells supporting Korn additions (which would leave minimal shells like dash unable to run it)?

## LICENSE

Public domain, I suppose.  It's not like anyone will want to claim this little script as their own.
