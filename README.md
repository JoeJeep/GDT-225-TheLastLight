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
