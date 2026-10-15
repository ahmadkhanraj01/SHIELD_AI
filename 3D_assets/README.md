# SHIELD_AI — 3D Asset Catalog

Low-poly assets for the project's educational Unity simulation: four scenario assets plus a city environment kit of buildings, road tiles, and street props. Each asset has an editable Blender source, an FBX export, and a PNG preview.

The visual style uses simple gray materials with blue accents. All models are exterior visuals without flight behavior. Three scenario assets also have specification JSON files.

| Group | Assets | Triangles |
|---|---:|---:|
| [Scenario assets](#inventory) | 4 | 3,504 |
| [Buildings and ground](#buildings-and-ground) | 7 | 7,112 |
| [Road tiles](#road-tiles) | 4 | 1,860 |
| [Street props](#street-props) | 6 | 1,102 |
| **Total** | **21** | **13,578** |

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

## City environment kit

Buildings, road tiles, and props for the defended city scene. Dimensions and triangle counts below were measured from the generated meshes in Blender. Unlike the scenario assets, these FBXs have **not yet been re-imported or checked in Unity**.

### Buildings and ground

The `_02` buildings are detailed revisions of the `_01` blockouts. Prefer `_02` for the scene; keep `_01` as lightweight stand-ins for distant or repeated buildings.

| Preview | Asset | Dimensions (m) | Triangles | Description | Files |
|---|---|---|---:|---|---|
| <img src="Building_Small_02/Building_Small_02_preview.png" alt="Building_Small_02 preview" width="180"> | Building_Small_02 | 7.60 × 7.70 × 11.70 | 1,176 | Three-storey residential building with window sills, floor ledges, front balconies, entrance canopy, rooftop water tank and AC units | [Blend](Building_Small_02/Building_Small_02.blend) · [FBX](Building_Small_02/Building_Small_02.fbx) · [PNG](Building_Small_02/Building_Small_02_preview.png) |
| <img src="Building_Tall_02/Building_Tall_02_preview.png" alt="Building_Tall_02 preview" width="180"> | Building_Tall_02 | 11.60 × 13.50 × 39.85 | 3,536 | Office tower with a glass-fronted podium, entrance canopy, eight window floors, blue corner fins, glazed crown, and antenna | [Blend](Building_Tall_02/Building_Tall_02.blend) · [FBX](Building_Tall_02/Building_Tall_02.fbx) · [PNG](Building_Tall_02/Building_Tall_02_preview.png) |
| <img src="Building_Block_02/Building_Block_02_preview.png" alt="Building_Block_02 preview" width="180"> | Building_Block_02 | 18.60 × 11.45 × 16.20 | 2,124 | Wide four-storey block with ground-floor shopfronts and blue awnings, pilasters, rooftop stair housing, AC units, and vents | [Blend](Building_Block_02/Building_Block_02.blend) · [FBX](Building_Block_02/Building_Block_02.fbx) · [PNG](Building_Block_02/Building_Block_02_preview.png) |
| <img src="Building_Small_01/Building_Small_01_preview.png" alt="Building_Small_01 preview" width="180"> | Building_Small_01 | 6.40 × 6.40 × 8.40 | 60 | Simple blockout: body, roof slab, window bands, door | [Blend](Building_Small_01/Building_Small_01.blend) · [FBX](Building_Small_01/Building_Small_01.fbx) · [PNG](Building_Small_01/Building_Small_01_preview.png) |
| <img src="Building_Tall_01/Building_Tall_01_preview.png" alt="Building_Tall_01 preview" width="180"> | Building_Tall_01 | 8.00 × 8.05 × 28.40 | 108 | Simple blockout: base, tower, window bands, antenna | [Blend](Building_Tall_01/Building_Tall_01.blend) · [FBX](Building_Tall_01/Building_Tall_01.fbx) · [PNG](Building_Tall_01/Building_Tall_01_preview.png) |
| <img src="Building_Block_01/Building_Block_01_preview.png" alt="Building_Block_01 preview" width="180"> | Building_Block_01 | 16.40 × 8.40 × 13.60 | 72 | Simple blockout: wide body, roof slab, window bands, vent | [Blend](Building_Block_01/Building_Block_01.blend) · [FBX](Building_Block_01/Building_Block_01.fbx) · [PNG](Building_Block_01/Building_Block_01_preview.png) |
| <img src="Ground_Tile_01/Ground_Tile_01_preview.png" alt="Ground_Tile_01 preview" width="180"> | Ground_Tile_01 | 20.00 × 20.00 × 0.23 | 36 | Flat 20 m slab with a plain road strip; superseded by the road tiles below | [Blend](Ground_Tile_01/Ground_Tile_01.blend) · [FBX](Ground_Tile_01/Ground_Tile_01.fbx) · [PNG](Ground_Tile_01/Ground_Tile_01_preview.png) |

### Road tiles

Every tile is **20 × 20 m** with its origin at the tile centre and the road surface at height 0. Each has a 10 m two-lane road and 5 m raised sidewalks with curbs. Place tiles on a 20 m grid and rotate them in 90° steps; lane dashes repeat every 4 m, so markings continue across tile edges.

| Preview | Asset | Dimensions (m) | Triangles | Description | Files |
|---|---|---|---:|---|---|
| <img src="Road_Straight_01/Road_Straight_01_preview.png" alt="Road_Straight_01 preview" width="180"> | Road_Straight_01 | 20.00 × 20.00 × 0.37 | 288 | Straight road with dashed centre line and edge lines | [Blend](Road_Straight_01/Road_Straight_01.blend) · [FBX](Road_Straight_01/Road_Straight_01.fbx) · [PNG](Road_Straight_01/Road_Straight_01_preview.png) |
| <img src="Road_Cross_01/Road_Cross_01_preview.png" alt="Road_Cross_01 preview" width="180"> | Road_Cross_01 | 20.00 × 20.00 × 0.37 | 684 | Four-way crossroads with crosswalks on every arm | [Blend](Road_Cross_01/Road_Cross_01.blend) · [FBX](Road_Cross_01/Road_Cross_01.fbx) · [PNG](Road_Cross_01/Road_Cross_01_preview.png) |
| <img src="Road_T_01/Road_T_01_preview.png" alt="Road_T_01 preview" width="180"> | Road_T_01 | 20.00 × 20.00 × 0.37 | 588 | T-junction with crosswalks | [Blend](Road_T_01/Road_T_01.blend) · [FBX](Road_T_01/Road_T_01.fbx) · [PNG](Road_T_01/Road_T_01_preview.png) |
| <img src="Road_Corner_01/Road_Corner_01_preview.png" alt="Road_Corner_01 preview" width="180"> | Road_Corner_01 | 20.00 × 20.00 × 0.37 | 300 | 90° turn | [Blend](Road_Corner_01/Road_Corner_01.blend) · [FBX](Road_Corner_01/Road_Corner_01.fbx) · [PNG](Road_Corner_01/Road_Corner_01_preview.png) |

### Street props

| Preview | Asset | Dimensions (m) | Triangles | Description | Files |
|---|---|---|---:|---|---|
| <img src="Streetlight_01/Streetlight_01_preview.png" alt="Streetlight_01 preview" width="180"> | Streetlight_01 | 2.29 × 0.40 × 7.40 | 120 | Tapered pole with an arm reaching 1.75 m along +X; place on a sidewalk with the arm over the road | [Blend](Streetlight_01/Streetlight_01.blend) · [FBX](Streetlight_01/Streetlight_01.fbx) · [PNG](Streetlight_01/Streetlight_01_preview.png) |
| <img src="Tree_01/Tree_01_preview.png" alt="Tree_01 preview" width="180"> | Tree_01 | 3.56 × 2.78 × 5.04 | 88 | Round deciduous tree | [Blend](Tree_01/Tree_01.blend) · [FBX](Tree_01/Tree_01.fbx) · [PNG](Tree_01/Tree_01_preview.png) |
| <img src="Tree_02/Tree_02_preview.png" alt="Tree_02 preview" width="180"> | Tree_02 | 2.85 × 3.00 × 5.50 | 82 | Three-tier pine tree | [Blend](Tree_02/Tree_02.blend) · [FBX](Tree_02/Tree_02.fbx) · [PNG](Tree_02/Tree_02_preview.png) |
| <img src="Bench_01/Bench_01_preview.png" alt="Bench_01 preview" width="180"> | Bench_01 | 1.80 × 0.55 × 0.94 | 132 | Slatted park bench | [Blend](Bench_01/Bench_01.blend) · [FBX](Bench_01/Bench_01.fbx) · [PNG](Bench_01/Bench_01_preview.png) |
| <img src="Car_01/Car_01_preview.png" alt="Car_01 preview" width="180"> | Car_01 | 1.98 × 4.38 × 1.57 | 340 | Blue sedan, static (wheels are not separate objects) | [Blend](Car_01/Car_01.blend) · [FBX](Car_01/Car_01.fbx) · [PNG](Car_01/Car_01_preview.png) |
| <img src="Car_02/Car_02_preview.png" alt="Car_02 preview" width="180"> | Car_02 | 1.98 × 4.38 × 1.57 | 340 | White variant of Car_01 | [Blend](Car_02/Car_02.blend) · [FBX](Car_02/Car_02.fbx) · [PNG](Car_02/Car_02_preview.png) |

### Environment kit conventions

- **Origin:** buildings and props sit on the ground with the origin at their base centre; road tiles use the tile centre.
- **Facing:** entrances, car fronts, and headlights face Blender −Y. FBXs use the same **+Z forward / +Y up** export setting as the scenario assets; confirm the facing after import.
- **Hierarchy:** each asset is an empty root named after the asset, with one child mesh per material (for example `Building_Tall_02_Windows`). This keeps draw calls low and makes materials easy to swap in Unity.
- **Materials:** `SHIELD_LightGray` (walls, sidewalks), `SHIELD_DarkGray` (trim, curbs, wheels), `SHIELD_Glass` (windows), `SHIELD_Blue` (accents), `SHIELD_Asphalt`, `SHIELD_White` (road markings), `SHIELD_Foliage`, and `SHIELD_Bark`. The last four extend the gray-and-blue palette for the city.
- **Previews:** rendered with a temporary ground plane, sun, and sky that are not part of the exported model.

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
