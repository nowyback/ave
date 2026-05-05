# Albedo Visual Engine (AVE) - Shader Integration Guide

This tutorial explains how to connect your shader pack to AVE to access data-driven block attributes for PBR, Path Tracing, and advanced lighting.

## 1. The Data Bridge
AVE uploads a "Block Attribute Map" directly to the GPU in a **Shader Storage Buffer Object (SSBO)**.
- **Binding Point**: `0`
- **Indexing**: Uses Minecraft's internal Block Registry IDs.

## 2. GLSL Implementation

To support **OpenGL 3.3 all the way to 4.3+**, your shader should include the following header:

```glsl
// Use at least version 330
#version 330 compatibility

// Required for SSBO support on OpenGL < 4.3
#extension GL_ARB_shader_storage_buffer_object : enable

// Define the AVE interface
layout(std430, binding = 0) readonly buffer BlockAttributes {
    uint attributes[];  // Packed: R=Scattering, G=Reflectivity, B=Roughness, A=Metallic
};

// Data structure for your lighting calculations
struct AVEData {
    float scattering;
    float reflectivity;
    float roughness;
    float metallic;
};

// Helper to fetch and normalize data
AVEData fetchAVEData(uint id) {
    uint p = attributes[id];
    return AVEData(
        float(p & 0xFFu) / 255.0,
        float((p >> 8u) & 0xFFu) / 255.0,
        float((p >> 16u) & 0xFFu) / 255.0,
        float((p >> 24u) & 0xFFu) / 255.0
    );
}
```

## 3. Recommended Workflow

### Step A: G-Buffer Storage
Store the `blockID` in a G-buffer texture during the main rendering pass. Most shader packs use a hidden texture (e.g., `colortex7`) for ID storage.

### Step B: Lighting Pass
In your lighting or path tracing pass:
1. Sample your ID texture to get the `blockID` for the current pixel.
2. Call `fetchAVEData(blockID)`.
3. Use the returned values in your PBR or Scattering equations.

## 4. Why use AVE?
- **Zero Config**: Users don't need to manually write `block.properties` for your shader.
- **Dynamic**: Changes to AVE's data-driven JSONs are reflected instantly in your shader.
- **Performance**: Fetching from an SSBO is significantly faster than sampling large LUT textures.

---
© 2026 CHROMSHOT Studio. All Rights Reserved.
