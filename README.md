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

## Project Setup Steps

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

## Version Control Steps

1. Created a new public GitHub repository at: https://github.com/JoeJeep/GDT-225-TheLastLight
2. Added a `.gitignore` file to the project root to exclude auto-generated UE5 folders:
   - Binaries/
   - Build/
   - DerivedDataCache/
   - Intermediate/
   - Saved/
3. Initialized a local Git repository inside the project folder.
4. Staged all project files and made the initial commit.
5. Pushed to the GitHub repository on the `main` branch.

---

## Repository Contents

```
GDT-225-TheLastLight/
    Config/         # Engine and project configuration files
    Content/        # UE5 level and asset files
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

*Updated: Week 1 — Initial project setup and version control*
