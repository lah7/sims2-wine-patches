# The Sims 2 under Wine

### What's this?

This repository contains patches and instructions to get The Sims 2 working under
the [Wine Compatibility Layer](https://www.winehq.org/).

The Sims 2 is a classic, but is designed to run on Windows. It has been historically ported to Mac as
[The Sims™ 2: Super Collection](https://www.aspyr.com/games/the-sims-2-super-collection) but
is limited to 6 expansions, 3 stuff packs and hasn't seen any updates in 3+ years.

It's possible to play The Sims 2 almost flawlessly by either modifying your prefix
or using a patched build of Wine on Linux, and Mac too.

### Implementations & Instructions

There are a few ways to play The Sims 2.

| Implementation            | Works?
| ------------------------- | -----------
| Wine (with no modifications) | No, crashes with **Direct3D returned an error: D3DERR_INVALIDCALL!**.
| [wine-staging](https://github.com/wine-staging/wine-staging) | Partial, severe graphical glitches.
| Wine (with patches) | Yes, with workarounds.
| [D9VK](https://git.froggi.es/joshua/d9vk) | **Yes, recommended** for Vulkan-enabled graphics cards.
| [Lutris](https://lutris.net/games/the-sims-2/) | Yes.
| Proton 4.11               | No, crashes with **Direct3D returned an error: D3DERR_INVALIDCALL!**.

The easiest to setup and provides the best compatibility is [D9VK](README-D9VK.md),
providing your graphics driver and hardware supports Vulkan.

* [Instructions for D9VK](README-D9VK.md)
* [Instructions for WineD3D](README-WineD3D.md)

As of 4.20, `wine-staging` added a patch for the missing
[Direct3DShaderValidatorCreate9](https://github.com/wine-staging/wine-staging/tree/master/patches/d3d9-Direct3DShaderValidatorCreate9)
implementation, although this still causes the 'red eagle pose'.


## Don't forget...

Since The Sims 2 doesn't work with an unmodified version of Wine, but does start
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
