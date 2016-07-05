# How to use

First you probably want to stop running your Red Eclipse using
`redeclipse.sh`/`redeclipse.bat`/`redeclipse_server.sh`/`redeclipse_server.bat`
scripts. They download new files which is likely to break patched Red
Eclipse. Learn to use `git` for updates instead. And use binaries
`bin` folder of Red Eclipse to run the game.

All patches were created for the stable branch of Red Eclipse
repository. For each patch there's specified latest commit hash with
which it is known to work.

You can apply a patch using following commands

```
$ git clone https://github.com/zaquest/repatches path/to/repatches
$ cd path/to/redeclipse/source
$ patch -p1 < path/to/repatches/wanted.patch
$ make -C src install
```

If you have patched Red Eclipse and want to update your game the following
should work most of the time. However, you better learn what you're doing
before running these commands. Also make sure all your patches work
with the latest stable branch before updating in this manner.

```
$ git stash
$ git pull
$ git submodule update
$ git stash pop
$ make -C src install
```

# Patches

## Fix third person crosshair for zoom / fix_3p_zoom.patch

Crosshair's default behavior in third person in Red Eclipse 1.5 is
to move cursor appropriately when zooming and getting too close to
surfaces. However the former might be annoying and the later is still
broken. It is necessary to move crosshair because Red Eclipse switches
from third to first person for zooming.  Cursor's behavior is
controlled with `thirdpersoncursor` variable.  This patch disables
default behavior (sets `thirdpersoncursor 0` by default) and
introduces new variable `thirdpersonzoom`. The variable works only
when `thirdpersoncursor` is `0` and when set it prevents Red Eclipse
from switching to first person for zooming from third person.

Known to work with 630847a
