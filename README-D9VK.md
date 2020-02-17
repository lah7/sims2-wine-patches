# How to play The Sims 2 under DXVK

DXVK is a **Direct3D 9/10/11 to Vulkan** compatibilty layer.
This provides the best compatibilty with newer and old versions of the game as
it implements vertex shaders and makes better use of the hardware.

https://github.com/doitsujin/dxvk


## Vulkan Prerequisites

Make sure you have a Vulkan-enabled graphics card with compatible drivers,
as well as Vulkan packages that provide libraries for 32-bit applications.


## Installation

1. Create a new prefix for The Sims 2 and run through installation as normal.

1. Download the latest "passed" build of DXVK:

    https://github.com/doitsujin/dxvk/releases

1. Extract the ZIP and install DXVK into the Wine prefix:

       export WINEPREFIX=/path/to/sims2_prefix
       dxvk-*/setup_dxvk.sh install

    DXVK writes a set of DLLs that overlay WineD3D, allowing this work to with
    whichever version of Wine you have installed.

1. Start The Sims 2!


### Not starting?

If you see any of these errors:

```
0009:err:vulkan:wine_vk_init Failed to load libvulkan.so.1.
0009:err:vulkan:wine_vk_init Failed to load Wine graphics driver supporting Vulkan..
0009:err:module:find_forwarded_export module not found for forward 'winevulkan.wine_vkGetInstanceProcAddr' used by L"C:\\windows\\system32\\vulkan-1.dll"
```

It's likely your system is missing the necessary Vulkan packages.
Use your package manager to install them. 32-bit libraries may be required too.

If the game still fails to load, it's possible your graphics card or graphics
driver does not support the Vulkan API.


## Known Issues

There may be bugs! See here for problems that may occur under D9VK:

https://github.com/Joshua-Ashton/d9vk/issues/242


### NVIDIA: Black boxes for "High" shadows

This also happens under the NVIDIA driver on Windows.

![Black Shadow Bug](.github/black-shadow-bug.jpg)

This can be fixed by installing the [Sim Shadow Fix](http://modthesims.info/d/569585/sim-shadow-fix-updated-2-jan-16.html) (v0.4) mod.
Extract this into `My Documents/EA Games/The Sims 2/Downloads`.
