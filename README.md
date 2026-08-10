# The Last Light
**GDT-225: Advanced Graphics Programming**
Grand Canyon University

---

## Project Overview

The Last Light is a narrative atmospheric scene built in Unreal Engine 5 as the final project for GDT-225. The player takes the role of a solitary lighthouse keeper working through a violent coastal storm to keep an aging beacon alight for a ship struggling somewhere in the dark. The player never leaves the lighthouse and never meets the crew. The only connection between keeper and ship is the rhythm and reach of the light itself.

The scene focuses on atmosphere and tension driven by a single resource mechanic: fuel. As the storm intensifies, the player must manage the lamp's fuel supply to keep the light burning through the night. Shader and lighting work across all seven course weeks drives the emotional arc of the scene, since there is no dialogue to rely on.

---

## Tools and Environment

| Tool | Purpose |
|------|---------|
| Unreal Engine 5.6.1 | Scene and shader development |
| GitHub | Version control and project delivery |
| Visual Studio Code | Blueprint and configuration editing |
| GIMP | Texture editing |

---

## Week 1 - Project Setup

1. Opened Epic Games Launcher and launched Unreal Engine 5.6.1.
2. Selected the **Games > Blank** template with the following settings:
   - Blueprint (not C++)
   - No Starter Content
   - Quality: Maximum
   - Target Platform: Desktop
3. Named the project `TheLastLight` and created it.
4. Switched the renderer from DirectX 12 to DirectX 11 via `Config/DefaultEngine.ini` to resolve a GPU driver stability issue.
5. Opened the default Open World level and saved it as `TheLastLight_Main` inside the Content folder.
6. Added basic starter assets via the Place Actors panel:
   - Cube (Static Mesh)
   - Cylinder (Static Mesh)
   - Both organized under a `StarterAssets` folder in the Outliner.
7. Saved the level with Ctrl+S.

---

## Week 2 - Basic Shader Development

### Shader Created: M_LampGlow

A basic lamp glow material was created in the UE5 Material Editor to represent the lighthouse beacon light. This shader demonstrates color control, emissive glow, and UV transformation effects.

### Node Graph Breakdown

| Node | Purpose |
|------|---------|
| Constant3Vector (R:1.0, G:0.4, B:0.0) | Sets the amber/orange lamp color |
| Texture Coordinate | Provides UV mapping data for the surface |
| Panner (Speed X: 0.1) | Shifts the UV coordinates to create a slow scrolling transformation effect |
| Texture Sample (T_Perlin_Mask) | Applies a Perlin noise texture to add organic variation to the glow |
| Multiply | Combines the color with the noise texture |
| Base Color | Receives the final color output |
| Emissive Color | Receives the same output to make the material emit light |

### How It Works

The Constant3Vector defines the warm amber color of the lamp. That color is multiplied against a Perlin noise texture that is being panned slowly across the surface using a Texture Coordinate and Panner node setup. The result is connected to both the Base Color and Emissive Color inputs, so the material both shows the color and emits light. The scrolling noise creates a subtle, organic variation across the surface that simulates the flicker and movement of a real lamp flame.

### Applied To

The M_LampGlow material was applied to the Cube mesh in the TheLastLight_Main level as a stand-in for the lighthouse lamp beacon.

---

## Version Control Log

| Week | Commit Description |
|------|-------------------|
| Week 1 | Initial project setup, starter assets, README |
| Week 2 | Added M_LampGlow shader with color and UV transformation |

---

## Repository Contents

```
GDT-225-TheLastLight/
    Config/         # Engine and project configuration files
    Content/        # UE5 level and asset files including M_LampGlow material
    .gitignore      # Excludes generated UE5 folders from version control
    TheLastLight.uproject
    README.md
```

---

## How to Clone and Open the Project

1. Clone the repository:
   ```
   git clone https://github.com/JoeJeep/GDT-225-TheLastLight.git
   ```
2. Navigate to the project folder and right-click `TheLastLight.uproject`.
3. Select **Open with Unreal Engine** to launch the project.

> Note: Unreal Engine 5.6.1 is required. If you experience GPU crashes on launch, set `DefaultGraphicsRHI=DefaultGraphicsRHI_DX11` in `Config/DefaultEngine.ini`.

---

*Updated: Week 2 — Basic shader development, M_LampGlow material with color and UV transformation*

---

## Week 3 - Lighting and Materials

### Materials Created

#### M_LighthouseStone
A physically based material representing the rough stone exterior of the lighthouse base.

| Property | Value | Purpose |
|----------|-------|---------|
| Base Color | R:0.35, G:0.33, B:0.30 | Neutral grey stone tone |
| Metallic | 0.0 | Non-metal surface |
| Roughness | 0.85 | High roughness, no shine, simulates wet stone |
| Normal | Flat normal (R:0.5, G:0.5, B:1.0) | Surface detail baseline |

#### M_LampMetal
A physically based material representing the weathered iron lamp housing.

| Property | Value | Purpose |
|----------|-------|---------|
| Base Color | R:0.2, G:0.2, B:0.22 | Dark grey iron tone |
| Metallic | 1.0 | Full metal surface |
| Roughness | 0.4 | Moderate shine, weathered but not polished |
| Normal | Flat normal (R:0.5, G:0.5, B:1.0) | Surface detail baseline |

### Lighting Adjustments

| Light | Change | Purpose |
|-------|--------|---------|
| DirectionalLight | Color: cool blue-grey, Intensity: 2.0 lux | Simulates overcast stormy sky |
| PointLight (new) | Color: amber, Intensity: 500 cd | Simulates beacon casting warm light |

### Applied To
- M_LighthouseStone applied to Cylinder (lighthouse base stand-in)
- M_LampMetal applied to Cube (lamp housing stand-in)
- Point Light positioned above Cube to cast amber beacon glow

---

*Updated: Week 3 — PBR materials, normal maps, and lighting adjustments*

---

## Week 4 - UV Mapping and Procedural Effects

### UV Mapping Updates

#### M_LighthouseStone
Added UV mapping via Texture Coordinate node to control how the Perlin noise texture tiles across the surface.

| Node | Settings | Purpose |
|------|----------|---------|
| Texture Coordinate | UTiling: 4.0, VTiling: 4.0 | Tiles texture 4x across the stone surface |
| Texture Sample (T_Perlin_Mask) | Color sampler | Adds surface variation |
| Multiply | Color x Texture | Combines stone color with noise pattern |

#### M_LampMetal
Added the same UV mapping setup with tighter tiling to match the smoother metal surface.

| Node | Settings | Purpose |
|------|----------|---------|
| Texture Coordinate | UTiling: 2.0, VTiling: 2.0 | Tiles texture 2x across the metal surface |
| Texture Sample (T_Perlin_Mask) | Color sampler | Adds surface variation |
| Multiply | Color x Texture | Combines metal color with noise pattern |

### Procedural Effect: M_OceanWater

A fully procedural animated ocean water material built using two overlapping Panner nodes driving Perlin noise textures in opposite directions. No keyframes or pre-baked animation used.

| Node | Settings | Purpose |
|------|----------|---------|
| Texture Coordinate | Default | Provides UV input for both ripple layers |
| Panner 1 | Speed X: 0.05, Speed Y: 0.03 | First ripple layer moving diagonally |
| Panner 2 | Speed X: -0.03, Speed Y: 0.05 | Second ripple layer moving in opposite direction |
| Texture Sample 1 | T_Perlin_Mask | First animated noise layer |
| Texture Sample 2 | T_Perlin_Mask | Second animated noise layer |
| Add | Layer 1 + Layer 2 | Blends both ripple layers together |
| Metallic | 0.0 | Non-metal surface |
| Roughness | 0.1 | Highly reflective, glossy water surface |
| Normal | Add node output | Drives light reflection to simulate wave movement |

### Scene Updates

- Added **OceanSurface** plane (Scale X:50, Y:50) to the level, positioned at Z:50
- Applied M_OceanWater to OceanSurface
- Repositioned Cube and Cylinder to Z:50 to sit on the ocean surface
- OceanSurface added to StarterAssets folder in Outliner

---

*Updated: Week 4 — UV mapping and procedural animated ocean water effect*

---

## Week 5 - Advanced Shaders and Post-Processing

### Post-Processing Volume: PostProcessVolume_Main

A Post Process Volume set to Infinite Extent (Unbound) was added to apply cinematic effects across the entire level.

| Effect | Setting | Purpose |
|--------|---------|---------|
| Bloom | Intensity: 2.0, Threshold: 0.5, Method: Standard | Makes bright light sources like the beacon bleed light into surrounding area |
| Vignette | Intensity: 0.6 | Darkens screen edges to create enclosed stormy atmosphere |
| Chromatic Aberration | Intensity: 0.5 | Adds color fringing around screen edges simulating a wet or damaged lens |

### Stylized Shader: M_RimLight_Stone

A rim lighting material applied to the Cylinder (lighthouse base stand-in). Uses a Fresnel node to create an amber glow around the silhouette edges of the object, simulating the beacon light catching the lighthouse tower against the dark stormy sky.

| Node | Settings | Purpose |
|------|---------|---------|
| Constant3Vector | R:0.35, G:0.33, B:0.30 | Base stone color |
| Fresnel | Exponent: 3.0, Base Reflect Fraction: 0.0 | Calculates edge glow based on camera angle |
| Constant3Vector | R:1.0, G:0.5, B:0.1 | Amber rim light color matching beacon |
| Multiply | Fresnel x Amber color | Combines glow intensity with color |
| Emissive Color | Multiply output | Makes edges emit amber light |
| Metallic | 0.0 | Non-metal surface |
| Roughness | 0.85 | Rough stone surface |

### Before and After Comparison

Before Week 5 the scene had correct PBR materials and lighting but read as flat and uncinematic. The post-processing volume added bloom that makes the amber beacon glow bleed realistically into the surrounding water surface. The vignette darkens the screen edges pushing focus toward the center where the lighthouse objects sit. The chromatic aberration adds a subtle lens distortion that reinforces the stormy wet atmosphere. The rim light shader on the cylinder creates a visible silhouette glow that reads clearly as a lighthouse tower catching beacon light even with stand-in geometry.

---

*Updated: Week 5 — Post-processing effects and rim light stylized shader*

---

## Week 6 - Shader Optimization and Profiling

### Profiling Tools Used

- **Shader Complexity View** (Optimization Viewmodes in viewport)
- **Stat GPU** (console command)
- **Material Editor Stats panel** (instruction counts)

### Shader Complexity Results

All materials in the scene returned green in the Shader Complexity view, indicating efficient shader cost across the entire scene with no red or orange hotspots detected.

### Stat GPU Results

| Metric | Avg | Max |
|--------|-----|-----|
| Queue Total | 0.32ms | 14.41ms |
| Postprocessing | 3.76ms | 6.16ms |
| Editor Primitives | 2.03ms | 5.66ms |
| VolumetricCloud | 0.66ms | 1.02ms |
| Lights | 0.05ms | 0.06ms |

**Key finding:** Postprocessing at 3.76ms average is the highest cost item, driven by the active Bloom, Vignette, and Chromatic Aberration effects in PostProcessVolume_Main. All other costs are minimal. Lights are extremely cheap at 0.05ms despite the Point Light and Directional Light both being active.

### Material Instruction Counts

| Material | Instructions | Notes |
|----------|-------------|-------|
| M_LampGlow | 136 | Panner + noise + multiply setup |
| M_LighthouseStone | 132 | UV mapped texture + PBR |
| M_LampMetal | 133 | UV mapped texture + PBR |
| M_OceanWater | 133 | Dual Panner procedural animation |
| M_RimLight_Stone | 142 | Fresnel rim light calculation |

M_RimLight_Stone is the highest at 142 due to the Fresnel node calculation. All materials are within an acceptable range for a scene of this complexity.

### Optimizations Applied

1. **M_OceanWater node consolidation:** Removed one redundant Texture Coordinate node, connecting a single TexCoord output to both Panner nodes instead of two separate nodes. The UE5 shader compiler optimized both versions to equivalent output, confirming the compiler performs automatic deduplication of identical node evaluations.

2. **M_RimLight_Stone cleanup:** Removed explicit Metallic (0.0) and Roughness (0.85) Constant nodes. UE5's shader compiler folds constant values into the compiled shader regardless of whether they are explicit nodes or defaults, confirming no instruction count change from removing redundant constant nodes.

### Key Findings and Conclusions

- The scene is well optimized across all materials with no critical hotspots
- The UE5 shader compiler handles redundant node optimization automatically during compilation
- Post-processing is the primary GPU cost at 3.76ms, a known tradeoff for the visual quality of Bloom, Vignette, and Chromatic Aberration
- If performance optimization were required in production, reducing Post Process effect intensity or disabling Chromatic Aberration would yield the most immediate frame time savings
- All material instruction counts are below 150, within acceptable range for a real-time scene

---

*Updated: Week 6 — Shader profiling and optimization documentation*
