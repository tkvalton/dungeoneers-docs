---
layout: default
title: Rig
parent: Entity System
nav_order: 2
has_children: true
permalink: /systems/entities/rig/
---

# Rig

Inherits: [Node3D](https://docs.godotengine.org/en/stable/classes/class_node3d.html)

## Child Classes
- [EntityRig](./entity-rig.md)
- [ModularCompanionRig](./modular-companion-rig.md)

## Description

RigController manages the visual representation, animations, and attachments for entities in the game. It serves as the central hub for handling mesh instances, outline effects, remote transforms for VFX, and various visual states of the entity.

Key features:
- Manages mesh instances and their materials
- Handles outline effects for selection and targeting
- Manages attachment points for weapons and VFX
- Controls casting VFX and transparency effects
- Integrates with the game's selection and targeting systems
- Holds the AnimationPlayer for the entity

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | [outline_eligible](#outline_eligible) | true | If true, can show selection outline |
| bool | [is_transparent](#is_transparent) | false | If true, uses transparent materials |

### General Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Entity | [rig_entity](#rig_entity) | null | Reference to owning entity |
| Array[MeshInstance3D] | [mesh_instances](#mesh_instances) | [] | All mesh instances in rig |
| Node3D | [hand_slot_right](#hand_slot_right) | null | Right hand attachment point |
| Node3D | [hand_slot_left](#hand_slot_left) | null | Left hand attachment point |
| Node3D | [head_slot](#head_slot) | null | Head attachment point |
| Node3D | [chest_slot](#chest_slot) | null | Chest attachment point |
| MeshInstance3D | [main_hand](#main_hand) | null | Main hand weapon mesh |
| MeshInstance3D | [off_hand](#off_hand) | null | Off hand weapon mesh |
| GPUParticles3D | [right_hand_cast_vfx](#right_hand_cast_vfx) | null | Right hand casting effects |
| GPUParticles3D | [left_hand_cast_vfx](#left_hand_cast_vfx) | null | Left hand casting effects |
| Dictionary | [remote_transforms](#remote_transforms) | {} | Remote transform points |
| Array[RemoteTransform3D] | [active_remotes](#active_remotes) | [] | Active remote transforms |
| AnimationPlayer | [animation_player](#animation_player) | null | Animation controller |

### Node References

| Type | Property | Description |
|------|----------|-------------|
| Skeleton3D | [skeleton_3d](#skeleton_3d) | Main skeleton reference |
| Decal | [hitbox_outline](#hitbox_outline) | Combat hitbox display |
| Decal | [target_marker](#target_marker) | Target indicator |
| Decal | [selection_marker](#selection_marker) | Selection indicator |

## Constants

| Name | Value | Description |
|------|-------|-------------|
| OUTLINE_SELECTION_ENAMY_MATERIAL | preload("...") | Enemy outline material |
| OUTLINE_SELECTION_FRIENDLY_MATERIAL | preload("...") | Friendly outline material |
| OUTLINE_SELECTION_HOVER_MATERIAL | preload("...") | Hover outline material |
| OUTLINE_SELECTION_NORMAL_MATERIAL | preload("...") | Default outline material |
| OUTLINE_SELECTION_NORMAL_TRANSPARENT_ENTITIES_MATERIAL | preload("...") | Transparent outline material |
| OUTLINE_SELECTION_PLAYER_MATERIAL | preload("...") | Player outline material |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [initialize_rig](#initialize_rig) | Initializes the rig |
| void | [connect_signals](#connect_signals) | Connects entity signals |
| void | [set_attachment_slots](#set_attachment_slots) | Sets up attachment points |
| void | [_setup_entity_animation_player](#_setup_entity_animation_player) | Sets up animation system |
| void | [create_remote_transforms](#create_remote_transforms) | Creates remote transform points |
| void | [create_remotes_for_slot](#create_remotes_for_slot) | Creates transforms for a slot |
| RemoteTransform3D | [assign_remote_transform](#assign_remote_transform) | Assigns transform to VFX |
| RemoteTransform3D | [find_available_remote](#find_available_remote) | Finds unused remote transform |
| void | [release_remote](#release_remote) | Releases a remote transform |
| void | [build_mesh_instances_array](#build_mesh_instances_array) | Builds mesh instance array |
| void | [_on_entity_combat_state_changed](#_on_entity_combat_state_changed) | Updates combat visuals |
| void | [_on_entity_selection_state_changed](#_on_entity_selection_state_changed) | Updates selection visuals |
| void | [set_highlight_overlay](#set_highlight_overlay) | Sets outline material |
| bool | [can_update_outline](#can_update_outline) | Checks if outline can update |
| void | [update_nameplate](#update_nameplate) | Updates nameplate color |
| void | [set_mesh_override](#set_mesh_override) | Sets material override |
| void | [clear_mesh_override](#clear_mesh_override) | Clears material override |
| void | [animate_transparency_off](#animate_transparency_off) | Animates to opaque |
| void | [animate_transparency_on](#animate_transparency_on) | Animates to transparent |
| void | [start_cast_vfx](#start_cast_vfx) | Starts casting effects |
| void | [stop_cast_vfx](#stop_cast_vfx) | Stops casting effects |


# Property Descriptions

## Exported Properties

#### outline_eligible
{: #outline_eligible }

bool **outline_eligible** = `true`
* bool **is_outline_eligible**()
* void **set_outline_eligible**(value: bool)

Determines if the entity can display selection outlines. Controls visibility of highlight overlays and material effects.

---

#### is_transparent
{: #is_transparent }

bool **is_transparent** = `false`
* bool **is_transparent**()
* void **set_is_transparent**(value: bool)

If true, entity uses transparent materials and special outline handling.

## General Properties

#### rig_entity
{: #rig_entity }

Entity **rig_entity**
* Entity **get_rig_entity**()
* void **set_rig_entity**(value: Entity)

Reference to the entity this rig belongs to. Used for team checks, combat state, and selection handling.

---

#### mesh_instances
{: #mesh_instances }

Array[MeshInstance3D] **mesh_instances** = `[]`
* Array[MeshInstance3D] **get_mesh_instances**()
* void **set_mesh_instances**(value: Array[MeshInstance3D])

Collection of all mesh instances in the rig. Used for material and transparency effects.

---

#### hand_slot_right
{: #hand_slot_right }

Node3D **hand_slot_right**
* Node3D **get_hand_slot_right**()
* void **set_hand_slot_right**(value: Node3D)

Right hand attachment point for weapons and effects.

---

#### hand_slot_left
{: #hand_slot_left }

Node3D **hand_slot_left**
* Node3D **get_hand_slot_left**()
* void **set_hand_slot_left**(value: Node3D)

Left hand attachment point for weapons and effects.

---

#### head_slot
{: #head_slot }

Node3D **head_slot**
* Node3D **get_head_slot**()
* void **set_head_slot**(value: Node3D)

Head attachment point for equipment and effects.

---

#### chest_slot
{: #chest_slot }

Node3D **chest_slot**
* Node3D **get_chest_slot**()
* void **set_chest_slot**(value: Node3D)

Chest attachment point for armor and effects.

---

#### main_hand
{: #main_hand }

MeshInstance3D **main_hand**
* MeshInstance3D **get_main_hand**()
* void **set_main_hand**(value: MeshInstance3D)

Main hand weapon mesh instance.

---

#### off_hand
{: #off_hand }

MeshInstance3D **off_hand**
* MeshInstance3D **get_off_hand**()
* void **set_off_hand**(value: MeshInstance3D)

Off hand weapon mesh instance.

---

#### right_hand_cast_vfx
{: #right_hand_cast_vfx }

GPUParticles3D **right_hand_cast_vfx**
* GPUParticles3D **get_right_hand_cast_vfx**()
* void **set_right_hand_cast_vfx**(value: GPUParticles3D)

Particle effects for right hand casting.

---

#### left_hand_cast_vfx
{: #left_hand_cast_vfx }

GPUParticles3D **left_hand_cast_vfx**
* GPUParticles3D **get_left_hand_cast_vfx**()
* void **set_left_hand_cast_vfx**(value: GPUParticles3D)

Particle effects for left hand casting.

---

#### remote_transforms
{: #remote_transforms }

Dictionary **remote_transforms** = `{"base": [], "head": [], "chest": [], "hand_right": [], "main_hand": []}`
* Dictionary **get_remote_transforms**()
* void **set_remote_transforms**(value: Dictionary)

Collection of remote transform points organized by attachment slot.

---

#### active_remotes
{: #active_remotes }

Array[RemoteTransform3D] **active_remotes** = `[]`
* Array[RemoteTransform3D] **get_active_remotes**()
* void **set_active_remotes**(value: Array[RemoteTransform3D])

Currently active remote transforms being used by effects.

---

#### animation_player
{: #animation_player }

AnimationPlayer **animation_player** = `null`
* AnimationPlayer **get_animation_player**()
* void **set_animation_player**(value: AnimationPlayer)

Controller for entity animations. Set up by child classes.

## Node References

#### skeleton_3d
{: #skeleton_3d }

Skeleton3D **skeleton_3d**
* Skeleton3D **get_skeleton_3d**()
* void **set_skeleton_3d**(value: Skeleton3D)

Reference to entity's main skeleton for animations and attachments.

---

#### hitbox_outline
{: #hitbox_outline }

Decal **hitbox_outline**
* Decal **get_hitbox_outline**()
* void **set_hitbox_outline**(value: Decal)

Combat state hitbox visualization.

---

#### target_marker
{: #target_marker }

Decal **target_marker**
* Decal **get_target_marker**()
* void **set_target_marker**(value: Decal)

Visual indicator for targeted entities.

---

#### selection_marker
{: #selection_marker }

Decal **selection_marker**
* Decal **get_selection_marker**()
* void **set_selection_marker**(value: Decal)

Visual indicator for selected entities.


## Method Descriptions

#### initialize_rig
{: #initialize_rig }

void **initialize_rig**(entity: Entity)

Initializes the rig with an entity reference.

Parameters:
* entity: Entity - Entity to initialize rig for

Implementation:
* Sets rig_entity reference
* Connects signals
* Sets up attachment slots
* Creates remote transforms
* Builds mesh instances array
* Sets initial highlight overlay

---

#### connect_signals
{: #connect_signals }

void **connect_signals**()

Connects necessary entity signals for combat and selection state changes.

---

#### _setup_entity_animation_player
{: #_setup_entity_animation_player }

void **_setup_entity_animation_player**()

Sets up the animation player system. To be overridden in child classes.

---

#### create_remote_transforms
{: #create_remote_transforms }

void **create_remote_transforms**()

Creates remote transform points for all attachment slots:
- Base transforms
- Head slot transforms
- Chest slot transforms
- Hand slot transforms
- Main hand transforms

---

#### create_remotes_for_slot
{: #create_remotes_for_slot }

void **create_remotes_for_slot**(key: String, parent: Node3D, count: int)

Creates a specified number of remote transforms for a given slot.

Parameters:
* key: String - Slot identifier
* parent: Node3D - Parent node
* count: int - Number of transforms to create

---

#### assign_remote_transform
{: #assign_remote_transform }

RemoteTransform3D **assign_remote_transform**(effect_vfx: EffectVFX, slot: String)

Assigns a remote transform to an effect VFX.

Parameters:
* effect_vfx: EffectVFX - Effect to assign transform to
* slot: String - Slot to use for transform

Returns: RemoteTransform3D or null if no transform available

---

#### find_available_remote
{: #find_available_remote }

RemoteTransform3D **find_available_remote**(slot: String)

Finds an unused remote transform for a given slot.

Parameters:
* slot: String - Slot to search in

Returns: RemoteTransform3D or null if none available

---

#### release_remote
{: #release_remote }

void **release_remote**(remote: RemoteTransform3D)

Releases a remote transform, making it available for reuse.

Parameters:
* remote: RemoteTransform3D - Transform to release

---

#### build_mesh_instances_array
{: #build_mesh_instances_array }

void **build_mesh_instances_array**(node: Node)

Recursively builds array of all mesh instances in the rig.

Parameters:
* node: Node - Starting node for recursion

---

#### _on_entity_combat_state_changed
{: #_on_entity_combat_state_changed }

void **_on_entity_combat_state_changed**(state: int)

Updates visual elements based on combat state.

Parameters:
* state: int - New combat state

---

#### _on_entity_selection_state_changed
{: #_on_entity_selection_state_changed }

void **_on_entity_selection_state_changed**(is_current: bool, is_selected: bool)

Updates selection marker based on selection state.

Parameters:
* is_current: bool - If currently selected
* is_selected: bool - If in selection group

---

#### set_highlight_overlay
{: #set_highlight_overlay }

void **set_highlight_overlay**(status: int)

Sets mesh overlay based on entity status:
* 0: Normal material
* 1: Hover material
* 2: No material
* 3: Team-based material

Parameters:
* status: int - Highlight status

---

#### can_update_outline
{: #can_update_outline }

bool **can_update_outline**()

Checks if outline can be updated based on current conditions.

Returns: bool - True if outline can be updated

---

#### update_nameplate
{: #update_nameplate }

void **update_nameplate**(color: int)

Updates nameplate border color.

Parameters:
* color: int - Color index to use

---

#### set_mesh_override
{: #set_mesh_override }

void **set_mesh_override**(material: Material)

Sets material override for all mesh instances.

Parameters:
* material: Material - Override material

---

#### clear_mesh_override
{: #clear_mesh_override }

void **clear_mesh_override**(material: Material)

Clears specific material override from mesh instances.

Parameters:
* material: Material - Material to clear

---

#### animate_transparency_off
{: #animate_transparency_off }

void **animate_transparency_off**()

Animates mesh instances to fully opaque over 1.5 seconds.

---

#### animate_transparency_on
{: #animate_transparency_on }

void **animate_transparency_on**()

Animates mesh instances to fully transparent over 1.5 seconds.

---

#### start_cast_vfx
{: #start_cast_vfx }

void **start_cast_vfx**()

Starts casting visual effects on both hands.

---

#### stop_cast_vfx
{: #stop_cast_vfx }

void **stop_cast_vfx**()

Stops casting visual effects on both hands.

---

#### find_available_remote
{: #find_available_remote }

RemoteTransform3D **find_available_remote**(slot: String)

Finds an available remote transform in the specified slot's pool.

Parameters:
* slot: String - Slot identifier to search in

Implementation:
* Checks if slot exists in remote_transforms
* Iterates through slot's remote transforms
* Returns first inactive remote transform
* Adds returned transform to active_remotes
* Returns null if no transforms available

---

#### release_remote
{: #release_remote }

void **release_remote**(remote: RemoteTransform3D)

Makes a remote transform available for reuse.

Parameters:
* remote: RemoteTransform3D - Transform to release

Implementation:
* Removes from active_remotes
* Clears remote path
* Disables position/rotation updates
* Disables global coordinates

---

#### build_mesh_instances_array
{: #build_mesh_instances_array }

void **build_mesh_instances_array**(node: Node)

Recursively builds array of all mesh instances in the rig.

Parameters:
* node: Node - Starting node for recursion

Implementation:
* Traverses node hierarchy
* Adds MeshInstance3D nodes to mesh_instances
* Recursively processes Node3D children

---

#### _on_entity_combat_state_changed
{: #_on_entity_combat_state_changed }

void **_on_entity_combat_state_changed**(state: int)

Updates hitbox outline based on combat state.

Parameters:
* state: int - New combat state (0: non-combat, 1: combat)

Implementation:
* State 0: Hides outline
* State 1: Shows and colors outline based on entity type:
  * Companion: Green (0.186, 0.745, 0)
  * Pet: Blue (0, 0.565, 1)
  * Other: Red (1, 0, 0)

---

#### _on_entity_selection_state_changed
{: #_on_entity_selection_state_changed }

void **_on_entity_selection_state_changed**(is_current: bool, is_selected: bool)

Updates selection marker visibility and color.

Parameters:
* is_current: bool - If entity is current selection
* is_selected: bool - If entity is in selection group

Implementation:
* Hides marker if not selected
* Sets color based on selection type:
  * Current: Cyan (0.221, 0.928, 0.943)
  * Selected: Green (0.186, 0.745, 0)

---

#### set_highlight_overlay
{: #set_highlight_overlay }

void **set_highlight_overlay**(status: int)

Sets mesh overlay material based on entity status.

Parameters:
* status: int - Highlight status code

Implementation:
* For transparent entities: Uses transparent material
* Otherwise sets material based on status:
  * 0: Normal material
  * 1: Hover material
  * 2: No material
  * 3: Team-based material (friendly/enemy)
* Applies material to all mesh instances if outline eligible

---

#### can_update_outline
{: #can_update_outline }

bool **can_update_outline**()

Checks if outline can be updated based on current conditions.

Returns: bool - True if outline can be updated

Implementation:
* Checks entity is not current target
* Checks entity is not current player
* Checks game is not paused
* Checks entity is not in selected units

---

#### update_nameplate
{: #update_nameplate }

void **update_nameplate**(color: int)

Updates nameplate border color for minions and pets.

Parameters:
* color: int - Color index to use

Implementation:
* Only updates for Minion or Pet entities
* Sets nameplate border to specified color

---

#### set_mesh_override
{: #set_mesh_override }

void **set_mesh_override**(material: Material)

Applies material override to all mesh instances.

Parameters:
* material: Material - Override material

Implementation:
* Only applies if outline eligible and not transparent
* Sets material override on all mesh instances

---

#### clear_mesh_override
{: #clear_mesh_override }

void **clear_mesh_override**(material: Material)

Removes specific material override from mesh instances.

Parameters:
* material: Material - Material to clear

Implementation:
* Only processes if outline eligible and not transparent
* Clears override if it matches specified material

---

#### animate_transparency_off
{: #animate_transparency_off }

void **animate_transparency_off**()

Animates mesh instances to fully opaque.

Implementation:
* Creates tween for each mesh instance
* Animates transparency to 0.0 over 1.5 seconds

---

#### animate_transparency_on
{: #animate_transparency_on }

void **animate_transparency_on**()

Animates mesh instances to fully transparent.

Implementation:
* Creates tween for each mesh instance
* Animates transparency to 1.0 over 1.5 seconds

---

#### start_cast_vfx
{: #start_cast_vfx }

void **start_cast_vfx**()

Activates casting visual effects.

Implementation:
* Shows and starts right hand VFX if present
* Shows and starts left hand VFX if present

---

#### stop_cast_vfx
{: #stop_cast_vfx }

void **stop_cast_vfx**()

Deactivates casting visual effects.

Implementation:
* Hides and stops right hand VFX if present
* Hides and stops left hand VFX if present
