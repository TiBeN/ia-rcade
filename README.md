ia-rcade
========

[![Build
Status](https://travis-ci.org/TiBeN/ia-rcade.svg?branch=master)](https://travis-ci.org/TiBeN/ia-rcade)

`ia-rcade` allows you to use the emulator [MAME](http://mamedev.org/) with
[roms hosted at archive.org](https://archive.org/details/messmame).

Machines ROMs/CHDs and software lists ROMs/CHDs are supported. 

Before using `ia-rcade` please read the [legal
notes](https://github.com/TiBeN/ia-rcade#legal) below.

![preview](./doc/screenshot.png)

Prerequisites
-------------

-   [Java](https://www.java.com/fr/download/) 1.8+.

    Mac OS x Users: Some users reported issues to install Java Superior
    to 6. If it is you case, read this [Stack Overflow
    thread](http://stackoverflow.com/questions/12757558/installed-java-7-on-mac-os-x-but-terminal-is-still-using-version-6).

-   A version of [Mame](http://mamedev.org/release.php) 0.149+ that
    suits your operating system. Make sure Mame is correctly installed
    and works as expected before trying `ia-rcade`. Recommended version
    is one that match exactly one of the [available romsets at
    archive.org](https://archive.org/details/messmame?&sort=publicdate).
    As of now, available romsets range from 0.149 to 0.197. So
    recommended version is 0.197. If your Mame version does not match
    exactly a romset version, `ia-rcade` searchs for roms in greatest
    romsets version less than your Mame version. In this case, some
    required files may be missing. Its a hit or miss but works pretty
    well if the version delta between Mame and romsets is not too high.
    Previous versions of Mame are available
    [here](http://mamedev.org/oldrel.html).

Warning
-------

Despite `ia-rcade` can be considered safe, it is for now a beta software.  It
should not affect the roms into your rompath. But if you take care of your
collection, it would be safer to try `ia-rcade` with another rompath. See
[below](https://github.com/TiBeN/ia-rcade#use-a-different-rompath)

If you change your version of Mame, i recommend you to use another empty
rompath to prevent a `mixed versions romset`. Some roms could have been
changed from a romset version to another so it is safer to download them
again.

Installation
------------

### Linux / OS X

-   Make your rompath writable or add another writable one on the
    'rompath' directive of `mame.ini`

        $ chmod +w /path/to/mame/roms

-   Install `ia-rcade` and make it executable:

        $ sudo curl -fsSLo /usr/local/bin/ia-rcade https://github.com/TiBeN/ia-mame/releases/download/1.2/ia-rcade
        $ sudo chmod +x /usr/local/bin/ia-rcade

-   Tell `ia-rcade` where is your Mame executable by making it available
    on your \$PATH environment variable — its name must match
    mame\[64\]\[.exe\] — or by setting on your \~./bashrc, or
    \~/.bash\_profile or somewhere else, the \$MAME\_EXEC environment
    variable:

        $ vim ~/.bashrc
        export MAME_EXEC=/path/to/mame64

### Windows

-   Download
    [ia-rcade.exe](https://github.com/TiBeN/ia-rcade/releases/download/1.2/ia-rcade.exe)
    and place it on the folder where is your mame.exe

You can alternatively place it somewhere else and use the \$MAME\_EXEC
env variable:

    C:\> SET MAME_EXEC=C:\Users\tiben\mame\mame.exe

### Compilation from the sources

The compilation requires `Maven`.

-   git clone this repository:

        $ git clone https://github.com/TiBeN/ia-rcade

-   Build and package using maven:

        $ cd /path/to/ia-rcade
        $ mvn package

The binary files `ia-rcade` (Linux/OS X) and `ia-rcade.exe` (Windows) and
the executable jar are available on the `target` directory.

Usage
-----

`ia-rcade` acts like a `command wrapper` of the original Mame executable.
Use it exactly like the original Mame command line. When you launch a
game or a system, `ia-rcade` looks at your rompath to determine what
ROM/CHD files are missing and fetch them from archive.org into your
rompath. Once the files are downloaded, it returns control to original
Mame executable which launches the game/system.

### Linux, Os X

Let's try `Galaxian`. Simply type what you would have typed with the original
Mame to launch the game:

    $ ia-rcade galaxian

### Windows

Let's try Pacman. Open a console `cmd` then type:

    C:\> cd \path\to\mame
    C:\> ia-rcade.exe pacman

### Executable JAR

Alternatively, the provided [executable
jar](https://github.com/TiBeN/ia-rcade/releases/download/1.2/ia-rcade.jar)
can be used directly:

    $ java -jar ia-rcade.jar sf2

### Use a different rompath

If you want to try `ia-rcade` using a different rompath than your Mame's
default, you can use the original Mame option `-rompath` on the
command-line.

    $ ia-rcade -rompath /tmp sms sonic

### Disable Mame execution

It is possible to run `ia-rcade` without running Mame afterward using the
`-noexecmame` option. This can be useful if you only want to download a
rom file without execute the game. If the rom is already available,
`ia-rcade` simply does nothing.

    $ ia-rcade -noexecmame sms sonic

Known limitations
-----------------

### No GUI support

`ia-rcade` does not work when used with the included Mame GUI. However it
should work with frontends using some tweaks. Reddit user `jstefa`
managed to make [`ia-rcade` work in his
cab](https://www.reddit.com/r/MAME/comments/4fruod/iamame_05_mame_thin_wrapper_which_downloads/d4xqj0l/)
with the frontend [attract-mode](http://attractmode.org/).

### Some ROMs/CHDs are missing

`ia-rcade` relies on [romsets
available](https://archive.org/details/messmame?&sort=publicdate) at
archive.org. Not all romsets for all Mame versions are hosted and some
versions miss parts like softwarelist or chd sets. `ia-rcade` tries to
find missing roms in previous collections but olders roms may not work
with a more recent version of Mame.

Legal
-----

`ia-rcade` is an independant project and is in any way associated
with the official Mamedev team.

`ia-rcade` uses archive.org as a service and does not host nor provide
directly any rom file.

Some rom files are the proprietary of copyright holders.

Contact and contributions
-------------------------

If you want to contribute or simply share your thoughs about `ia-rcade`
feel free to send your pull requests here at github or join me at
[reddit](https://www.reddit.com/user/tiben_/).

One really simple contribution is keep me informed when new romsets are
hosted at archive.org.

Discussions
-----------

Releases announces on reddit triggered some good discussions:

-   [0.5 on
    /r/MAME](https://www.reddit.com/r/MAME/comments/4fruod/%60ia-rcade%60_05_mame_thin_wrapper_which_downloads/)
-   [0.7 on
    /r/emulation](https://www.reddit.com/r/emulation/comments/4tkrqb/%60ia-rcade%60_07_released/)

