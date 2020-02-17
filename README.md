# The Sims 2 under Wine

### What's this?

This repository contains instructions and patches to get The Sims 2 working under
the [Wine Compatibility Layer](https://www.winehq.org/).

The Sims 2 is a classic, but is designed to run on Windows. It has been historically ported to Mac as
[The Sims™ 2: Super Collection](https://www.aspyr.com/games/the-sims-2-super-collection) but
is limited to 6 expansions, 3 stuff packs and hasn't seen any updates in 3+ years.

It's possible to play The Sims 2 almost flawlessly by either modifying your prefix
or using a patched build of Wine on Linux, and Mac too.

### Implementations & Instructions

There are a few ways to play The Sims 2.

| Implementation            | Works?       | Instructions
| ------------------------- | ------------ | ------------------
| Wine 5.2 (and later) | Maybe, likely to crash with **Direct3D returned an error: D3DERR_INVALIDCALL!**. | 
| [wine-staging](https://github.com/wine-staging/wine-staging) | Partial, severe graphical glitches. |
| Wine 4.x (with patches) | Yes, with workarounds. | [Instructions](README-WineD3D.md)
| [DXVK](https://github.com/doitsujin/dxvk) | **Yes.** Recommended for Vulkan-enabled graphics cards. | [Instructions](README-D9VK.md)
| [Lutris](https://lutris.net/games/the-sims-2/) | Yes.
| Proton 4.11               | No, crashes with **Direct3D returned an error: D3DERR_INVALIDCALL!**. |

The easiest to setup and provides the best compatibility is [DXVK](README-D9VK.md),
providing your graphics driver and hardware supports Vulkan.

As of 5.2, `wine` added the stub interface.

> d3d9: Return a stub interface from Direct3DShaderValidatorCreate9().


## Don't forget...

When testing The Sims 2 for the purposes of sending test reports to AppDB. Please only do 
so if this is against an unmodified version of Wine or `wine-staging`. Patched versions,
Lutris or DXVK versions are not accepted.

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
