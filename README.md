# The Sims 2 under Wine

This repository contains patches and instructions to get The Sims 2 working under
the [Wine Compatibility Layer](https://www.winehq.org/).

The Sims 2 is a classic, but is designed to run on Windows. It has been historically ported to Mac as
[The Sims™ 2: Super Collection](https://www.aspyr.com/games/the-sims-2-super-collection) but
is limited to 6 expansions, 3 stuff packs and hasn't seen any updates in 3+ years.

It's possible to play The Sims 2 almost flawlessly by either modifying your prefix
or using a patched build of Wine on Linux, and Mac too.

| Implementation            | Instructions          | Works?
| ------------------------- | --------------------- | -----------
| Wine (no modifications)   |                       | No, crashes with **Direct3D returned an error: D3DERR_INVALIDCALL!**.
| [wine-staging](https://github.com/wine-staging/wine-staging) | | Partial, severe graphical glitches.
| Wine (patched)            | [README-WineD3D.md](README-WineD3D.md) | Yes, with workarounds.
| [D9VK](https://git.froggi.es/joshua/d9vk) | [README-D9VK.md](README-D9VK.md) | **Yes, recommended** for Vulkan-enabled graphics cards.
| [Lutris](https://lutris.net/games/the-sims-2/) | | Yes!

The easiest to setup and provides the best compatibility is [D9VK](README-D9VK.md),
providing your graphics driver and hardware supports Vulkan.


## Note for NVIDIA users

### Black boxes for "High" shadows

This also happens under the NVIDIA driver on Windows. This previously did not happen
with earlier versions of the NVIDIA driver (around 396.x and before).

![Black Shadow Bug](.github/black-shadow-bug.jpg)

This can be fixed by installing the [Sim Shadow Fix](http://modthesims.info/d/569585/sim-shadow-fix-updated-2-jan-16.html) (v0.4) mod.
Extract this into `My Documents/EA Games/The Sims 2/Downloads`.


## Don't forget...

The Sims 2 doesn't work with an unmodified version of Wine, but does start
with **wine-staging**. Please **do not** submit bug reports of patched versions, Lutris
or D9VK versions to AppDB.

* [AppDB entry for The Sims 2](https://appdb.winehq.org/objectManager.php?sClass=application&iId=1942)
* [AppDB's stats - The Sims 2 is voted **#6**!](https://appdb.winehq.org/votestats.php)


## External Links

* [YouTube video demonstrating base game under Wine 1.8-rc2 (patched)](https://www.youtube.com/watch?v=j-pFDlEtnC0)
* [YouTube video demonstrating EP9 under Wine 1.8-rc2 (patched)](https://www.youtube.com/watch?v=h9rZPdNLd6I&t=37s)
* [Lutris](https://lutris.net/games/the-sims-2)
* [Lutris - GitHub Wiki](https://github.com/lutris/lutris/wiki/Game:-The-Sims-2) - covers Origin version.
* [WineHQ AppDB - The Sims 2.x](https://appdb.winehq.org/objectManager.php?sClass=version&iId=2633)


## License

Wine is distributed under the [GNU Lesser General Public License 2.1](https://source.winehq.org/source/LICENSE).
