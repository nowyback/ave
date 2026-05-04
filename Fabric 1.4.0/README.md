# **Albedo Visual Engine**

Albedo Visual Engine (AVE) is a high-performance, data-driven GPU rendering bridge for Minecraft. Built for the next generation of shaders and mods, AVE uses SSBO (Shader Storage Buffer Objects) to offload complex block data directly to the GPU, allowing for block, world or biome-specific visual effects and lighting that standard rendering engines can't handle.

AVE is designed for the next-gen shaders like OSMIUM shaders and other advanced shader packs that have data driven rendering.

## **Requirements**:
- Minecraft 1.20.0 or higher
- OpenGL 3.30 or higher
- Modern graphics card with support for SSBO
- Shader Loader (for example, Iris or Oculus)
- Modloader API


<details>
<summary>Open GL Compatibility</summary>

| Open GL Version | Features                                                                    |
|-----------------|-----------------------------------------------------------------------------|
|     <3.30       | Not supported. Minecraft will start, but AVE will not work.                 |
|      3.30       | Supported. UBO will be used instead of SSBO. May cause performance issues.  |
|      4.00       | Supported. SSBO with ARB extension will be used.                            |
|      4.30+      | Supported. SSBO will be used.                                               |


</details>

## **Notice**

Please remember this project is in early development and will most likely contain bugs or other issues. If you find any please DM me on Discord (nowyback) or create an issue on [GitHub](https://github.com/nowyback/ave/issues). Also please remember to download the right version for your Minecraft and mod loader version. The latest version can be found on the [releases page](https://github.com/nowyback/ave/releases).

## **API Library**

Coming Soon

## **Support**

- Patreon: [nowyback](https://www.patreon.com/c/nowyback)
- Youtube: [nowyback](https://www.youtube.com/@nowyback)