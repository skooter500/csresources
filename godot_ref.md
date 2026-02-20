# Godot 4 Quick Reference

## Keyboard Shortcuts

| Key | Use |
|-----|-----|
| F5 | Run project |
| F6 | Run current scene |
| F7 | Resume after pause |
| F8 | Stop |
| F9 | Toggle breakpoint |
| F10 | Step over |
| F11 | Step into |
| Ctrl + A | Add new node |
| Ctrl + D | Duplicate node |
| Ctrl + Shift + A | Instantiate scene |
| Ctrl + S | Save |
| Ctrl + K | Comment line |
| Ctrl + F | Search file |
| Ctrl + R | Search/Replace file |
| Ctrl + Shift + F | Find in files |
| Ctrl + Shift + R | Replace in files |
| Ctrl + Shift + F11 | Maximise editor |
| Ctrl + \ | Recent files |
| Ctrl + F1 | Switch to 2D |
| Ctrl + F2 | Switch to 3D |
| Ctrl + F3 | Switch to Script |
| Alt + D | Toggle bottom panel |
| F | Focus selected in viewport |
| Q / W / E / R | Select / Move / Rotate / Scale gizmo |

## Nodes

### Core
| Node | Purpose |
|------|---------|
| Node | Base class, no transform |
| Node3D | 3D transform |
| Node2D | 2D transform (position, rotation float, scale) |
| Timer | Emits `timeout` signal on interval |

### 3D Physics
| Node | Purpose |
|------|---------|
| StaticBody3D | Immovable collider (world geometry) |
| RigidBody3D | Physics-simulated body |
| CharacterBody3D | Kinematic body (`move_and_slide`) |
| Area3D | Detect overlaps, no physics response |
| CollisionShape3D | Collision shape — set `Shape` property |

### 3D Rendering
| Node | Purpose |
|------|---------|
| MeshInstance3D | Renders a 3D mesh |
| Camera3D | 3D camera |
| DirectionalLight3D | Sun-like directional light |
| OmniLight3D | Point light |
| SpotLight3D | Cone light |
| GPUParticles3D | GPU particle system |
| CSGBox3D / CSGSphere3D | Constructive solid geometry |

### 3D Navigation & Path
| Node | Purpose |
|------|---------|
| Path3D | Defines a Curve3D path |
| PathFollow3D | Moves along a Path3D |
| NavigationAgent3D | Pathfinding agent |
| NavigationRegion3D | Baked navmesh region |

### 2D Physics & Rendering
| Node | Purpose |
|------|---------|
| StaticBody2D | Immovable 2D collider |
| RigidBody2D | 2D physics body |
| CharacterBody2D | Kinematic 2D body |
| Area2D | 2D overlap detection |
| CollisionShape2D | 2D collision shape |
| Sprite2D | 2D texture/sprite |
| AnimatedSprite2D | Frame-based 2D animation |
| TileMap | 2D tile-based levels |

### XR / VR
| Node | Purpose |
|------|---------|
| XROrigin3D | World origin for XR |
| XRCamera3D | Tracked headset camera |
| XRController3D | Tracked controller |

### UI (Control nodes)
| Node | Purpose |
|------|---------|
| Control | Base UI node |
| Label | Display text |
| Button | Clickable button |
| VBoxContainer / HBoxContainer | Stack children vertically/horizontally |
| ProgressBar | Visual progress bar |
| TextureRect | Display a texture in UI |

### Audio
| Node | Purpose |
|------|---------|
| AudioStreamPlayer | Non-positional audio |
| AudioStreamPlayer3D | Positional 3D audio |

## Transforms

| Task | Code |
|------|------|
| Set position | `position = Vector3(x,y,z)` or `global_position = ...` |
| Translate | `translate(v)`, `move_and_slide()`, `move_and_collide(v)` |
| Rotate | `rotate_x/y/z(angle)`, `rotate(axis, angle)` |
| Set rotation | `rotation = Vector3(x,y,z)` (radians) |
| Look at target | `look_at(target_pos, Vector3.UP)` |
| Set scale | `scale = Vector3(x,y,z)` |
| Local ↔ World | `to_global(local_pos)`, `to_local(global_pos)` |
| Basis from quat | `Basis(quaternion)` |
| Slerp rotation | `basis.slerp(target_basis, t)` |

## Referencing Nodes

```python
$Timer                              # by name
$"../Sibling"                       # relative path
get_parent()
find_child("Name")
get_node("/root/Main/Player")
get_tree().root
get_tree().quit()
get_tree().change_scene_to_file("res://scene.tscn")

@onready var cam: Camera3D = $Camera3D
@onready var path: Path3D = get_node("../Path3D")
```

## Particle Systems

| Property | Meaning |
|----------|---------|
| ProcessMaterial | Shader controlling particle behaviour |
| DrawPass | What each particle looks like (mesh + material) |
| Amount | Total particle count |
| Lifetime | How long each particle lives |
| Emission Shape | Where particles spawn |
| Explosiveness | 0 = steady stream, 1 = all at once |
| Randomness | Timing randomness |
| One Shot | Fire once then stop |
| Preprocess | Fast-forward simulation on start |

## GDScript

```python
# Variables & types
var i: int = 0
var f: float = 0.0
var s: String = "hello"
var v: Vector3 = Vector3(1, 2, 3)
var arr: Array = []
var dict: Dictionary = {}
const MAX: int = 100

# Signals
signal health_changed(new_val: int)
emit_signal("health_changed", hp)
some_node.health_changed.connect(_on_health_changed)

# Coroutines / await
await get_tree().create_timer(2.0).timeout
await get_tree().process_frame

# Instantiate a PackedScene (prefab)
@export var bullet_scene: PackedScene
var b = bullet_scene.instantiate()
add_child(b)

# Control flow
if condition:
    pass
elif other:
    pass
else:
    pass

match value:
    1: pass
    "hello": pass
    _: pass          # default

for i in range(10): pass
for item in array: pass
while condition: pass

# Functions & classes
func my_func(a: int, b: float) -> String:
    return str(a + b)

class_name MyClass extends Node3D

# Annotations
@export var speed: float = 5.0
@onready var mesh: MeshInstance3D = $Mesh
@tool   # runs in editor
```

| Code | Description |
|------|-------------|
| `Input.is_action_pressed("ui_accept")` | Check input action |
| `Input.get_axis("left", "right")` | -1 to 1 axis input |
| `delta` | Time since last frame |
| `lerp(a, b, t)` | Linear interpolate |
| `randf_range(min, max)` | Random float in range |
| `randi() % n` | Random int 0..n-1 |
| `a.dot(b)` | Dot product |
| `a.cross(b)` | Cross product |
| `v.normalized()` | Unit vector |
| `v.length()` | Magnitude |
| `a.distance_to(b)` | Distance |
| `a.angle_to(b)` | Angle between vectors |
| `v.clamp(min, max)` | Clamp vector magnitude |
| `basis * vector` | Transform a vector by a basis |
| `Vector3.UP / RIGHT / FORWARD` | World axis constants |
| `DebugDraw3D.draw_sphere(pos, r, color)` | Debug sphere |
| `DebugDraw3D.draw_line(a, b, color)` | Debug line |
