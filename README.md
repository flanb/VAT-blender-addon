# VAT Blender Addon

This Blender plugin generates Vertex Animation Textures (VAT) from animated meshes. It is designed to simplify the export of complex animations to Three.js or other, using textures to store vertex movements.

## Installation
1. Download `VAT.py`.
2. In Blender, go to **Edit > Preferences > Add-ons**.
3. Click **Install from Disk...** and select the `VAT.py` file.
4. Enable the addon in the list.

## Features
//TODO

## Supported Modifiers

The following Blender modifiers are supported by the VAT addon:

| Modifier Name     |
|-------------------|
| ARMATURE          |
| CAST              |
| CLOTH             |
| CURVE             |
| DISPLACE          |
| HOOK              |
| LAPLACIANDEFORM   |
| LATTICE           |
| MESH_DEFORM       |
| SHRINKWRAP        |
| SIMPLE_DEFORM     |
| SMOOTH            |
| CORRECTIVE_SMOOTH |
| LAPLACIANSMOOTH   |
| SURFACE_DEFORM    |
| WARP              |
| WAVE              |
| PARTICLE_SYSTEM   |
| EXPLODE           |

**Warning:** If a modifier changes the number of vertices during the animation (such as `PARTICLE_SYSTEM` or `EXPLODE`), the plugin will not work correctly.

For `PARTICLE_SYSTEM`, it is recommended to set both the Emission Frame Start and End to 1 in the panel, and to start the animation at frame 1. This ensures the vertex count remains constant throughout the animation.

## Usage
1. Select an animated object in your Blender scene.
2. Bake the animation:
    - Go to the **Cache** section in the modifier panel.
    - Click **Bake All Dynamics** to bake the animation.
3. Access the addon panel (On the right near "Item" or "Tool" tab).
4. Configure the desired options (wrap mode, Y-flip, etc.).
5. Start the VAT texture generation.
6. The plugin will generate a new mesh `export_mesh` with a new uv set `vertex_anim`, and textures `positions` and `normals`.

| Output        | Description                                                             | Export Format & Settings                                                                                       | Example Image                                                                                                         |
|---------------|-------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| `export_mesh` | Mesh with new UV set `vertex_anim`. Can be exported for use in engines. | .glb or other mesh formats                                                                                     | <img width="157" alt="image" src="https://github.com/user-attachments/assets/aa5efc2a-5393-4b7b-86cd-af817c323b1e" /> |
| `positions`   | Vertex position animation texture.                                      | If `Normalize` is **false**: export as **OpenEXR**, `Color` `RGB`, `Color Depth` `Half` or `Full`, `Non-Color` | <img width="200" alt="image" src="https://github.com/user-attachments/assets/54134b64-8436-440f-ad69-8ec01a882b07" /> |
|               |                                                                         | If `Normalize` is **true**: export as **PNG**, same settings as above                                          | <img width="193" alt="image" src="https://github.com/user-attachments/assets/d2aa6067-f177-4387-acf0-9af945ceaf3f" /> |
| `normals`     | Vertex normal animation texture.                                        | **PNG** or other supported formats                                                                             | <img width="193" alt="image" src="https://github.com/user-attachments/assets/d2aa6067-f177-4387-acf0-9af945ceaf3f" /> |

## Usage for threejs
//TODO

Blender uses Z as the up axis, while in Three.js the up axis is Y. Therefore, when sampling the position texture in GLSL, you should use `texturePos.xzy` to correctly map the axes.
