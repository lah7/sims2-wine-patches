# How to play The Sims 2 under D9VK

D9VK is a **Direct3D 9 to Vulkan** compatibilty layer based on DXVK's codebase.
This provides the best compatibilty with newer and old versions of the game as
it implements vertex shaders and makes better use of the hardware.

https://git.froggi.es/joshua/d9vk


## Vulkan Prerequisites

Make sure you have a Vulkan-enabled graphics card with compatible drivers,
as well as Vulkan packages that provide libraries for 32-bit applications.


## Steps

1. Create a new prefix for The Sims 2 and run through installation as normal.

1. Download the latest "passed" build of D9VK:

    https://git.froggi.es/joshua/d9vk/-/jobs

1. Extract the ZIP and install D9VK into the Wine prefix:

       export WINEPREFIX=/path/to/sims2_prefix
       build/dxvk-release/setup_dxvk.sh install

    D9VK is a set of DLLs that are overridden by Wine, therefore, D9VK works with
    any new (and system installed) version of Wine.

1. Start The Sims 2!


## Problems?

### Missing Vulkan libraries

If you see any of these errors:

```
0009:err:vulkan:wine_vk_init Failed to load libvulkan.so.1.
0009:err:vulkan:wine_vk_init Failed to load Wine graphics driver supporting Vulkan..
0009:err:module:find_forwarded_export module not found for forward 'winevulkan.wine_vkGetInstanceProcAddr' used by L"C:\\windows\\system32\\vulkan-1.dll"
```

It's likely your system is missing the necessary Vulkan packages.
Use your package manager to install them, and perhaps their 32-bit libraries too.



### NVIDIA: Black boxes for "High" shadows

This also happens under the NVIDIA driver on Windows.

![Black Shadow Bug](.github/black-shadow-bug.jpg)

This can be fixed by installing the [Sim Shadow Fix](http://modthesims.info/d/569585/sim-shadow-fix-updated-2-jan-16.html) (v0.4) mod.
Extract this into `My Documents/EA Games/The Sims 2/Downloads`.
