# SHIELD_AI — 3D Asset Catalog

Four low-poly assets for the project's educational Unity simulation. Each asset has an editable Blender source, an FBX export, and a PNG preview.

The visual style uses simple gray materials with blue accents. All models are exterior visuals without flight behavior. Three assets also have specification JSON files.

## Inventory

Dimensions are reported **width × length × height**, in metres. Counts and measurements below come from the asset-generation reports; the source files were not independently measured for this README.

| Preview | Asset | Dimensions (m) | Triangles | Animated parts | Files |
|---|---|---|---:|---|---|
| <img src="Radar_01/Radar_01_preview.png" alt="Radar_01 preview" width="180"> | [Radar_01](#radar_01) | Height: 3.60; width/length not reported | 1,856 | Rotating mount and dish | [Blend](Radar_01/Radar_01.blend) · [FBX](Radar_01/Radar_01.fbx) · [PNG](Radar_01/Radar_01_preview.png) |
| <img src="FPV_Quadcopter_01/FPV_Quadcopter_01_preview.png" alt="FPV_Quadcopter_01 preview" width="180"> | [FPV_Quadcopter_01](#fpv_quadcopter_01) | 0.634 × 0.372 × 0.290 | 972 | Four propellers | [Blend](FPV_Quadcopter_01/FPV_Quadcopter_01.blend) · [FBX](FPV_Quadcopter_01/FPV_Quadcopter_01.fbx) · [PNG](FPV_Quadcopter_01/FPV_Quadcopter_01_preview.png) · [Specs](FPV_Quadcopter_01/FPV_Quadcopter_01_specs.json) |
| <img src="Shahed_Style_Drone_01/Shahed_Style_Drone_01_preview.png" alt="Shahed_Style_Drone_01 preview" width="180"> | [Shahed_Style_Drone_01](#shahed_style_drone_01) | 2.400 × 1.800 × 0.345 | 256 | Rear propeller | [Blend](Shahed_Style_Drone_01/Shahed_Style_Drone_01.blend) · [FBX](Shahed_Style_Drone_01/Shahed_Style_Drone_01.fbx) · [PNG](Shahed_Style_Drone_01/Shahed_Style_Drone_01_preview.png) · [Specs](Shahed_Style_Drone_01/Shahed_Style_Drone_01_specs.json) |
| <img src="Generic_Missile_01/Generic_Missile_01_preview.png" alt="Generic_Missile_01 preview" width="180"> | [Generic_Missile_01](#generic_missile_01) | 0.700 × 2.290 × 0.700 | 420 | No dedicated animated part reported | [Blend](Generic_Missile_01/Generic_Missile_01.blend) · [FBX](Generic_Missile_01/Generic_Missile_01.fbx) · [PNG](Generic_Missile_01/Generic_Missile_01_preview.png) · [Specs](Generic_Missile_01/Generic_Missile_01_specs.json) |
| — | **Total** | — | **3,504** | — | — |

## Radar_01

Fictional radar with a ground-level root and separate base, rotating mount, and dish. The reported height is 3.60 metres.

- [Blender source](Radar_01/Radar_01.blend)
- [Unity FBX export](Radar_01/Radar_01.fbx)
- [Preview PNG](Radar_01/Radar_01_preview.png)

No radar specification JSON appears in the supplied directory listing.

**Animation:** rotate the mount about its local Unity Y axis after checking the imported hierarchy. The dish should follow the mount while the base stays fixed.

**Visual review:** the preview appears to show mounting pieces near the lower front of the dish. Inspect this area in Blender before deciding whether to revise it.

## FPV_Quadcopter_01

Compact, stylized quadcopter with four arms, motors, separate propellers, a front camera, and a battery block.

- [Blender source](FPV_Quadcopter_01/FPV_Quadcopter_01.blend)
- [Unity FBX export](FPV_Quadcopter_01/FPV_Quadcopter_01.fbx)
- [Preview PNG](FPV_Quadcopter_01/FPV_Quadcopter_01_preview.png)
- [Specifications JSON](FPV_Quadcopter_01/FPV_Quadcopter_01_specs.json)

**Animation:** each propeller has a reported motor-centered pivot. Inspect its imported local axes before choosing the spin axis.

## Shahed_Style_Drone_01

Fictional delta-wing exterior inspired by a recognizable silhouette, with a central body, wingtip fins, and a separate rear propeller. The dimensions are visual design choices, not validated real-world specifications.

- [Blender source](Shahed_Style_Drone_01/Shahed_Style_Drone_01.blend)
- [Unity FBX export](Shahed_Style_Drone_01/Shahed_Style_Drone_01.fbx)
- [Preview PNG](Shahed_Style_Drone_01/Shahed_Style_Drone_01_preview.png)
- [Specifications JSON](Shahed_Style_Drone_01/Shahed_Style_Drone_01_specs.json)

**Animation:** rotate only the rear propeller for the visual spin effect. Inspect its local axis after import.

## Generic_Missile_01

Fictional cylindrical exterior with a pointed nose, tail fins, and a rear nozzle. It contains no internal weapon components or guidance system.

- [Blender source](Generic_Missile_01/Generic_Missile_01.blend)
- [Unity FBX export](Generic_Missile_01/Generic_Missile_01.fbx)
- [Preview PNG](Generic_Missile_01/Generic_Missile_01_preview.png)
- [Specifications JSON](Generic_Missile_01/Generic_Missile_01_specs.json)

Movement and visual trails are separate Unity features; they are not included in this model.

## File conventions

| File | Purpose |
|---|---|
| `<AssetName>.blend` | Editable, asset-only Blender source |
| `<AssetName>.fbx` | Exchange model for Unity |
| `<AssetName>_preview.png` | Rendered preview used by these READMEs |
| `<AssetName>_specs.json` | Additional metadata where available |

The previews and file links are relative to this `3D_assets/README.md`. Keep each asset's files together and preserve filename spelling and capitalization for GitHub compatibility.

## Unity import checklist

1. Copy the FBX into `Assets/Models/<AssetName>/` in the Unity project.
2. Place the model in a test scene and inspect it from several angles.
3. Confirm metre scale and the reported **+Z forward / +Y up** orientation.
4. Check materials in the project's rendering pipeline.
5. Inspect child objects and test propeller or mount rotation where applicable.
6. Create a prefab after verification.

The creation reports state that the FBXs passed re-import checks for transforms, hierarchy, materials, and relevant pivots. They also report checks of normals and closed geometry. Repeat the relevant checks in Unity before using the assets in a larger scene.

## Working on more assets

- Create each new asset in a separate Blender scene or file.
- Use the same simple material palette and clear object names.
- Keep moving parts separate with appropriate pivots.
- Save the Blender source before exporting.
- Save a preview with the same filename pattern.
- Check for existing files before overwriting; use numbered versions for revisions.
- Update this catalog when a new asset is added.

Read the [Blender MCP Windows guide](../Blender_MCP_Windows_Guide.md) for connection setup and the restart checklist.

[Back to project README](../README.md) · [Project roadmap](../SHIELD_AI_ROADMAP.md)
