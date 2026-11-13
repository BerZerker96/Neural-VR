# Neural Rendering VR — DLSS 5 neural rendering for VR

Neural Rendering VR puts NVIDIA's DLSS 5 neural rendering (DLSS‑NR) on the
picture inside your VR headset. It works with **OpenXR, SteamVR (OpenVR) and
Oculus (LibOVR)** games using **Direct3D 11, Direct3D 12, Vulkan or OpenGL**,
64‑ and 32‑bit. **Your desktop is never touched**: only the eye images sent to
the headset are changed.

In short:
- **DLSS 5 in VR**, with foveated rendering. Full quality where you look, and
  optionally a light low-resolution pass outside the fovea so there is no edge.
- **Post-processing** (sharpen, fine detail, anti-aliasing, SMAA, bloom,
  dehaze, colour), always with or without DLSS 5.

**What depends on what** (3.6): only the DLSS 5 options need the NR model and
DLSS 5 switched on. Everything else works on its own, with DLSS 5 on or off:

| Option | Needs DLSS 5? | Needs | Where |
|---|---|---|---|
| DLSS 5 look, foveation, NR resolution, upscaler, outer DLSS 5, cadence | yes | the NR model, an RTX GPU, HAGS on | app, VR panel |
| Post-processing (all of it) | no | any GPU the game runs on | app, VR panel *Game* |
| Frame generation (FidelityFX / RIFE / DLSS Gen), AER mode | no | RIFE: *Install RIFE* in the Layer Installer; DLSS Gen: RTX 40 / 50 + your nvngx_dlssg.dll | app *Framegen*, VR panel *Framegen* |
| 3D Strength, World Scale | no | - | app (purple card), VR panel *Game* |
| Camera (move the game's centre) | no | - | VR panel *Camera* |
| Edge fill (no black area around the game) | no | - (OpenXR, Oculus and SteamVR games) | VR panel *Fill* |
| Game render foveation (VRS) | no | NVIDIA GPU, D3D11 / D3D12 game | app *Fovea*, VR panel *Fovea* |
| Screenshots, VR panel, hotkeys | no | - | everywhere |
- **A settings panel inside the headset** (F12): change everything without
  taking the headset off - including the **Camera** tab (3.6), which moves
  the game's centre forward / back / left / right in any VR game.
- **3D Strength** (a depth boost), **World Scale**, **AER mode** for
  alternate-eye mods, and **stick-turn-aware** DLSS 5 motion.
- **Global hotkeys** and **PNG screenshots** of what the headset shows.
- **★ Frame generation** (new in 3.0): 2x, 3x, 4x or adaptive, with a
  FidelityFX-style optical-flow method or the RIFE neural network. No motion
  vectors needed, works in OpenXR, SteamVR and Oculus games, with or without
  DLSS 5. See *Frame generation*.
- **Game render foveation** (new in 3.1): the game itself shades less
  outside the fovea (variable rate shading) - real GPU time saved.
- **SMAA, Advanced sharpen, Light bloom** (new in 3.1) in post-processing.

> **Notice.** Not affiliated with NVIDIA. NVIDIA, DLSS and RTX are NVIDIA
> trademarks. NVIDIA's runtime `nvngx_dlssnr.dll` (the "NR model") is **not
> included**: you get it yourself, see *Getting the NR model*. Don't use this in
> competitive online games: injecting into a game is what anti‑cheat looks for.

## Start here (5 steps)

1. **Unpack** the `NeuralRenderingVR` folder somewhere it can stay, for example
   `C:\Games\NeuralRenderingVR`.
2. Run **`NeuralRenderingVR-LayerInstaller.exe`** → **Install everything**
   (Windows asks for administrator rights once). This one install covers every
   VR game. No game folders are changed.
3. **Get the NR model** (`nvngx_dlssnr.dll`, next section). Then run
   **`NeuralRenderingVR.exe`**, click **Browse…** in the green **NR model** bar
   at the top, and pick the file.
4. In the same bar, click **Self‑test DLSS 5**. It runs DLSS 5 once on your GPU,
   with no headset needed, and says *PASSED* or what is wrong.
5. **Start a VR game.** It appears under **Live**. In the headset:
   - **F12** opens the VR panel (all settings, use the mouse);
   - **Ctrl+F9** turns DLSS 5 on/off, **Ctrl+F10** changes the style;
   - **Ctrl+F7** turns post-processing on/off;
   - **Ctrl+F12** takes a screenshot.

Windows must have **Hardware-accelerated GPU scheduling** turned on (Settings
→ System → Display → Graphics → Default graphics settings), then reboot. The NR
model bar warns when it is off.

## Getting the NR model

The NR model is NVIDIA's `nvngx_dlssnr.dll`: the large file that holds the DLSS
5 neural network. Neural Rendering VR can't include it. Recommended sources:

| Your GPU | Recommended | Then in Neural Rendering VR |
|---|---|---|
| **RTX 50** | the **main** DLSS 5 model from the **RenoDX Discord**, where DLSS 5 modding is coordinated | **Browse…** to it; leave *Allow RTX 20/30/40* **off** |
| **RTX 40 / 30 / 20** | the **patched** model for older cards from the **RenoDX Discord**: the shipped one uses kernels that do not run on pre-Blackwell GPUs ([Tom's Hardware report](https://www.tomshardware.com/pc-components/gpus/exclusive-dlss-5-has-already-been-ported-to-work-on-rtx-4000-series-graphics-cards-incompatible-cuda-instructions-get-patched-to-work-on-previous-gen-hardware)) | **Browse…** to it and run the Self-test. Turn *Allow RTX 20/30/40* on only if the Self-test says your GPU is refused |
| any RTX | the model that comes with **[DLSS 5 Swapper](https://github.com/rakanki911/DLSS5-Swapper/releases)** (it bundles `nvngx_dlssnr.dll` for its DX12 game installs) | **Browse…** to the `nvngx_dlssnr.dll` from its download |

Tips:
- Keep the file somewhere it stays: for example in this folder's `runtime\`
  subfolder (Neural Rendering VR looks there by itself), and pick it once.
- The bar shows the file's version. After you replace the file, running games
  pick up the new one the next time they start.
- On RTX 20/30, community reports say DLSS 5 is slower and less stable than on
  RTX 40/50. Start with foveation on, 1 pass and **Auto performance**.
- Get the file only from sources you trust, and read *Legal notes*: it's
  NVIDIA's file and their terms apply to it.

## Using it in the headset: the VR panel

Press **F12** in any VR game (or **Open in headset** in the window). A dark,
semi-transparent panel appears in front of you:
- **Move the mouse** to move its cursor, **click** to change things, use the
  **wheel** to scroll. The mouse goes to the panel only while the **VR game's
  window is in front** on the desktop. Then the game doesn't get the mouse.
  **Alt+Tab** to any other window and the mouse works there normally at once.
  If the panel says *click the game's window*, click the game once on the
  desktop. The cursor follows the mouse's own movement (Raw Input), so games
  that hide, lock or recentre the Windows cursor, or take the mouse for
  themselves (DirectInput), don't stop it. If the game runs **as
  administrator**, run Neural Rendering VR as administrator too - Windows
  keeps the mouse from it otherwise (the agent log says so).
- **Top row:** *Neural VR* on the left; in the middle the **FPS counter**
  (white in a cyan frame): the game's own frames per second for the **L**eft
  eye, the **R**ight eye and **Both** (complete stereo frames - with an
  alternate-eye mod each eye shows half the game's rate), plus, while frame
  generation is making frames, **Headset** (game + made frames). On the right
  small **Screenshot** (camera) and **Close** (X) buttons and the big
  **DLSS 5 ON/OFF** button. A status line shows what DLSS 5 is doing. The
  cursor is a black arrow with a bright cyan outline.
- **Switches:** check boxes, choice buttons and the DLSS 5 button are
  **cyan when off** and **red with white words when on**; other buttons are
  cyan (the Camera tab keeps its red / green / blue pad).
- **Tabs:** *DLSS 5* (model and look), *Fovea* (fovea, NR resolution,
  upscaler, outer DLSS 5, game render foveation), *Game*
  (post-processing, 3D Strength, World Scale - per game), *Framegen*,
  *Runtimes* (VR runtimes, NR model status, RTX 20/30/40, screenshots),
  *Panel* (size, position, distance and opacity of the panel itself),
  *Camera* and *Fill* (edge fill).
- **Edge fill** (3.6): when a game runs below the headset's rate, the runtime
  turns its last frame with your head and shows **black** where that frame
  does not reach. With *Fill the black area around the game* on, a wider
  picture lies under the game's at all times, made from its newest frame:
  - **Edge stretch**: the rim pixels carried outward;
  - **Mirror**: the rim reflected (stretched to twice its width);
  - **Ambient light**: the rim's colours as a soft, darkening glow.

  *How far* adds 5-45 degrees on each side (25 by default). The game's own
  image is never touched, and the fill is world-locked by the pose of the
  game frame it was made from, so the runtime moves it exactly as it moves
  that frame:
  - **OpenXR** (also OpenComposite, UEVR - its dummy layer is skipped -,
    REFramework, vrframework, XRBridge32): a projection layer of our own
    *under* the game's (no depth on it).
  - **Oculus (LibOVR)**: an eye layer of our own under the game's.
  - **SteamVR (OpenVR)**: its Submit has no layers, so it is a side-by-side
    stereo *overlay* above the scene: a ring that is transparent where the
    game's picture is and holds the fill outside it, 8 m in front of the
    frame's head. While the frame is fresh the ring lies outside your view;
    when SteamVR turns an older frame, it covers the black.
  Cost: made once per game frame at 3/8 of the eye's resolution from a
  half-resolution copy; generated frames (frame generation) show the same
  fill, with no GPU work. With or without DLSS 5 and frame generation, AER
  mods included. Layers blended with what is behind (passthrough), head-locked
  layers and quad-view (Varjo) sessions are left alone.
- **Camera** (3.6, per game): the red **Forward**, **Back**, **Left** and
  **Right** buttons and the green **Up** and **Down** beside Forward move where the game puts you by
  *Each press* (1-200 cm, 25 cm by default); press as often as you like (in
  whole millimetres, up to 50 m each way). The blue **Reset** goes back to the
  game's own centre. *Where it is now* shows the offset.
  It works the same in every VR game and mod, with or without DLSS 5:
  - OpenXR (also OpenComposite, UEVR, vrframework, OFXR-Bridge games): the
    game's room spaces are moved - `xrLocateViews` and `xrLocateSpace` give
    the head and the controllers moved; the runtime gets the real poses back
    with every frame (projection, quad and cylinder layers), so its
    reprojection stays right.
  - SteamVR (OpenVR): `WaitGetPoses` gives the game the head and
    controllers moved; posed submits get the real pose back.
  - Oculus (LibOVR): `ovr_GetTrackingState` (head and hands, and so
    `ovr_GetEyePoses`) moved; the layer's render poses and world-locked
    quads get the real poses back.
  - Directions are the room's (tracking space: forward = -Z), not where you
    are looking. Head-locked layers (HUDs) are left alone.
  - Limits: SteamVR games that read poses only through
    `IVRSystem::GetDeviceToAbsoluteTrackingPose`, and OpenXR games that use
    `xrLocateSpaces` (OpenXR 1.1) for controllers, see the head moved but not
    those controllers. SteamVR games with anti-cheat are left alone.
- It has every setting of the window. The exceptions are the hotkeys and the
  file/folder pickers (Browse…, Folder…), which need the desktop.
- Every change applies at once and is saved, so the window and all other VR
  games use it too. **Screenshots never show the panel.**
- **F12** again, **Esc** or **Close** closes it. If no VR game is showing it,
  it closes by itself after 2.5 s and gives the mouse back. This watchdog runs
  next to the mouse capture itself, so it works even if the program that
  opened the panel hangs.

## What's in the folder

| File | What it is |
|---|---|
| `NeuralRenderingVR.exe` | **Start this.** Control panel: the DLSS 5 switch, the OpenXR / OpenVR / Oculus toggles, the model, foveation and post-processing settings, logs and a **Diagnostics** report. Changes apply live. |
| `NeuralRenderingVR-LayerInstaller.exe` | Installs everything (asks for admin). |
| `NeuralRenderingVR-Agent.exe`, `NeuralRenderingVR-Agent32.exe` | Background agent for native SteamVR / Oculus games, 64- and 32-bit. Starts at logon. |
| `NeuralRenderingVR-EngineHost.exe` | 64-bit DLSS 5 engine for 32-bit games (NVIDIA's runtime is 64-bit only). |
| `layer\NeuralRenderingVR_XR.dll`, `layer\NeuralRenderingVR_XR32.dll` + `.json` | OpenXR API layer, 64- and 32-bit. |
| `layer\NeuralRenderingVR_VkLayer.dll`, `layer\NeuralRenderingVR_VkLayer32.dll` + `.json` | Vulkan helper layer: makes Vulkan SteamVR / Oculus games shareable with the engine (see below). |
| `hook\NeuralRenderingVR_Hook.dll`, `hook\NeuralRenderingVR_Hook32.dll` | OpenVR / Oculus hook loaded by the agent. |
| `hook\NeuralRenderingVR_Hook[32]_dxgi.dll` / `_version.dll` | The same hook as a per-game file, for the fallback install. |
| `runtime\` | Optional place for your `nvngx_dlssnr.dll`. |

## Requirements

- Windows 10 (1703 or newer) or Windows 11, 64‑bit.
- An NVIDIA RTX GPU (RTX 20, 30, 40 or 50) with a current NVIDIA driver.
  Shipped `nvngx_dlssnr.dll` builds accept only Blackwell (RTX 50); for older
  cards see *Getting the NR model*. **Allow RTX 20/30/40 (unofficial)** in the
  NR model bar is **off by default**. When you turn it
  on, Neural Rendering VR answers that DLL's architecture query with the
  Blackwell value, for that DLL only: only the NR runtime's own NVAPI lookup
  is redirected (its import table), NVAPI itself is not modified, the game's
  own NVAPI queries keep the real answer, and nothing is written to disk.
  Read *Legal notes* below before turning it on.
- **Hardware-accelerated GPU scheduling ON** (Windows Settings → System →
  Display → Graphics → Default graphics settings). With it off, or with an old
  driver, DLSS‑NR does not start.
  [mbucchia's notes for the Virtual Desktop DLSS‑NR build](https://github.com/mbucchia/VirtualDesktop-OpenXR/wiki/Experimental-DLSS%E2%80%90NR-Build)
  name the same two causes.
- Your own `nvngx_dlssnr.dll` (the NR model, see *Getting the NR model*).
- Only for DLSS 5: the NR model, an RTX GPU and HAGS. Post-processing, frame
  generation, 3D Strength, World Scale, the Camera, screenshots and the VR
  panel work without the NR model and with DLSS 5 off.
- Optional: the **RIFE** frame-generation model (Layer Installer → *Install
  RIFE*; downloaded from its own release, not shipped here). Without it RIFE
  falls back to FidelityFX.
- Optional: **DLSS Gen** frame generation - an RTX 40 / 50 GPU and NVIDIA's
  `nvngx_dlssg.dll` next to `NeuralRenderingVR.exe`. The Layer Installer's
  **Download DLSS Gen** fetches it from NVIDIA's own Streamline SDK 2.14.16
  release on GitHub (only the DLL and its license text, about 4 MB, read out
  of the SDK archive; checked by SHA-256) and places it there; *Pick file...*
  copies one you have. The app finds it by itself. Not included here.
- Game render foveation (VRS): an NVIDIA GPU and a Direct3D 11 / 12 game.
- To get everything: run the Layer Installer's *Install everything* once (the
  OpenXR layer, the Vulkan helper layer and the agent for SteamVR / Oculus
  games), and leave the agent running (it starts at logon).

## Which games are covered

| How the game talks to VR | What Neural Rendering VR uses |
|---|---|
| OpenXR: most new games, MSFS, DCS, iRacing… (64- or 32-bit, any runtime) | OpenXR layer (global) |
| Native OpenVR / SteamVR (Half‑Life: Alyx, Unity/Unreal SteamVR games…) | agent + hook (global) |
| OpenVR linked into the game statically (no `openvr_api.dll`) | agent + hook on the SteamVR client (`vrclient`) |
| Native Oculus / Meta PC SDK (LibOVR) | agent + hook (global) |
| Unity / Unreal games with the Meta OpenXR plugin (OVRPlugin) | OpenXR layer (the LibOVR hook stands aside) |
| **UEVR** (praydog) | OpenXR layer when UEVR uses OpenXR, also with Virtual Desktop (UEVR's dummy projection layer is skipped); agent + hook when it uses OpenVR, even when UEVR is injected long after the game started. Unreal's BGRA eye images are supported |
| **REFramework** VR (praydog, RE Engine games) | agent + hook when it uses OpenVR (SteamVR running, its default); OpenXR layer otherwise. Its alternate-frame eye submission is handled |
| **witcher3-vr** and other D3D12 OpenXR mods with array swapchains | OpenXR layer |
| **Luke Ross R.E.A.L. VR** mods (OpenVR, Oculus or OpenXR) | the matching path; alternate-eye rendering is handled (an eye image resubmitted unchanged is not processed twice; in AER mode frame generation makes each eye from its own frames, both eyes at one moment) |
| **vrframework** multi-game mods (a `dxgi.dll` in the game folder; Assassin's Creed Black Flag and Origins to Shadows, God of War / Ragnarok, Starfield, Alan Wake 2, Control, A Plague Tale) | OpenXR layer (the mod has an OpenXR loader built in, which loads API layers) or agent + hook on the SteamVR client when it uses OpenVR. Its own DLSS / FSR per eye: DLSS 5 runs in the engine host. *Runtime* alternate-eye mode: frame generation makes each eye from its own frames (both at one moment); *Viewport reproject* / *DDR* modes send both eyes new each frame. Its own **VRS image**: game render foveation stands aside by itself - use one or the other |
| Flat-to-VR mods with their own VR host process and a built-in OpenXR loader (e.g. ACUnityVR, DeusExHRVR) | OpenXR layer in the host process; their virtual-screen (quad) mode is processed too |
| OpenVR game through **OpenComposite / OpenOVR** | OpenXR layer (OpenComposite turns the game's frames into OpenXR frames; the OpenVR hook stands aside, so nothing is processed twice, and it never asks OpenComposite for interface versions the game doesn't use) |
| **NieR:Automata VR** and other mods that skip the OpenXR loader | OpenXR layer - **automatic, from the first start**: the agent sees the mod's DLL in the game folder and loads the hook early; when the mod asks the runtime for its entry points, it gets the official OpenXR loader's, so the layer loads in front of the runtime. As a fallback the official loader is also placed next to the game (see *Other mods and tools*) |
| **Direct3D 9 / Direct3D 10 games** on SteamVR (UE3 games, older mods) | agent + hook. D3D9 mods submit a shared surface (`TextureType_DXGISharedHandle`) or a D3D11 copy; D3D10 games submit a D3D10 texture. All three are processed (shared surfaces on Neural Rendering VR's own D3D11 device). 32-bit ones run DLSS 5 in the engine host |
| **Dishonored VR** (1.0.4, OpenXR, 32-bit D3D9 game) | OpenXR layer: with XRBridge32 (Pimax and other 64-bit-only runtimes) DLSS 5 runs in its 64-bit host; with the mod's SteamVR shim, in the game through the engine host. The mod's own check of registered layers (`DisableBadApiLayers`) no longer switches Neural Rendering VR off (since 2.4.0; *Reinstall layers* once). |
| **junglejuz VR mods**: Batman Arkham Knight / City / Origins VR, Dark Souls III VR, NieR:Automata VR | OpenXR layer (D3D11; City and Origins are 32-bit and run DLSS 5 in the engine host). Their HUD and menu quads are left alone; NieR's mod skips the OpenXR loader and is handled as above |
| Quad‑view apps (Varjo, Pimax foveated) | OpenXR layer; DLSS 5 on the inner views |
| OpenGL games (OpenVR or OpenXR), e.g. Vivecraft | the matching path + the OpenGL bridge |
| Oculus compatibility runtimes under another file name (Pimax Play's Oculus support, ReVive) | found by their LibOVR exports, in the hook and in the agent |
| 32-bit games of any of the above | same paths; DLSS 5 runs in `NeuralRenderingVR-EngineHost.exe` |
| Vulkan SteamVR / Oculus games (No Man's Sky, Doom VFR, Serious Sam, …) | agent + hook + the **Vulkan helper layer**, which enables the interop extensions when the game creates its device (the hook usually arrives a moment later) |
| OpenGL Oculus games (`ovr_CreateTextureSwapChainGL`), OpenGL array textures (`Submit_GlArrayTexture`) | the matching path + the OpenGL bridge |

Coverage by runtime and graphics API (✓ = processed, 64- and 32-bit):

| | D3D11 | D3D12 | Vulkan | OpenGL |
|---|---|---|---|---|
| OpenXR (any runtime: SteamVR, Meta, Pimax, Varjo, WMR, VDXR, ALVR…) | ✓ | ✓ | ✓ | ✓ |
| OpenVR / SteamVR | ✓ | ✓ | ✓ (helper layer) | ✓ |
| Oculus LibOVR (Meta, Pimax Play, ReVive) | ✓ | ✓ | ✓ (helper layer) | ✓ |

Eye-image formats: RGBA8 / BGRA8 / BGRX8 (and their sRGB variants), RGB10A2,
RGBA16F, R11G11B10F. Not processed: MSAA eye images (OpenGL MSAA renderbuffers,
multisampled swap chains; SteamVR resolves those itself) and pre‑1.0 Oculus
SDKs (0.x).

Graphics APIs: D3D11, D3D12, Vulkan and **OpenGL**. OpenGL (Vivecraft /
Minecraft VR, Doom 3 BFG and Quake VR ports, emulators, OpenGL OpenXR apps)
goes through NVIDIA's `WGL_NV_DX_interop2`: the eye image is blitted into a
shared D3D11 texture (flipped to top-down rows), processed like a D3D11 game
and blitted back, with the game's GL state restored.

**Per-game fallback** (installer, bottom card) puts the hook next to one
game's `.exe`. You only need it if the agent misses a game:
- games that run **as administrator** when the agent could not start elevated
  (the installer's "Neural Rendering VR Agent" scheduled task is missing);
- Oculus games using **D3D12 or Vulkan** that create their swap chains within
  milliseconds of starting.

**Don't stack two DLSS‑NR injectors.** CheekyFoveatedDLSS's OpenXR layer or
UEVR plugin with DLSS-NR enabled counts too. Diagnostics lists such layers. If you use Virtual Desktop's
experimental DLSS‑NR build (VDXR), or another DLSS‑NR mod, turn DLSS‑NR off
there or turn Neural Rendering VR's OpenXR toggle off. Otherwise the image goes through
the network twice.

## Frame generation

The green **★ Framegen** card (under the hotkeys) and the VR panel's
**Framegen** tab. Every setting applies mid-game.

| Setting | What it does |
|---|---|
| **Frame generation** | On/off (hotkey Ctrl+F6). Works with DLSS 5 off too. |
| **Method** | **FidelityFX**: optical flow (block matching from coarse to fine on a luminance pyramid, the head's rotation taken out first using the eye poses) and a two-way warp that picks, per pixel, the candidate that matches both frames. The lightest. **RIFE**: the RIFE 4.6 network (run by Neural Rendering VR's own Direct3D 12 executor, no Python or Vulkan needed). Better on large, complex motion; costs more GPU. Install it in the **Layer Installer** (*Install RIFE*); until then RIFE falls back to FidelityFX. **DLSS Gen** (3.7): NVIDIA's DLSS Frame Generation network (RTX 40 / 50) makes the frame half way between the game's two, fed with this app's own motion (the head's turn between the frames plus the measured optical flow) - each eye has its own. 2x uses it for every made frame; 4x for the middle one; 3x, Low latency and AER offsets use FidelityFX for the moments it does not make. When the network itself declines a frame (it saw a cut), the newer frame is shown turned to that moment instead. Needs `nvngx_dlssg.dll` next to `NeuralRenderingVR.exe` (not included - the Layer Installer's **Download DLSS Gen** fetches NVIDIA's own build); without it, or on a GPU that refuses it, FidelityFX is used and the status line says why. Works with every runtime and graphics API frame generation works with (it runs in this app's own Direct3D 12 engine on the eye images). |
| **Frames** | **2x** (the game renders at half the headset's rate), **3x**, **4x**, or **Adaptive** (1x to 6x): follows the game's frame rate so the headset gets its refresh rate - a 50 fps game runs at 45 with 2x, a 38 fps game at 30 with 3x, a 20 fps game at 18 with 5x (90 Hz). It reacts within a few frames when the game slows down and steps back one step at a time when it speeds up; every step is checked and undone if it did not bring the headset more frames. |
| **Always reach refresh** | (on by default) 2x / 3x / 4x are minimums: when the game can't keep up with the chosen one, it is raised (up to 6x) the same way, so the headset keeps getting its refresh rate. Off: exactly the chosen multiplier. |
| **Quality** | Resolution of the motion search (Perf. 25 %, Balanced 33 %, Quality 50 %, Ultra 67 % of the eye; RIFE 25-67 %). |
| **Latency** | **Smooth**: the generated frames lie between the game's last two frames (one headset frame of delay; head rotation stays instant through the runtime's reprojection). **Low latency**: they're made ahead of the newest frame instead (FidelityFX only; a little more artefacting at edges). |
| **Highest refresh rate** | Asks the headset for its highest refresh rate (OpenXR runtimes with `XR_FB_display_refresh_rate`: Quest Link, Virtual Desktop, Pico; at the next game start). |
| **Keep the HUD steady** | Head-locked parts of the image (HUDs, menus) are not moved. |

**How it presents.** OpenXR: the layer paces the game (xrWaitFrame returns
every *m* headset frames with the matching display time) and submits the
generated frames as full frames of their own. SteamVR / OpenVR: the game's
two eye submits are held, the generated pair goes first with its interpolated
pose, then SteamVR's next frame slot is waited for and the game's pair
follows (each eye with the pose it was made for). Oculus / LibOVR: the
generated frames go out from Neural Rendering VR's own swap chains, each with
its own frame begin. Through OpenComposite
and XRBridge32 games are OpenXR games to the layer, so they're covered too.

**Turn off** SteamVR Motion Smoothing, ASW, SSW or Virtual Desktop's frame
synthesis while it's on - two frame generators fight.

**Frame rates.** The generated frames are presented on the game's own
thread, in step with the runtime. A GPU-bound game (as VR games usually
are: little CPU work per frame, the GPU is the limit) gets the headset's
full refresh rate at any frame rate the multiplier covers. A game whose own
CPU work per frame is longer than a headset frame (11 ms at 90 Hz) gets
most of the way (e.g. ~70 frames/s to a 90 Hz headset from a 38 fps
CPU-limited game) - the adaptive multiplier then stops at the step that
still brings more frames instead of climbing for nothing. The log says
which case a game is (`frame generation ... -> ...` lines).

**Every runtime and graphics API.** OpenXR: Direct3D 11 / 12, Vulkan,
OpenGL. SteamVR / OpenVR: Direct3D 11 / 12, Direct3D 10 and Direct3D 9
(shared surfaces), Vulkan and OpenGL - the generated frames are the same kind
of texture the game submits (on its own device / GL context). Oculus /
LibOVR: Direct3D 11 / 12, OpenGL and Vulkan swap chains. If a generated frame
can't be made (a Vulkan game whose device lacks the external-memory
extensions - install the Vulkan helper layer -, a driver without sharing),
the game's own image is shown in its place: never an empty or old one.

**Alternate-eye rendering (AER).** Mods that render one eye per frame (Luke
Ross' R.E.A.L. VR in AER mode, vrframework mods' *Runtime* AER, any mod
that submits one new eye per frame) are recognised in every runtime (the eye that isn't
new comes with its old image or pose). Frame generation then makes **each eye
from its own two frames** (two game frames apart) for **one moment for both
eyes**: the generated frames show both eyes in step - which plain AER never
does - and the game's own frames go out as they are. A copy of the old eye
(mods that copy both eyes into one swapchain every frame) is kept out of the
history. UEVR's *Native stereo* and *Synchronized sequential* modes render
both eyes per VR frame: the usual case.

**Limits.** Apps with four views (quad views) and games with anti-cheat are
left alone. If the runtime rejects a generated LibOVR frame, frame generation
turns itself off for that session and the game's frames go on unchanged.
With the VR panel open, the panel is part of the image the frames are made
from: with *Keep the HUD steady* on (the default) it stays in place like a
HUD.

**With OFXR-Bridge.** Only one frame generator should run: when OFXR-Bridge's
frame generation is on for the game (its `[ofxr] enabled`), Neural Rendering
VR's stands aside and DLSS 5 keeps running; turn OFXR's off to use this one.

## Other mods and tools

| Tool | What happens |
|---|---|
| **Ultimate ASI Loader** (ThirteenAG) | No conflict with the background agent. For the per-game fallback, if the game folder has the ASI loader, Neural Rendering VR is installed as `scripts\NeuralRenderingVR.asi` (or `plugins\`) instead of taking a proxy DLL name. |
| **OptiScaler** (and its DLSS-NR forks, e.g. tig3rmast3r's VR build and Dagherbou's) | OptiScaler's own upscaling works alongside. If the game also runs DLSS-NR through one of the DLSS-NR forks, Neural Rendering VR sees NVIDIA's NR runtime loaded by another mod and **stands aside**, so the image isn't run through DLSS-NR twice. Turn the fork's DLSS-NR off to use Neural Rendering VR's instead. |
| **OFXR-Bridge** (tig3rmast3r's and djules75's, 0.2 / 0.3) | Works together, no crash, DLSS 5 not blocked. Neural Rendering VR's layer is kept above OFXR's (the installer and the agent re-order the layer list when OFXR registers itself), so OFXR generates frames from the DLSS 5 output and its generated frames are not processed again. OFXR hooks Direct3D 12 and NGX in the whole game; Neural Rendering VR's DLSS 5 then runs in its own engine process, out of reach of those hooks, and OFXR's `nvngx.dll_dlssnr.dll` forwarder no longer counts as "another DLSS-NR mod". If OFXR's own *Neural Rendering* stage is on, Neural Rendering VR stands aside (one DLSS-NR is enough). If OFXR's frame generation is on, Neural Rendering VR's frame generation stands aside. |
| **ReShade**, ReShade add-ons (e.g. OpenXR UI), **Special K**, other D3D wrappers / proxy `d3d11.dll` `dxgi.dll` `d3d12.dll` in the game folder | Works together. These wrap *every* graphics device made in the game, so DLSS 5 then runs its own devices in `NeuralRenderingVR-EngineHost.exe` instead, where no wrapper is loaded. The game only opens the shared images. The log says *running DLSS 5 in NeuralRenderingVR-EngineHost.exe (... is loaded)*. Before 2.2.2 a ReShade OpenXR add-on could crash on DLSS 5's own D3D11 device. |
| **OpenComposite / OpenOVR** | See the table above. |
| **CheekyFoveatedDLSS, VDXR's DLSS-NR** | Another DLSS-NR: Cheeky in the game is detected and Neural Rendering VR stands aside; for VDXR turn one of them off (it runs inside Virtual Desktop and can't be detected). |
| Browsers (WebXR), web views, Discord, OBS | They use the OpenXR runtime directly on purpose and are left alone. Nothing is placed next to them, and copies an older version put there are removed. |
| **Control Resonant VR** (nmfvr, `dxgi.dll` in the game folder) and other D3D12 mods that hook `ExecuteCommandLists` | Automatic. Neural Rendering VR sees that the game queue's submit is hooked and runs its copies on a queue of its own, ordered with fences, so the mod's hook never sees Neural Rendering VR's command lists in the middle of its own VR frame. A mod that calls OpenXR again from inside that hook is passed straight on instead of waiting on itself. |
| **AC Unity VR** (ACUnityVRHost.exe, OpenXR loader built in) | OpenXR layer in the mod's VR host. The host switches every OpenXR layer off once its `ACUnityVR-implicit-layers-disabled.flag` exists (written after one failed start) - the agent switches ours back on as the host starts. If DLSS 5 still doesn't show, set `DisableImplicitLayers=0` in `ACUnityVR.ini` (or delete the flag file) and send `ACUnityVR-OpenXR.log`. |
| **XRBridge32** (32-bit OpenXR games on a 64-bit-only runtime, e.g. Pimax) | Automatic. DLSS 5 runs once, in XRBridge32's 64-bit host (`xrbridge_host.exe`), inside the same process as the OpenXR session: no extra copies and no trip through the engine host. The 32-bit layer in the game sees the runtime named *XRBridge32* and only passes calls on (before 2.3.1 both ran DLSS 5, which cost a lot). Profiles, the VR panel and screenshots use the game's name, not the host's. Needs the 64-bit layer installed (it is, with *Install everything*). Checked with the newer XRBridge32 (shared-memory calls, NT handles for D3D12 / Vulkan games, D3D9 virtual-screen proxy): the host clears `XR_ENABLE_API_LAYERS`, which only affects explicit layers - Neural Rendering VR is implicit and still loads there. The new XRBridge32 starts its host before the game's first OpenXR instance, so a mod's switch-off of our 64-bit layer (Dishonored VR) reached the host and DLSS 5 fell back to the slow path in the game; since 2.5.0 it is switched back on in the host before the host's OpenXR instance starts. |
| Mods that skip the OpenXR loader (**NieR:Automata VR**, ...) | They load no OpenXR layer at all - not Neural Rendering VR, not OpenXR Toolkit, not OFXR. **Automatic, first start:** the agent finds a DLL in the game folder that talks to OpenXR runtimes without any loader and loads the hook right away. When that DLL asks the runtime for `xrNegotiateLoaderRuntimeInterface` / `xrGetInstanceProcAddr`, it gets the official Khronos loader's (`extras\openxr_loader`, Apache-2.0), which loads every API layer and the same runtime below them. Loaders built into a program (UEVR, OVRPlugin) already load layers and are not touched. **Fallback:** if the runtime was loaded before the hook arrived, the loader is copied next to the game's `.exe` (never replacing one) for the next start. `[advanced] auto_openxr_loader=0` turns the copy off. |

`[advanced] yield_to_other_nr=0` makes Neural Rendering VR run even when another
DLSS-NR mod is loaded in the game (double processing).

## Settings (NeuralRenderingVR.exe)

**Per game:** *Post-processing* and *3D Strength* are saved for each game on
its own. The bar at the top of both cards shows which game you are changing
(it follows the VR game that is running; the arrows pick another game, or
*New games*, the values a game starts with before it has its own). Hotkeys
for these two change the game that is running. DLSS 5, foveation, the NR
model, hotkeys and the VR panel are the same for every game. In the VR
panel, both are in the *Game* tab.

**Same for all games:** a switch in both cards (and in the VR panel). On, one
set of values is used for every game instead of a profile per game; off, each
game gets its own profile back. Post-processing, 3D Strength and World Scale
each have their own switch.

**Keep game detail and DLSS 5 cadence** (Resolution card; VR panel:
*Foveation* tab). *Keep game detail* (on by default): below 100 % NR
resolution only DLSS 5's change is scaled up and put on the game's own
full-resolution image, so lowering the NR resolution saves GPU time without
making the picture soft. *DLSS 5 on: All frames / Every 2nd / Every 3rd*: in
between, the last DLSS 5 change is moved with your head and reused - half or
a third of the GPU cost.

**Stick and controller turns** (3.4): DLSS 5's motion vectors come from the
head's rotation; the turn the game's camera makes on its own (a stick turn, a
third-person camera) is measured on the GPU between the last two frames (yaw /
pitch) and added, so DLSS 5's history does not drag behind in turns.

**AER mode** (Framegen card / VR panel, per game, 3.4): for alternate-eye mods
(Luke Ross R.E.A.L. VR, vrframework AER, UEVR AFR). Every frame shown gets both
eyes at one moment: the newer eye as rendered, the other made between its own
two frames (as OFXR-Bridge's AER framegen). Which eye is older comes from the
mod's eye poses; *Swap eyes* decides when they don't tell.

**Dehaze** (Post-processing): large-radius local contrast on the mid-tones
that cuts through haze, worked out at a quarter of the resolution (light on
the GPU since 3.3). 0 % is off.

**3D Strength and World Scale** (purple card; VR panel: *Game* tab).
Neither is a DLSS feature: both work with DLSS 5 off, in OpenXR, SteamVR
(OpenVR) and Oculus (LibOVR) games.
- **3D Strength** (3.5: as Primashock's OpenXR Toolkit depth boost / VectorXR's
  convergence): each eye's image is shown shifted a little (the runtime is
  told a shifted projection; SteamVR: the texture bounds), so near things
  stand out more and the world keeps its size. 0-100 % (100 % = 0.05 in
  tangent space per eye); 20-40 % to start. Applies live. The outer edge of
  the view loses a sliver.
- **World Scale** sets how big the world looks, the way OpenXR Toolkit does
  it: 25 % to 250 %, 100 % is real size, 200 % makes the world look twice as
  big (the game renders with half the eye distance). Only the eye distance
  changes - your head's and hands' movement stay 1:1, so controllers never
  drift away from your hands (UEVR's world scale changes the engine's
  units instead, which only an engine mod can do). It has its own switch and
  its own *same for all games* switch, so it can be per game while 3D Strength
  is global, or the other way round.
- They are independent: 3D Strength shifts the projection, World Scale the
  eye distance. The runtime always gets the real eye poses back with each
  frame, so its reprojection does not undo either. SteamVR and Oculus games
  read the eye distance once at start: restart the game after switching
  World Scale on or off there (3D Strength applies live).


Each card has its own header strip (dark blue with a thin cyan frame; red for
post-processing). Everything fits on one screen, no scrolling: the header with the big red
**DLSS 5** master switch, the green-framed **NR model** bar under it, and
five columns of cards. On a narrow window the cards rearrange into fewer
columns.

**DLSS 5** (top right, red). The master switch. Its hotkey is shown next to
it (Ctrl+F9 by default). The chip beside it says *Active in VR*, *Off* or
*Post-processing only*.

**NR model** (the bar with the thin green frame, at the top). Where your
`nvngx_dlssnr.dll` is (path, version, **Browse…**), **Self‑test DLSS 5**, and
**Allow RTX 20/30/40** (off by default; read *Legal notes* first). A chip
warns when Windows GPU scheduling (HAGS) is off. The frame turns orange while
no runtime is set. The self-test result appears inside the bar (**Hide**
closes it).

**VR runtimes.** One toggle each for **OpenXR**, **OpenVR / SteamVR** and
**Oculus / LibOVR**, with install status. Below them:
- an install line: *Layers up to date*, or *out of date* when the installed
  layers, hooks or agents differ from the ones next to `NeuralRenderingVR.exe`
  (after you unpack a new version);
- **Reinstall layers** (asks for administrator rights once) copies the new
  layers, hooks, agents and engine host into place, re-registers them and
  refreshes per-game hooks. Restart running VR games afterwards;
- **Installer…**, **Open logs** and **Diagnostics**.

**Neural model.**
- **Preset:** Default / A (original) / B (faster, needs NR 310.9.16 or newer).
- **Style:** Standard / Natural / Cinematic.
- **Passes:** 1, 2 or 3 (maximum 3). Each further pass runs DLSS 5 again on
  the previous pass' output, with its own temporal history, for a stronger
  effect at about 2× / 3× the network cost. If a pass can't start, fewer run.
  If any pass fails in a frame, that frame keeps the game image.
- **Auto performance** + **GPU budget** (2–25 ms, both eyes): over budget it
  drops a pass, then lowers the NR resolution in 15 % steps (down to half);
  well under budget it gives them back. Start with about half your frame
  time: 90 Hz = 11 ms per frame → 5–6 ms. Lowering and raising the NR
  resolution does not rebuild DLSS 5 (it runs on part of what was made for
  your NR resolution), so the steps cause no hitch.
- **Intensity**, **Blend** (with the original), **Local tone**, **Structure**.
- **Automatic mask**, which protects skin and unlocks **Skin structure**.
- **UI correction.**
- **Temporal history:** *Head* (motion vectors from your head rotation, the
  default), *Static* (zero motion) or *Per frame* (no history).

**Foveated rendering.**
- **On/off.** Off processes the whole eye at full quality.
- **Fovea centre:** lens centre (plus **Offset X/Y**) or **Eye tracking**
  (restart the game after switching). The gaze comes from:
  - the OpenXR runtime's `XR_EXT_eye_gaze_interaction` (Quest Pro over Link,
    Varjo, Pimax Crystal, Vive Pro Eye…), in OpenXR games;
  - **Pimax's eye tracker, in every game**: the agent reads it through Pimax's
    own client (`libPVRClient64.dll`, as PimaxXR does) and shares it, so SteamVR
    and Oculus games, 32-bit games, games through XRBridge32, and OpenXR runtimes
    without the extension get an eye-tracked fovea too. Nothing of Pimax's
    client loads into the game. The agent must be running (it is, after
    *Install everything*).
  - Without a gaze source the fovea stays at the lens centre.
- **Width/Height**, **Softness** and **Roundness**.
- **Fovea outline:** a cyan ring for checking alignment.
- **Game renders foveated** (new in 3.1, off by default): *real* foveated
  rendering of the game itself. DLSS 5's foveation limits where DLSS 5 runs;
  this makes the **game** shade less outside the fovea, with variable rate
  shading (VRS), so the game's own GPU time drops. The pattern follows the
  fovea above (place, width, height, roundness, offsets), per eye in
  side-by-side render targets; **Outside the fovea** (3.3): *Quality* (a
  large full-rate area, a 2x1 ring, 2x2 outside), *Balanced* (2x2 ring, then
  4x4), *Performance* (a smaller full-rate area) or *Ultra performance* (the
  smallest full-rate area). VRS changes how the **game** renders, before DLSS
  5 sees the image, so it works the same at every **NR resolution** and with
  **Keep game detail** on or off. Direct3D 12 games, and Direct3D 11 games on
  NVIDIA; Vulkan, OpenGL and Direct3D 9/10 games render normally (no VRS
  hook there). Render targets at least about the size of the eye images
  get it; shadow maps and small post-processing targets don't (fholger's
  openvr_foveated works the same way). Every runtime: OpenXR, SteamVR,
  Oculus, OpenComposite, XRBridge32, UEVR.
  - With **Fovea centre: Eye tracking** (and a headset with eye
    tracking), the pattern follows your gaze (since 3.1.2).
  - **Direct3D 12 games:** any GPU with VRS tier 2 (NVIDIA RTX / GTX 16,
    AMD RX 6000+, Intel Arc). Render targets the game creates after the VR
    view has started get it. OpenXR games are watched from the moment their
    VR session is created (before their eye targets exist), as OpenXR Toolkit
    does; SteamVR / Oculus games from their first submitted frame (most
    engines create eye targets when VR starts or the resolution changes;
    otherwise restart the game with it switched on).
  - **Compared with OpenXR Toolkit's foveated rendering:** the same kind of
    VRS (D3D12 tier 2 / NVIDIA NVAPI on D3D11), the same rule for which
    render targets get it (about the eye images' size), fixed or following
    the eye tracker. Differences: it also works in SteamVR / Oculus /
    OpenComposite / XRBridge32 games (OpenXR Toolkit is OpenXR only), and it
    has no per-game "ignore this render target" list - switch it off for a
    game that looks wrong. Vendor implementations built into games (NVIDIA
    VRWorks, Unreal / Unity foveated rendering) can do more because the game
    chooses the targets itself; turn those on in the game when it has them,
    and leave this off for that game.
  - **Direct3D 11 games:** NVIDIA RTX / GTX 16 (NVIDIA's NVAPI VRS
    extension). Vulkan and OpenGL games: not possible from outside the game.
  - **Games and mods with their own VRS** (vrframework mods' VRS image,
    games with a VRS setting): as soon as the game sets shading rates itself
    (Direct3D 12), this one stands aside for that session and leaves the
    game's own alone - two foveations on one shading-rate image would undo
    each other. Resets to full rate don't count. (Direct3D 11 games that use
    NVIDIA's VRS themselves are rare and not detected: switch it off there.)
  - The usual trade-off of fixed foveated rendering: some games render in
    ways that pick up the pattern on the wrong targets (blurry UI, a blocky
    edge). If a game looks wrong, switch it off for that game; the log says
    which render targets got the pattern (`vrs:` lines).
- **Quad‑view apps:** process the inner views only.

**Resolution & upscaler.**
- **NR resolution.** At **100 %** the network gets the eye's own pixels 1:1
  and its result goes back 1:1 (the card says *native 1:1*). Nothing is
  resampled, so the image is as sharp as the network makes it. (Before 2.1 an
  eye whose width was not a multiple of 8 was stretched by a few pixels and
  back, which softened it.) Anything from 98 % up snaps to native. Below that
  the network runs at a lower resolution and is scaled back up.
- **NR upscaler** (on by default). Scales the network's result back up with
  the **Upscale filter** you pick - Nearest (blocky), Bilinear (soft), Bicubic
  (Catmull-Rom, default) or Lanczos (sharpest, no ringing at edges). At 100 %
  NR resolution nothing is scaled, so the filter shapes the 1:1 image: Nearest
  raw, Bilinear softer, Bicubic slightly and Lanczos clearly sharper. It also puts back
  the eye image's own fine detail that a lower-resolution network cannot
  reproduce. **Upscaler detail** (3.6) sharpens the **DLSS 5 layer itself**
  where it is scaled up - the network's own texels minus their blur, limited
  so edges get no halos - never the game's image: with *Keep game detail* on
  only DLSS 5's change is sharpened, and outside the fovea or at 100 % NR
  resolution (nothing scaled) it does nothing. For the whole picture use
  *Sharpness* / *Advanced sharpen* in post-processing.
- **Outer DLSS 5** (off by default, with foveation on). Also runs DLSS 5 on
  the whole eye at a low resolution (**Outer resolution**, 35 % by default)
  and puts it under the fovea, so the DLSS 5 look carries on outside the
  fovea and there is no visible edge. The full-resolution fovea still blends
  in through **Softness**. This costs about one more network run at
  that resolution (35 % ≈ 12 % of a full-eye pass), and the whole eye is
  copied through the engine.
- A **GPU cost** estimate for the current settings.

**Post-processing** (the card with the thin red frame and red sliders). A toggle plus
sliders for **Sharpness** (contrast-adaptive), **Small detail** (sharpens small
textures), **FXAA**, **Contrast**, **Saturation** and **Warmth** (cold ← →
warm), and **Reset post-processing**. It applies to the whole eye image
after DLSS 5 and is VR only, like everything else. When it is on, the whole
eye is copied through the engine, which adds a small GPU cost.

- **Advanced sharpen** (new in 3.1): a local-contrast sharpener. The finest
  detail is lifted in proportion to how *flat* its neighbourhood is, so
  texture detail (fabric, foliage, skin, terrain) gets sharper while object
  outlines - which already have high local contrast - are left alone and get
  no halos. Luma only (no colour fringes), soft-limited.
- **SMAA** (new in 3.1): Enhanced Subpixel Morphological Anti-Aliasing by
  Jorge Jimenez et al. (the reference implementation, MIT), as compute
  shaders: edges found on the eye image, blended along their shape - smooth
  slanted edges without FXAA's blur of texture detail. A slider like FXAA
  (3.3): 0 % off, 100 % full SMAA (High preset).
- **Light bloom** (new in 3.1): bright parts of the image glow softly. A
  mip-chain bloom in linear light (13-tap downsampling and tent upsampling,
  as in Jimenez's SIGGRAPH 2014 talk), added with a screen blend so nothing
  clips. **Light bloom** = intensity, **Bloom radius** = how far the glow
  spreads, **Bloom threshold** = how bright a part must be to glow.
- Order: SMAA, Advanced sharpen, Light bloom, then Dehaze, FXAA, Sharpness,
  Small detail and the colour settings. All of them are per game (or *Same
  for all games*), in the app and in the VR panel's *Game* tab, and run
  with or without DLSS 5, in every API and runtime.
- **Small detail** sharpens fine texture detail only (one-pixel structure:
  fabric, foliage, distant text), with a tight limit so edges don't get
  halos. Use it together with, or instead of, **Sharpness**.
- **Independent of DLSS 5** (3.6: always - the old *Run without DLSS 5*
  switch is gone): post-processing keeps running when DLSS 5 is switched off
  (master switch or hotkey), and DLSS-NR is not loaded at all then.

**Hotkeys.** Global keys that work while a game has focus, also inside the
headset. Each one changes the setting for every VR game, exactly like the
switch in the window, and applies within half a second.

| Action | Default |
|---|---|
| DLSS 5 on/off | Ctrl+F9 |
| Cycle style (Standard → Natural → Cinematic) | Ctrl+F10 |
| Cycle passes (1 → 2 → 3) | Ctrl+F11 |
| Foveation on/off | Ctrl+F8 |
| Post-processing on/off | Ctrl+F7 |
| Screenshot (PNG) | Ctrl+F12 |
| Cycle model preset (Default → A → B) | not set |
| Cycle NR resolution (100 → 75 → 50 %) | not set |
| Auto perf. on/off | not set |
| Outer DLSS 5 on/off | not set |
| NR upscaler on/off | not set |
| VR panel open/close | F12 |

Click a key button and press the new key, with Ctrl / Alt / Shift if you
like. **Esc** cancels and **Delete** clears it. A key can only belong to one
action. **Global hotkeys** turns them all off; **Beep** plays a short sound
when one fires, which you hear in the headset. The keys are only watched,
never swallowed, and no keyboard hook goes into any game: the background agent
watches them (it runs elevated, so admin games are covered). When the agent is
not running, the control window does it, and with neither running, the VR
game does. The chip on the card shows which. In `config.ini` the keys are in
`[hotkeys]` (for example `toggle_dlss=ctrl+F9`, or `none`).

**Screenshots.** The screenshot key (or **Take now**) saves the next frame of
both eyes, exactly as the headset gets them (with DLSS 5 and
post-processing), as `<game>_<date>_<time>_left.png` and `_right.png`. They go
to the **Screenshots** folder next to `NeuralRenderingVR.exe`, or to any
folder you pick with **Folder…**; **Open** shows it. If a game can't write
there, the PNGs go to `%LOCALAPPDATA%\NeuralRenderingVR\Screenshots`. The
window shows a message when they are saved. With foveation on and
post-processing off, the frame that is saved is briefly copied as a whole
eye; this doesn't drop the network's history. With DLSS 5 and
post-processing both off, the plain eye image is saved. **Eyes** (app and
VR panel): *Both* saves two PNGs, *Left* or *Right* only that eye. The picture
is the finished eye image - what the headset gets after DLSS 5 and
post-processing - before the compositor's lens distortion, so it looks like a
normal flat image of that eye.

**VR panel** (in the headset). Press **F12** (change it under Hotkeys), or
**Open in headset** in the window's **VR panel** card. A dark,
semi-transparent panel appears in front of you in any VR game: OpenXR,
SteamVR or Oculus, with D3D11, D3D12, Vulkan or OpenGL, 64- or 32-bit. It has
every setting the window has:
- **DLSS 5** on/off (the big red button) and the status line;
- the **DLSS 5** tab (preset, style, passes, temporal history, intensity,
  blend, local tone, structure, mask, skin, UI correction, auto performance);
- the **Foveation** tab (foveation, centre, size, softness, roundness,
  offsets, outline, quad views; NR resolution, upscaler, upscaler detail,
  outer DLSS 5, outer resolution, cost);
- the **Post-processing** tab (on/off, run without DLSS 5, all sliders, reset);
- the **Runtimes** tab (runtimes, NR model status, RTX 20/30/40,
  screenshots; hotkeys and file pickers stay in the window);
- the **Panel** tab (size, left/right, down/up, distance, opacity, reset).

**Screenshot now** is at the top, next to **Close**. Move the mouse to
move the cursor, click to change things, and use the wheel to scroll. The
mouse goes to the panel only while the VR game's window is in front. Alt+Tab
gives it back to the desktop at once. F12, Esc or Close closes the panel. If no
VR game shows the panel for 2.5 seconds, it closes by itself. Every change applies at once and is
saved to `config.ini`, so the window and all other VR games get it too. The
panel is drawn after DLSS 5, post-processing and screenshots, so screenshots
never show it. It's a flat panel at the chosen distance (stereo depth), the same
size in both eyes. The window's **VR panel** card has the same size and place
settings.

**Live.** Every running VR app using Neural Rendering VR: API, graphics API,
NR size, passes, GPU ms and fps.

Advanced options without a UI (resource states, NGX app id, flat depth value)
live in `%LOCALAPPDATA%\NeuralRenderingVR\config.ini`, section `[advanced]`.

## Behaviour notes

- **First frames of a game:** the DLSS-NR runtime loads in the background, so
  the headset never freezes. Frames pass through unprocessed for the second or
  two this takes.
- **Unreal Engine games:** if you pick the launcher `.exe` in the game's root,
  the installer finds the real binary in `<Project>\Binaries\Win64` and
  installs the hook there.
- **Old Oculus SDK games:** both LibOVR layer layouts (pre-1.25 and 1.25+)
  are detected per frame, as are EyeFov, EyeFovDepth, EyeFovMultires and
  EyeMatrix layers.
- **Virtual screens:** when an OpenXR app shows no 3D scene, only large quad
  layers (menus and cutscenes of flat-to-VR mods), those screens are processed
  with static history. `[advanced] xr_quad_screens=0` turns this off.
- **Eye image formats:** RGBA8, BGRA8 (Unreal, UEVR, many Oculus games),
  RGB10A2, RGBA16F and R11G11B10F, sRGB or not. When the GPU can't write a
  format from a compute shader (often BGRA8), the engine writes it with a small
  render-target pass instead. The Self-test checks that path too.
- **Several projection layers per frame:** the scene is the layer whose
  swapchains were drawn this frame, opaque, and largest. (UEVR adds a dummy
  layer first when Virtual Desktop is running.)
- **Luke Ross R.E.A.L. VR** and **vrframework** mods install themselves as the
  game's `dxgi.dll`, so Neural Rendering VR's per-game fallback uses
  `version.dll` there (theirs is never replaced). The universal install
  (agent) is the better choice for these mods.
- **Alternate-eye rendering** (one eye new per frame) is recognised in every
  runtime: the eye that is not new (its image or its pose unchanged from the
  last frame while the other eye moved on) is not processed again where that
  can be seen, and frame generation makes each eye from its own frames, both eyes at the
  same moment (see *Frame generation*). The log says when it happens and when
  both eyes are new again.
- **Switching runtimes inside one game** (UEVR): the OpenVR / Oculus hook's
  claim on a process expires 2 s after its last frame, so the OpenXR layer
  takes over by itself.
- **Runtime-internal calls are ignored.** Meta's OpenXR runtime lives in
  `LibOVRRT64_1.dll` and SteamVR's in `vrclient_x64.dll`. Their own calls into
  LibOVR / OpenVR are never taken for a game's frames, and the LibOVR hook
  stands aside in any process that runs an OpenXR session.

## Troubleshooting

- **Diagnostics:** `NeuralRenderingVR.exe → Diagnostics` writes
  `NeuralRenderingVR-diagnostics.txt`: install state, every OpenXR API layer on the
  system, the active runtime, HAGS, and the end of every log. Send that file
  when asking for help.
- **Logs:** `NeuralRenderingVR.exe → Open logs`, which is
  `%LOCALAPPDATA%\NeuralRenderingVR\logs`. There's one file per game and path:
  `openxr-<game>.log`, `hook-<game>.log`, `selftest-NeuralRenderingVR.exe.log`. For a
  mod with a separate VR host process, look for `openxr-<host>.log` (e.g.
  `openxr-ACUnityVRHost.exe.log`). Its first frames log
  `processed eye ... of swapchain ...` or `NOT processed ...`.
- **"nvngx_dlssnr.dll not found":** pick it with **Browse…** in the green NR
  model bar at the top of the window (see *Getting the NR model*).
- **"NGX init failed":** turn on hardware-accelerated GPU scheduling, update
  the NVIDIA driver, check that the DLL is a DLSS‑NR runtime and your GPU is
  supported (RTX 20/30/40: use the patched model). Run the Self‑test.
- **Foveated DLSS 5 drags or smears when you turn your head:** look in the
  game's `openxr-<game>.log` for `rendered with a camera of its own`. Since
  2.8.1 DLSS 5's motion and the fovea follow the camera the game really
  renders with (NieR VR, Alan Wake VR, OpenComposite games use their own);
  `[advanced] fovea_guard` (default 0.05) is the hidden margin DLSS 5 gets
  around the fovea.
- **The VR panel's cursor does not move in a viewer app** (Osiris VR Viewer,
  desktop viewers): since 2.9.0 a VR app without a window of its own gets the
  mouse while the panel is open; otherwise switch on *Mouse always to the
  panel*.
- **The VR panel's cursor does not move:** look at the `panel:` lines in
  `agent-NeuralRenderingVR-Agent.exe.log`. Every 10 s it counts the mouse
  events it got (Raw Input / hook); "another mouse hook takes the events
  first" or "the game runs as administrator" say what is in the way.
- **A mod switches all OpenXR layers off** (AC Unity VR's host after one
  failed start, Dishonored VR): the agent switches Neural Rendering VR's layer
  back on in that process while it starts (`agent: ... switched back on`).
  `[advanced] keep_layer_switch_off=1` leaves it off.
- **The VR panel does not appear:** the game must show up under **Live**.
  Games with anti-cheat, and games where another DLSS 5 mod already runs, are
  left alone on purpose, so the panel can't appear there either. If F12 is
  also Steam's screenshot key, give the panel another key under Hotkeys.
- **A native SteamVR / Oculus game shows nothing in Live:** check that the agent
  is running (VR runtimes card: "Universal · running"; NeuralRenderingVR.exe starts it
  if needed) and look at `agent-NeuralRenderingVR-Agent.exe.log`. Its first line says
  whether it runs elevated. A game "-> hook loaded" line means the hook is in;
  then `hook-<game>.log` shows which compositor / LibOVR calls it saw.
  Anti-cheat protected games refuse injection; that's by design.
- **After an update the old behaviour is still there:** the VR runtimes card
  says *Layers out of date*. Click **Reinstall layers**, then restart the VR
  game.
- **Image too dark/bright or the wrong colours on a D3D12 or Vulkan game:**
  some engines hand over textures in an unusual state. Try a different
  `d3d12_state_*` / `vk_layout_*` under `[advanced]`.
- **Disable the OpenXR layer for one launch:** set the environment variable
  `DISABLE_XR_APILAYER_NEURALRENDERINGVR=1`.
- **Vulkan SteamVR / Oculus game: "VkDevice lacks VK_KHR_external_memory_win32"**
  in its hook log: the Vulkan helper layer is not installed (installer card
  "Vulkan helper layer") or the game was already running when it was
  installed. Reinstall layers, restart the game. The layer only touches
  processes with a VR runtime loaded; `DISABLE_NEURALRENDERINGVR_VK_LAYER=1` turns it
  off for one launch (anti-cheat games that object to Vulkan layers).
- **A D3D11, 32-bit or OpenGL game shows nothing:** run **Self-test**. Its
  line "D3D11 / 32-bit / OpenGL games: sharing ..." says whether this PC can
  share images between D3D11 and the DLSS engine, in which direction, with the
  error codes. Send it along with Diagnostics.
- **A game crashes:** its `hook-<game>.log` / `openxr-<game>.log` ends with an
  `exception ... at <module>+<offset>; stack: ...` line. "Neural Rendering VR involved"
  means a Neural Rendering VR module was on the stack: send that log.
- **Games with their own DLSS** (RE Engine, Streamline games) run DLSS 5 in
  `NeuralRenderingVR-EngineHost.exe` (log: "running DLSS 5 in NeuralRenderingVR-EngineHost.exe").
  `[advanced] engine_host=0` forces the old in-process engine, `=1` uses the
  host for every game.
- **Too slow / stutters:** turn on **Auto performance**, or lower passes,
  fovea size and NR resolution yourself. On Pimax-class resolutions (about
  1900×1950 per eye and up), start with 1 pass and foveation on.

## Uninstall

`NeuralRenderingVR-LayerInstaller.exe` → **Uninstall**, then **Remove** any per-game
entries. Then delete the folder and `%LOCALAPPDATA%\\NeuralRenderingVR`. Hook files
still loaded in a running game are removed at the next reboot. Scripted:
`NeuralRenderingVR-LayerInstaller.exe --uninstall-all`; install with `--install`.

## How it works (short)

- **One engine per GPU, on its own D3D12 device.** The game's eye region is
  copied into a shared texture. DLSS‑NR (NGX feature 18) runs on it, and the
  result is blended back with a feathered fovea mask. All synchronisation is
  GPU‑side through shared fences, so the game's CPU thread never waits. D3D11
  uses `ID3D11Device5` fences; Vulkan imports the D3D12 textures and fences
  through `VK_KHR_external_memory_win32` / `external_semaphore_win32`. Neural Rendering VR
  adds those extensions to the game's VkDevice automatically.
- **Hook points.** OpenXR: `xrReleaseSwapchainImage`, with eye layout from
  `xrEndFrame`. OpenVR: `IVRCompositor::Submit`. LibOVR:
  `ovr_CommitTextureSwapChain`. Each runs right before the VR runtime takes the
  image.
- **Motion vectors** come from the eye orientation delta between frames
  (rotation‑only reprojection). Depth is flat, as with any image‑only use of
  DLSS‑NR.

Details for developers: [ARCHITECTURE.md](ARCHITECTURE.md).

## Building from source

MinGW‑w64 (GCC 13+), on Linux or Windows/MSYS2:

```
./build.sh                       # x64 + x86 -> build/ and dist/NeuralRenderingVR/
./tests/build_tests.sh           # optional tests (fake runtimes, 64- and 32-bit)
# MSYS2: CXX64/CC64 (UCRT64 or MINGW64 g++/gcc), CXX32/CC32 (MINGW32), WINDRES
```

`tools/gen_proxy.py` regenerates the dxgi/version forwarding stubs.

## Legal notes

Not legal advice. These are the points to know before using or redistributing
Neural Rendering VR.

- **Its own code.** Neural Rendering VR is GPL-3.0-or-later. It contains no
  code from NeuralScreen (PolyForm Strict) and no NVIDIA code. See *Credits*
  for what it learned from other projects and how that was checked.
- **NVIDIA's DLL is not included and must not be redistributed with it.**
  You supply `nvngx_dlssnr.dll` yourself, under the terms you got it with.
- **Two compatibility measures touch how that DLL sees its surroundings:**
  - *Caller name* (always on, required): the DLL serves only callers named
    like NVIDIA's NGX loader (`nvngx.dll`), so Neural Rendering VR reports
    that name for its own module, to that DLL only. CheekyFoveatedDLSS and
    similar tools do the same.
  - *RTX 20/30/40* (opt-in, off by default): see Requirements.

  NVIDIA's RTX SDK licence (section 4) forbids licensees to "bypass, disable,
  or circumvent any technical limitation" of the SDK. If you agreed to that
  licence, or got the DLL under similar terms, these measures may conflict
  with it. That is a contract question between you and NVIDIA. Decide for
  yourself, and keep the RTX 20/30/40 option off if in doubt.
- **Anti-cheat.** Neural Rendering VR works inside VR games. Don't use it in
  online games with anti-cheat. In a game with a known anti-cheat module
  loaded (Easy Anti-Cheat, BattlEye, Vanguard, nProtect GameGuard, XIGNCODE
  and others) the agent never injects and the OpenXR layer stays inactive,
  but the list can't be complete; turn the matching runtime toggle off for
  such games to be sure.
- **Trademarks.** NVIDIA, DLSS and RTX (NVIDIA), SteamVR and OpenVR (Valve),
  Oculus and Meta (Meta), OpenXR and Vulkan (Khronos) are named only to say
  what Neural Rendering VR works with. It is not affiliated with or endorsed
  by any of them.
- **Name change.** Up to 1.7.1 the app was called NeuralVR. Installing 1.8
  removes the old NeuralVR agents, layers and files and keeps your settings.

## Credits and license

Neural Rendering VR is free software under the **GNU GPL v3.0 or later** (see `LICENSE`).

- **Frame generation:** the *FidelityFX* method follows the approach of AMD's
  FidelityFX frame interpolation and optical flow (method only, own shaders);
  **RIFE** is by Zhewei Huang (hzwer) et al. (MIT), in nihui's
  rife-ncnn-vulkan conversion (MIT, downloaded by the installer, not
  included); **OFXR-Bridge** by tig3rmast3r and djules75 inspired universal
  VR frame generation with both methods and the RIFE installer (no code
  used). Details in `THIRD_PARTY_NOTICES.md`.

- **[CheekyFoveatedDLSS](https://github.com/ClarkCheekyKent/CheekyFoveatedDLSS)**
  (GPL‑3.0) by ClarkCheekyKent is the reference for the DLSS‑NR feature
  contract: the feature id, the `DLSSNR.*` parameter names, the caller‑identity
  requirement, the LibOVR layer ABI, and the idea of foveating DLSS‑NR in VR.
- **[NeuralScreen](https://github.com/perseval-BLR/NeuralScreen)** by
  perseval‑BLR inspired the idea of running DLSS‑NR on a finished image, and
  its documentation reported that shipped NR runtimes gate on the GPU
  architecture and that extra passes darken the image slightly. NeuralScreen
  is under the PolyForm Strict licence, which does not allow modified or
  derived versions, so Neural Rendering VR uses none of its code. Up to 1.7.0
  (then named NeuralVR), the GPU architecture handling followed NeuralScreen's
  implementation too closely; 1.7.1 replaced it with a new design (an
  import-table filter inside the NR runtime, with the values from NVIDIA's
  public NVAPI reference). Do not redistribute NeuralVR 1.7.0 or older.
  The 1.8.0 sources were compared with NeuralScreen's (12-token sequences of
  code, 9-word sequences of text and comments): the only matches are generic
  Direct3D / Windows API calls, `#include` lists and NVAPI's public struct
  layout.
- Third‑party components: see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
