# The Sims 2 Patches for Wine

This repository contains a collection of patches to get The Sims 2 working under
the [Wine Compatibility Layer](https://www.winehq.org/).


## What's this?

The Sims 2 is one of those classics that is highly unlikely to be ported to
another platform.

There are some technical limitations that prevents The Sims 2 from working in Wine,
the most obvious one being **Direct3D returned an error: D3DERR_INVALIDCALL!**.
It's one of the reasons why the game remains
[**Garbage** on AppDB](https://appdb.winehq.org/objectManager.php?sClass=application&iId=1942). Also [voted #6](https://appdb.winehq.org/votestats.php)!

Fear not, as some bug busters have patched the source to enables developers to
investigate the missing Direct3D features, as well as enabling Sims 2 fans to start
the game with some graphical issues. This repository will maintain the latest
copy of Wine with these patches for you to test, debug or play.


## Releases

See the **Releases** page for the compiled binaries, which can also be imported
in front-ends such as [PlayOnLinux](http://www.playonlinux.com/en).

These are built on **Ubuntu 16.04 (x86)** system, meaning they will only
compatible with a **32-bit Wine prefix**.


## Credits

I take no credit for the patches.

Comment | Author                | Notes
--------| --------------------- | -----------------
124     | swswine               | Initial Patch
160     | Robert Walker         | Updated to Wine 3.5.
161     | Alexandr Oleynikov    | Updated to Wine 3.7 with staging patches.
164     | Paul Gofman           | Updated to Wine 3.18, works with newer drivers.

These patches are copies [from bug report 8051](https://bugs.winehq.org/show_bug.cgi?id=8051).


## Known Issues

TBA

**Please do not submit test reports to AppDB when using patched copies of Wine
as the test results do not reflect the nature of "vanilla" Wine.**

## Compile from Source

1. Clone this repository to acquire the patches.

    git clone https://github.com/lah7/sims-2-wine-patches.git

2. Download a copy of the Wine source code from https://dl.winehq.org/wine/source/

    tar -xvf wine-XXX.tar.bz2
    ln -s wine-XXX a
    patch -p0 < /path/to/file.patch
    cd wine-XXX/
    ./configure --prefix=/path/to/build/
    make install -j4

To speed up compiling, change `-j4` to the number of processor cores you have.

#### macOS Support

I haven't compiled for this platform before, but technically, if you install
all the dependencies, Wine would be able to compile and install too.


## External Links

* YouTube 1.8-rc2 demo (Base game) - https://www.youtube.com/watch?v=j-pFDlEtnC0
* YouTube 1.8-rc2 demo (EP9 game) - https://www.youtube.com/watch?v=h9rZPdNLd6I&t=37s
* Lutris - https://lutris.net/games/the-sims-2/


## License

Wine is distributed under the [GNU Lesser General Public License 2.1](https://source.winehq.org/source/LICENSE).

