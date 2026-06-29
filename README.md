# FFT-Style Ocean – Godot 4

A realistic Gerstner Wave ocean simulation for Godot 4.3+.

## Quick Start

1. Open Godot 4x or later.
2. Click **Import** and select this folder's `project.godot`.
3. Press **F5** (or the Play button) to run.

## Controls (in game)

| Input | Action |
|---|---|
| Left-drag | Orbit camera |
| Scroll wheel | Zoom in / out |
| (Auto) | Slow auto-rotation |

## Project Structure

```
fft_ocean/
├── ocean/
│   ├── ocean.gdshader       ← GPU Gerstner wave shader
│   └── ocean_mesh.gd        ← Inspector-driven script
├── scenes/
│   └── ocean_scene.tscn     ← Ready-to-run scene
├── scripts/
│   └── camera_controller.gd ← Orbit camera
└── project.godot
```

## All Customisable Properties

Select **OceanMesh** in the scene tree to see every property in the Inspector.

### Mesh
| Property | Default | Description |
|---|---|---|
| `mesh_size` | 300 | World-unit width/depth of the ocean plane |
| `mesh_subdivisions` | 256 | Vertex resolution (higher = smoother, more GPU cost) |

### Global Wave Controls
| Property | Default | Description |
|---|---|---|
| `wave_speed` | 1.5 | Overall animation speed multiplier |
| `wave_scale` | 1.0 | Scales all wavelengths uniformly — increase for calmer/larger ocean |
| `amplitude_mul` | 1.0 | Global wave height multiplier |
| `choppiness` | 1.0 | Horizontal crest displacement (0 = sine-like, 2 = very choppy) |
| `gravity` | 9.81 | Physics gravity — affects propagation speed (lower = slower waves) |

### Wave A–D (each has identical controls)
| Property | Description |
|---|---|
| `wx_enabled` | Toggle this wave layer on/off |
| `wx_direction` | 2D travel direction (auto-normalised) |
| `wx_steepness` | 0–1 — how peaked the crest is (>0.5 can cause folding/foam) |
| `wx_wavelength` | Distance between crests in world units |

Suggested roles:
- **A** — long ocean swell (high wavelength, low steepness)
- **B** — cross-swell (medium wavelength, different direction)
- **C** — chop (short wavelength, medium steepness)
- **D** — surface ripple (very short wavelength, low steepness)

### Foam
| Property | Default | Description |
|---|---|---|
| `foam_threshold` | 1.2 | Jacobian cutoff — lower = more foam |
| `foam_scale` | 2.5 | Size of the foam noise pattern |
| `foam_strength` | 1.0 | Overall foam opacity multiplier |
| `foam_roughness` | 0.6 | Surface roughness in foamy areas |

### Colors
| Property | Description |
|---|---|
| `color_shallow` | Water color at wave crests / near surface |
| `color_deep` | Water color in troughs / deep |
| `color_foam` | Whitecap / foam color |
| `depth_blend` | 0–1 — how strongly depth affects color |

### Surface
| Property | Default | Description |
|---|---|---|
| `metallic` | 0.05 | PBR metallic factor |
| `roughness` | 0.08 | Specular spread (low = mirror-like) |
| `specular_str` | 0.5 | Specular intensity |
| `fresnel_power` | 4.0 | Fresnel falloff sharpness |
| `fresnel_str` | 0.4 | Fresnel reflection brightness |
| `emission_str` | 0.04 | Subtle backlit glow on crests |
| `transparency` | 0.0 | 0 = opaque, 1 = fully transparent |

## Preset Ideas

**Stormy Sea:** `wave_speed=3.0`, `amplitude_mul=2.5`, `choppiness=1.8`, `foam_threshold=0.8`, all waves on  
**Calm Lagoon:** `wave_speed=0.6`, `amplitude_mul=0.3`, `choppiness=0.3`, `foam_strength=0.0`, only Wave A+B  
**Alien Ocean:** swap colors to reds/purples, `gravity=2.0`, `wave_speed=0.4`  
**Arctic:** `color_shallow=(0.7,0.85,0.9)`, `color_deep=(0.3,0.55,0.7)`, `foam_strength=1.5`

------------------

two types of files
the not merged one which has all the deep water material calculations and the other one which can be used on ponds and rivers because the
material is being calculated with alpha or transparency or basically the not merged one doesnt have to do with alpha and stuff and the merged has something to do with alpha
