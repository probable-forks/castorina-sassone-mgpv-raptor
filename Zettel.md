## Patches & Hacks

### Wayland Support

My development environment uses *Wayland* and SDL 2 creates a Wayland window by default. Instead of reconfiguring the SDL to create an X11 window (under Xwayland) it suffices to change a single pre-processor in `gpu_device.hpp`, per chapter:

- `#define VK_USE_PLATFORM_WAYLAND_KHR`
- ~~`#define VK_USE_PLATFORM_XLIB_KHR`~~

### Path to `spirv.h`

The unified `spirv.h` header is present on my *Gentoo* dev. environment but is not sourced from `spirv_cross`, necessitating a change in `spirv_parser.hpp` for later chapters:

- `#include <spirv/unified1/spirv.h>`
- ~~`#include <spirv_cross/spirv.h>`~~



## Buiding & Running

Configure an out-of-tree build with *CMake*:

```sh
# (Several deprecation warnings are printed by CMake!)
cmake -B build -DCMAKE_BUILD_TYPE=Debug
```

Build and run each chapter, given the path to a `.gltf` model:

1. Chapter 1:

   ```sh
   mgpv_chapter=1; \
   mgpv_model_gltf=~/archive/samples/khronos-gltf/Sponza/glTF/Sponza.gltf; \
   cmake --build build --target Chapter${mgpv_chapter} -- -j 8 && \
   VULKAN_SDK=/usr ./build/source/chapter${mgpv_chapter}/Chapter${mgpv_chapter} "${mgpv_model_gltf}"
   ```

2. Chapter 2:

   ```
   mgpv_chapter=2; \
   mgpv_model_gltf=~/archive/samples/khronos-gltf/Sponza/glTF/Sponza.gltf; \
   cmake --build build --target Chapter${mgpv_chapter} -- -j 8 && \
   VULKAN_SDK=/usr ./build/source/chapter${mgpv_chapter}/Chapter${mgpv_chapter} "${mgpv_model_gltf}"
   ```

3. Chapter 3:

   ```
   mgpv_chapter=3; \
   mgpv_model_gltf=~/archive/samples/khronos-gltf/Sponza/glTF/Sponza.gltf; \
   cmake --build build --target Chapter${mgpv_chapter} -- -j 8 && \
   VULKAN_SDK=/usr ./build/source/chapter${mgpv_chapter}/Chapter${mgpv_chapter} "${mgpv_model_gltf}"
   ```

Notes:

- setting `VULKAN_SDK` is necessary for `glslangValidator` to be correctly found and executed (in `gpu_device.cpp`) which occurs at runtime for shader compilation – a pattern of which I am not fond!



# Models and Sample Assets

Models downloaded from:
- https://github.com/KhronosGroup/glTF-Sample-Assets
- https://github.com/KhronosGroup/glTF-Sample-Models


More Sample Assets:

- https://polyhaven.com/models
