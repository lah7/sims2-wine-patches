# The Sims 2 Patches for Wine

This repository contains a collection of patches to get The Sims 2 working under
the [Wine Compatibility Layer](https://www.winehq.org/).


## What's this?

The Sims 2 is a classic, but is designed to run on Windows. It has been historically ported to Mac as
[The Sims™ 2: Super Collection](https://www.aspyr.com/games/the-sims-2-super-collection) but
is limited to 6 expansions, 3 stuff packs and hasn't seen any updates in 3+ years.

There are some technical limitations that prevents The Sims 2 from working in Wine,
the most obvious one being **Direct3D returned an error: D3DERR_INVALIDCALL!**.
It's one of the reasons why the game remains
[**Garbage** on AppDB](https://appdb.winehq.org/objectManager.php?sClass=application&iId=1942). Also [voted #6](https://appdb.winehq.org/votestats.php)!

Fear not, as some bug busters have patched the source to investigate the missing
Direct3D features. For players, The Sims 2 starts and is playable with the odd glitch!
For developers, there's some interesting things to uncover. This repository will
maintain the latest copy of Wine with these patches for you to test, debug or play.


## Binaries

See the **[Releases](https://github.com/lah7/sims-2-wine-patches/releases)** page
for the compiled binaries, which can be downloaded and used as-is, or added to
front-ends such as [PlayOnLinux](http://www.playonlinux.com/en) or
[PlayOnMac](http://www.playonmac.com/en).

The binaries are currently compiled without 64-bit support (SysWOW64), meaning they require a 32-bit Wine prefix.

Package     | Compiler OS   | Compiler Arch | Wine Prefix  | Notes |
----------- | ------------- | ------------- | ------------ | ----- | 
`linux-x86` | Ubuntu 16.04  | i386          | 32-bit       |
`mac-x86`   | macOS 10.14.2 | amd64         | 32-bit       | macOS 10.15 will deprecate 32-bit support.

macOS builds are considered experimental.

## Credits

Comment                                                     | Author                | Notes
----------------------------------------------------------- | --------------------- | -----------------
[124](https://bugs.winehq.org/show_bug.cgi?id=8051#c124)    | swswine               | Initial patch and discovery
[160](https://bugs.winehq.org/show_bug.cgi?id=8051#c160)    | Robert Walker         | Updated to Wine 3.5.
[161](https://bugs.winehq.org/show_bug.cgi?id=8051#c161)    | Alexandr Oleynikov    | Updated to Wine 3.7 with staging patches.
[164](https://bugs.winehq.org/show_bug.cgi?id=8051#c164)    | Paul Gofman           | Updated to Wine 3.18, works with newer drivers.

See [bug report 8051 on Wine's bug tracker](https://bugs.winehq.org/show_bug.cgi?id=8051) for development discussions.


## Known Issues

### Hardcoded 256 vertex shaders

The Sims 2 requests 1024 vertex shader constants, but Wine has a hardcoded limit
of 256. Direct3D 9 normally supports up to 8192, using hardware shaders first
(where available), followed by software emulation. Software emulation is currently
not supported in Wine.

### Undocumented or unimplemented D3D9 interfaces

The developers of The Sims 2 used some obscure features of Direct3D 9
as discovered in [the bug report discussion](https://bugs.winehq.org/show_bug.cgi?id=8051#c124).
Some of these will require implementation in Wine which are quite the task:

* Remove hardcoded vertex shader limit - [see D3D9_MAX_VERTEX_SHADER_CONSTANTF in d3d9_private.h](https://github.com/wine-mirror/wine/blob/2ef62f90853d9903cdded2442e382b89a4c3a55f/dlls/d3d9/d3d9_private.h#L43)
  * The game expects at least 1024.
  * *Suggestion:* Via registry?
* [Add ProcessVertices with shader support (#46742)](https://bugs.winehq.org/show_bug.cgi?id=46742)
* [Add support for undocumented Direct3DShaderValidatorCreate9() implementation (#46735)](https://bugs.winehq.org/show_bug.cgi?id=46735)

### Shader Models

Shader Model 2 and Shader Model 3 reveal differences, especially in the original
base game (no patches, no expansions). Newer expansion packs suggest an improved
rendering engine is used and may show no difference.

#### [Base game only] 3D Rendering

| Shader Model Version | `useShaders` | Screenshot |
| -------------------- | ------------ | ---------- |
| 2 | `false` | ![SM2, shaders disabled](.github/base-game-sm2-shadersfalse.jpg)
| 2 | `true` | ![SM2, shaders enabled](.github/base-game-sm2-shaderstrue.jpg)
| 3 | `false` | ![SM3, shaders disabled](.github/base-game-sm3-shadersfalse.jpg)
| 3 | `true` | ![SM3, shaders enabled](.github/base-game-sm3-shaderstrue.jpg)

The Shader Model version can be set via [Wine's registry](https://wiki.winehq.org/Useful_Registry_Keys):

    HKEY_CURRENT_USER\Software\Wine\Direct3D\MaxShaderModelPS
    HKEY_CURRENT_USER\Software\Wine\Direct3D\MaxShaderModelVS

    REG_DWORD => 2

By opening the cheat console (CTRL+SHIFT+C), you can toggle between parameters
that will effect rendering in-game:

    boolProp useShaders false
    boolProp lightingEnabled false

To play earlier versions of the game, you will need to force **Shader Model 2**
via the registry, force shaders and disable the lighting engine. Write the following:

    boolProp useShaders true
    boolProp lightingEnabled false

And save to:

    C:\users\YOURNAME\My Documents\EA Games\The Sims 2\Config\userStartup.cheat

![Base game rendering with shaders, no lighting](.github/base-game-sm2-shaders-nolighting.jpg)

This is not necessary when using newer versions of the game and expansion packs.
Results may differ on different graphic cards and drivers.

**Previous Wine patches/binaries forced Shader Model 2, but this is no longer the case.**

### Corrupted family thumbnails

The 'red eagle' pose appears on the neighbourhood screen and during loading screens.

![Red Eagle Pose](.github/red-eagle-pose.jpg)

The only exception is when a new default neighbourhood is loaded for the first time
in which the thumbnails were already pre-rendered.

### Skin tone mismatch

A Sims' skin colour may not match between their head and body.

![Skin Tone Mismatch](.github/skin-tone-mismatch.jpg)

### Polygon Explosion
Icons above a Sim's head (like the one when you get a new friend) can appear glitchy.

### Black screen after resolution changes
Changing resolution while at a household can sometimes result in a black screen.

### [NVIDIA only] Black box shadows
This also happens under the NVIDIA driver on Windows. This previously did not happen
with earlier versions of the NVIDIA driver (around 396.x and before) and the original
Wine patches.

![Black Shadow Bug](.github/black-shadow-bug.jpg)

The workaround is to set the shadow settings to **Medium**.

### [Wine] Huge log files.
As the patches expose a lot of FIXMEs. If you're running via the terminal;
keeping a log or using PlayOnLinux, beware that this can fill up to many
hundreds of MBs, causing potential slowdown.

### Other Notes

* If there are any technical explainations or issues, feel free to create a pull request.
* Please **do not** submit test reports to AppDB when using patched copies of Wine
as the test results do not reflect "vanilla" Wine.
* To view FPS and shader version in-game, press <kbd>CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>S</kbd>
* There are some engine differences/improvements between the original release,
later expansion packs and the Origin version.


## Compile from Source

Wine can be built on GNU/Linux and macOS.

1. Clone this repository to acquire the patches.

       git clone https://github.com/lah7/sims-2-wine-patches.git

2. Download a copy of the Wine source code from https://dl.winehq.org/wine/source/

3. Install the dependencies.

    https://wiki.winehq.org/Building_Wine#Satisfying_Build_Dependencies

3. Patch the source and build:

       tar -xvf wine-XXX.tar.bz2
       ln -s wine-XXX a
       patch -p0 < /path/to/file.patch
       cd wine-XXX/
       ./configure --prefix=/path/to/build/
       make install -j4

To speed up compiling, change `-j4` to the number of processor cores you have.

If running via `make` only, you can use the `wine` script to run the build.


## Bug Reports
Developers and hackers, these are the bug reports on WineHQ Bugzilla:

* [8051 - The Sims 2 demo needs support for software vertex processing](https://bugs.winehq.org/show_bug.cgi?id=8051)
* [46735 - The Sims 2 demo needs Direct3DShaderValidatorCreate9() implementation](https://bugs.winehq.org/show_bug.cgi?id=46735)
* [46742 - The Sims 2 demo needs support for ProcessVertices() with software vertex shaders](https://bugs.winehq.org/show_bug.cgi?id=46742)

## External Links
* [YouTube video demonstrating base game under Wine 1.8-rc2 (patched)](https://www.youtube.com/watch?v=j-pFDlEtnC0)
* [YouTube video demonstrating EP9 under Wine 1.8-rc2 (patched)](https://www.youtube.com/watch?v=h9rZPdNLd6I&t=37s)
* [Lutris](https://lutris.net/games/the-sims-2)
* [Lutris - GitHub Wiki](https://github.com/lutris/lutris/wiki/Game:-The-Sims-2) - covers Origin version.
* [WineHQ AppDB - The Sims 2.x](https://appdb.winehq.org/objectManager.php?sClass=version&iId=2633)


## License

Wine is distributed under the [GNU Lesser General Public License 2.1](https://source.winehq.org/source/LICENSE).

