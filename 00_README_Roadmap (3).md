# RealDrive City — Project Foundation (Unity 6, C#)

## Honest Scope Note
This is a AAA-scale open-world driving game (city + highway + village + mountains +
airport + railway + trains + AI traffic + weather + day/night + full character sim).
That scope is normally built by a team of 15–40 people over 12–24 months. What follows
is a **real, buildable foundation**: correct project architecture, working core systems,
and a phase-by-phase roadmap so you (or a team) can fill in content (models, city
blockout, VFX, audio assets) using industry-standard patterns. Every script below is
functional, mobile-optimized C#, not pseudocode.

## Phased Delivery Plan
- **Phase 1 (done):** Project structure, GameManager, SaveSystem, AudioManager,
  WeatherManager, DayNightCycle, physics-based VehicleController, CharacterController.
- **Phase 2 (done):** NavAgentBase, PedestrianAI, TrafficAI (drives real VehicleController
  physics, not fake kinematics), PoliceAI pursuit FSM, PoolManager, CullingController
  (distance-based agent activation), LODManager (quality-tied LOD bias/shadow distance).
- **Phase 3:** Train system (spline-based movement, coaches, signals, crossings, station logic).
- **Phase 4:** UI system (main menu, HUD, pause, settings, graphics quality, save/load screens).
- **Phase 5:** Vehicle damage/crash system, fuel system, transmission (manual/auto), camera rigs
  (interior/exterior/FPV/TPV), input system (tilt/buttons/steering wheel).
- **Phase 6:** World building guide (city/highway/village/mountain/airport/rail layout in Unity
  Terrain + ProBuilder), reflection probes, volumetric fog, post-processing profile.
- **Phase 7:** Android/Play Store build settings, IL2CPP + ARM64 config, texture compression
  (ASTC), performance profiling checklist for Snapdragon/MediaTek.

Say "continue to Phase 2" (etc.) any time and I'll keep building.

## Folder Structure
```
RealDriveCity/
  Assets/
    _Project/
      Scripts/
        Core/          -> GameManager, GameState, SceneLoader
        Vehicles/       -> VehicleController, WheelData, DamageSystem, FuelSystem
        Character/       -> CharacterController, AnimationController, VehicleEntryExit
        AI/            -> TrafficAI, PedestrianAI, PoliceAI, NavAgentBase
        Train/          -> TrainController, RailSignal, StationStop
        Weather/         -> WeatherManager, DayNightCycle, RainController
        SaveSystem/       -> SaveManager, SaveData, JsonUtilityWrapper
        Audio/          -> AudioManager, EngineAudio, AmbientAudio
        UI/            -> MainMenu, HUDController, PauseMenu, SettingsMenu
        Optimization/     -> LODManager, PoolManager, CullingController
      Prefabs/
      Scenes/          -> MainMenu, CityWorld, Loading
      Materials/
      Models/
      Audio/
      Animations/
      Resources/
  ProjectSettings/  (created by Unity itself)
```

## Unity 6 Project Setup Checklist
1. New project -> **Mobile 3D URP** template (Universal Render Pipeline is mandatory for
   mobile 60 FPS — do not use HDRP on Android).
2. Player Settings: API level Android 13+ (target), min API 24 (Android 7.0).
3. Scripting Backend: **IL2CPP**, Target Architecture: **ARM64 only** (Play Store requirement).
4. Color Space: Linear.
5. Graphics API: Vulkan (primary) + OpenGLES3 fallback.
6. Install packages: Input System, Cinemachine, Addressables, ProBuilder, TextMeshPro,
   Universal RP, AI Navigation.
