Ia Mame
=======

IaMame is a thin command line wrapper for the Mame Emulator which downloads
automatically needed system roms and software from [The Internet Archive 
Mess and Mame collections](https://archive.org/details/messmame) if they are 
not found on the rompath directory before execution.
No needs to have Gigas of roms collections on your drive anymore.

**It is still under development** but actualy works for Mame roms, softwarelist 
roms
and most of cd-rom CHD collections. I'm facing issues on some CHD collections 
(pxs, saturn) due to version differences between the collection and the 
Mame executable. It is especially true if the delta of the version is high.
(PSX CHDs will work great using Mame v0.161 but not with 0.170 for example)

The goal of `ia-mame` is to be totally transparent. So simply tell it where is
your mame executable and use it like the real mame. 

It works on Linux, Windows, and should work on Mac but it has not been tested.

Prerequisites
-------------

- Mame 0.161+

- Java 1.7+

Be sure your Mame copy works as expected before trying IaMame, especially 
be sure that one of the paths on the rompath parameter is writable. IaMame 
will store downloaded files on the first writable found.

Installation
------------

- Make sure you have Java 7+ and Mame somewhere on your drive.

- Make sure your Vanilla Mame copy works as expected

- Make the Mame rompath writable if it is not, or tweak the Mame
  'rompath' parameter on the mame.ini to add a writable one.

- Download the 
  [release tarball](https://github.com/TiBeN/ia-mame/releases/latest) and 
  unzip it somewhere.

- IaMame needs to know where is your Mame executable. You can make it 
  available from your $PATH environment, IaMame will find it itself if its 
  name matches something like mame[64][.exe]. Otherwise, you can set it
  using the $MAME_EXEC environment variable.
 
### Compilation from the sources

The compilation requires Maven.

- git clone this repository:

```bash
$ git clone https://github.com/TiBeN/ia-mame
```

- Build and package using maven:

```bash
$ cd /path/to/ia-mame
$ mvn package
```

Usage
-----

IaMame is a wrapper and works like the original Mame. Just tell it where
is your mame executable if not available on your PATH and use it like the
real Mame.

### Linux and MacOs

```
# Let's try Street Fighter 2 arcade board
$ cd /path/to/ia-mame/bin
$ export MAME_EXEC=/path/to/mame64
$ ia-mame sf2
INFO: Download from archive.org missing rom files: [sf2] for machine "Stree...
Downloading 668kB / ??kB, progress: ??

# Mame is launched when downloadsfinished
```

### Windows 

```
# Let's try Columns on the Sega Master System
C:\> cd \path\to\ia-mame\bin
C:\> SET MAME_EXEC=C:\path\to\your\Mame
C:\> ia-mame.bat sms columns
INFO: Download from archive.org missing rom files: [sms] for machine "Master..
Downloading 25kB / ??kB, progress: ??
INFO: Download from archive.org missing software file: Software: [device: sms_cart, name: Columns (Eu...
Downloading 4kB / ??kB, progress: ??

# Mame is launched when downloads finished
```

If you feels not confortable with the Mame command line, i suggest you to
become familiar with it by reading the official 
[documentation](http://docs.mamedev.org/). The original [MESS
documentation](http://www.mess.org/mess/howto) can be pretty useful too to 
better understand the softwarelist mechanism and knowing which `<system>` 
and `<software>` names to type. Mess is now merged with Mame but was 
previously the console/computer part of Mame. 

What's more, i'm planning to do a very rudimentary GUI to simplify things a
little for users which do not like command line, especially on Windows
environment.

I have not tested now but IaMame should be compatible with frontends, the
usage command line beeing the same as the original Mame.
