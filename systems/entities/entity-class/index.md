---
layout: default
title: Entity
parent: Entity System
nav_order: 1
has_children: true
permalink: /systems/entities/entity-class/
---

# Entity

Inherits: [CharacterBody3D](https://docs.godotengine.org/en/stable/classes/class_characterbody3d.html)

## Description

Entity is the base class for all characters and creatures in the game world. It provides core functionality for movement, combat, stats management, and interaction with the game's systems. This class serves as the foundation for both player-controlled characters and AI-driven entities.

Key features:a
- Manages entity stats, health, and resources
- Handles movement and physics interactions
- Provides a framework for combat mechanics including damage and healing
- Manages effects, abilities, and status conditions
- Integrates with the game's AI and targeting systems
- Supports various entity types (Companion, Minion, Boss, NPC)

## Child Classes
- [Companion](./companion.md)
- [Minion](./minion.md)
- [Boss](./boss.md)
- [Pet](./pet.md)

## Enumerations

enum Team:
- NONE = 0 — Default team, no specific allegiance
- ALLY = 1 — Friendly to the player
- ENEMY = 2 — Hostile to the player
- NEUTRAL = 3 — Neither friendly nor hostile

# Signals

| Signal | Description |
|--------|-------------|
| `entity_taken_damage(damage_taken: int, is_tick_damage: bool, was_crit: bool)` | Emitted when entity receives damage. Includes damage amount and type information |
| `entity_health_changed(new_health: int)` | Emitted when entity's health value changes |
| `entity_dodged(damage_dodged: int)` | Emitted when entity successfully dodges an attack |
| `entity_parried(damage_parried: int)` | Emitted when entity successfully parries an attack |
| `entity_blocked(damage_blocked: int)` | Emitted when entity successfully blocks damage |
| `entity_died(entity: Entity)` | Emitted when entity's health reaches 0 and dies |
| `entity_delt_damage(effect: Effect, target: Variant)` | Emitted when entity successfully deals damage to a target |
| `entity_heal_cast(effect: Effect, target: Variant)` | Emitted when entity casts a healing effect |
| `entity_ability_cast(ability: Ability, target: Variant)` | Emitted when entity uses an ability |
| `entity_basic_attack_cast()` | Emitted when entity performs a basic attack |
| `entity_critical_hit(effect: Effect, target: Variant)` | Emitted when entity lands a critical hit |
| `entity_casting()` | Emitted when entity begins casting an ability |
| `entity_stop_casting()` | Emitted when entity stops or interrupts casting |
| `entity_resource_changed(new_resource: int)` | Emitted when entity's resource value changes |
| `entity_stat_changed()` | Emitted when any of entity's stats are modified |
| `entity_interrupted()` | Emitted when entity's cast or action is interrupted |
| `target_update(target_name: String)` | Emitted when entity changes targets |
| `effect_gained(effect: Effect)` | Emitted when entity gains a new effect |
| `effect_updated(effect: Effect)` | Emitted when an existing effect is modified |
| `effect_lost(effect: Effect)` | Emitted when an effect expires or is removed |
| `pet_follow()` | Emitted when entity commands pets to follow |
| `pet_stop_follow()` | Emitted when entity commands pets to stop following |
| `action_state_changed(state: String)` | Emitted when entity's action state changes |
| `movement_state_changed(state: String)` | Emitted when entity's movement state changes |
| `entity_combat_state_changed(state: int)` | Emitted when entity enters/leaves combat (0: Out of Combat, 1: In Combat) |
| `entity_selection_state_changed(is_current: bool, is_selected: bool)` | Emitted when entity's selection state changes |

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| int | [entityID](#entityid) | 0 | Unique identifier for the entity type |
| int | [entity_unique_ID](#entity_unique_id) | 0 | Unique instance ID for individual entities in the world |
| String | [entity_name](#entity_name) | "NAME" | Display name of the entity |
| int | [entity_type](#entity_type) | 0 | Type of entity (0: Companion, 1: Pet, 2: Minion, 3: Boss, 4: NPC) |
| int | [level](#level) | 1 | Current level of the entity |
| Color | [resource_colour](#resource_colour) | Color("3f92ff") | Color used for the resource bar display |
| float | [pull_range](#pull_range) | 0.0 | Range at which the entity will engage in combat |
| float | [attack_range](#attack_range) | 0.0 | Range at which entity will attack |
| bool | [always_immobile](#always_immobile) | false | If true, entity cannot move |
| bool | [does_not_face_direction](#does_not_face_direction) | false | If true, entity will not rotate to face targets |

### Immunity Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | [physical_damage_immunity](#physical_damage_immunity) | false | Immune to physical damage |
| bool | [magical_damage_immunity](#magical_damage_immunity) | false | Immune to magical damage |
| bool | [flee_immunity](#flee_immunity) | false | Cannot be forced to flee |
| bool | [disorient_immunity](#disorient_immunity) | false | Cannot be disoriented |
| bool | [rooted_immunity](#rooted_immunity) | false | Cannot be rooted |
| bool | [forceful_displacement_immunity](#forceful_displacement_immunity) | false | Cannot be knocked back or pulled |
| bool | [silance_immunity](#silance_immunity) | false | Cannot be silenced |
| bool | [blind_immunity](#blind_immunity) | false | Cannot be blinded |
| bool | [cripple_immunity](#cripple_immunity) | false | Cannot be crippled |
| bool | [incapacitated_immunity](#incapacitated_immunity) | false | Cannot be incapacitated |

### Node Path Properties

| Type | Property | Description |
|------|----------|-------------|
| RigController | [rig](#rig) | Reference to entity's visual and animation controller |
| CollisionShape3D | [entity_collision_shape](#entity_collision_shape) | Physics collision shape |
| EntityStatsContainer | [entity_stats](#entity_stats) | Stats and attributes manager |
| StateMachine | [ai](#ai) | AI state machine controller |
| AggroTable | [aggro_table](#aggro_table) | Tracks threat levels from other entities |
| AbilityContainer | [ability_container](#ability_container) | Manages entity abilities |
| PetsContainer | [pet_container](#pet_container) | Manages pet entities |
| DynamicFollowerSystem | [pet_follower_system](#pet_follower_system) | Controls pet movement and formation |
| EffectsContainer | [effects_container](#effects_container) | Holds & Manages current active parasite effects |
| Camera3D | [full_body_cam](#full_body_cam) | Full body camera view |
| Camera3D | [face_cam](#face_cam) | Face close-up camera |
| Nameplate | [nameplate](#nameplate) | UI elements display |
| DamageNumbers | [damage_number_origin](#damage_number_origin) | Floating combat text origin point |
| MarginContainer | [debug_checker](#debug_checker) | Debug UI container |
| Timer | [debug_timer](#debug_timer) | Debug update timer |
| EquipmentInventoryData | [equipment_data](#equipment_data) | Equipment inventory manager |
| InventoryData | [inventory_data](#inventory_data) | General inventory manager |

### General Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Entity | [target](#target) | null | Current target of the entity |
| Vector3 | [target_position](#target_position) | Vector3.ZERO | Position of current target |
| bool | [target_locked](#target_locked) | false | If true, target cannot be changed |
| Team | [team](#team) | Team.NONE | Current team allegiance |
| Ability | [casting_ability](#casting_ability) | null | Currently casting ability |
| AnimationPlayer | [animation_player](#animation_player) | null | Entity's animation controller |

### State Flags

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | [dead](#dead) | false | If true, entity is defeated |
| bool | [currently_moving](#currently_moving) | false | If true, entity is in motion |
| bool | [in_combat](#in_combat) | false | If true, entity is in combat |
| bool | [casting](#casting) | false | If true, entity is casting an ability |
| bool | [immobile](#immobile) | false | If true, entity cannot move |
| Effect | [active_movement_effect](#active_movement_effect) | null | Current movement-affecting effect |
| bool | [falling](#falling) | false | If true, entity is in mid-air |
| bool | [walking](#walking) | false | If true, entity is walking (vs running) |
| bool | [flying](#flying) | false | If true, entity is in flight mode |

### Status Effect Flags

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | [incapacitated](#incapacitated) | false | If true, entity is stunned |
| bool | [flee](#flee) | false | If true, entity is forced to flee |
| bool | [disorient](#disorient) | false | If true, entity is disoriented |
| bool | [rooted](#rooted) | false | If true, entity cannot move |
| bool | [silance](#silance) | false | If true, entity cannot cast spells |
| bool | [blind](#blind) | false | If true, entity cannot use physical abilities |
| bool | [cripple](#cripple) | false | If true, entity has reduced movement |

### Status Effect Immunity Flags

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | [incapacitated_immune](#incapacitated_immune) | false | Current immunity to incapacitation |
| bool | [flee_immune](#flee_immune) | false | Current immunity to flee effects |
| bool | [disorient_immune](#disorient_immune) | false | Current immunity to disorientation |
| bool | [root_immune](#root_immune) | false | Current immunity to root effects |
| bool | [silance_immune](#silance_immune) | false | Current immunity to silence effects |
| bool | [blind_immune](#blind_immune) | false | Current immunity to blind effects |
| bool | [cripple_immune](#cripple_immune) | false | Current immunity to cripple effects |

# Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Called when the node enters scene tree |
| void | [_initialize_entity](#_initialize_entity) | Initializes all components and systems |
| void | [_connect_entity_signals](#_connect_entity_signals) | Connects necessary signals |
| void | [_set_entity_team](#_set_entity_team) | Sets team based on entity type |
| void | [_setup_rig](#_setup_rig) | Sets up entity's rig and mesh instances |
| void | [_setup_animations](#_setup_animations) | Sets up animation system |
| void | [_setup_stats](#_setup_stats) | Initializes stats container |
| void | [_setup_ai](#_setup_ai) | Sets up AI system |
| void | [_setup_pet_container](#_setup_pet_container) | Initializes pet system |
| void | [setup_nameplate](#setup_nameplate) | Sets up entity's nameplate |
| void | [_setup_effects](#_setup_effects) | Initializes effects container |
| void | [_setup_immunities](#_setup_immunities) | Sets up immunity flags |
| void | [_setup_ability_container](#_setup_ability_container) | Initializes ability container |
| void | [face_direction](#face_direction) | Forces entity to face direction |
| void | [set_target](#set_target) | Sets current target |
| void | [animation_finished](#animation_finished) | Handles animation completion |
| void | [change_combat_state](#change_combat_state) | Changes combat state |
| void | [die](#die) | Handles entity death |
| void | [_on_entity_taken_damage](#_on_entity_taken_damage) | Processes damage taken |
| void | [cast_interrupted](#cast_interrupted) | Interrupts current cast |
| void | [stop_cast](#stop_cast) | Forces cast stop |
| void | [entity_fleed](#entity_fleed) | Applies flee effect |
| void | [flee_immune_timer_end](#flee_immune_timer_end) | Ends flee immunity |
| void | [entity_disorientated](#entity_disorientated) | Applies disorient effect |
| void | [disorient_immune_timer_end](#disorient_immune_timer_end) | Ends disorient immunity |
| void | [entity_rooted](#entity_rooted) | Applies root effect |
| void | [rooted_immune_timer_end](#rooted_immune_timer_end) | Ends root immunity |
| void | [entity_silanced](#entity_silanced) | Applies silence effect |
| void | [silance_immune_timer_end](#silance_immune_timer_end) | Ends silence immunity |
| void | [entity_blinded](#entity_blinded) | Applies blind effect |
| void | [blind_immune_timer_end](#blind_immune_timer_end) | Ends blind immunity |
| void | [entity_crippled](#entity_crippled) | Applies cripple effect |
| void | [cripple_immune_timer_end](#cripple_immune_timer_end) | Ends cripple immunity |
| void | [set_current_target_on](#set_current_target_on) | Highlights current target |
| void | [set_current_target_off](#set_current_target_off) | Removes target highlight |
| void | [debug_display](#debug_display) | Toggles debug display |
| void | [connect_to_effect](#connect_to_effect) | Connects effect callbacks |
| void | [_on_tree_exiting](#_on_tree_exiting) | Handles cleanup on removal |

# Property Descriptions

## Exported Properties

#### entityID
{: #entityid }

int **entityID** = `0`
* int **get_entity_id**()
* void **set_entity_id**(value: int)

Unique identifier for the entity type. This ID is used to identify different types of entities in the game (e.g., different types of companions or enemies). Essential for saving and loading entity data.

Note: All new entities must have a unique ID set using the relevant database updater tool script.

---

#### entity_unique_ID
{: #entity_unique_id }

int **entity_unique_ID** = `0`
* int **get_entity_unique_id**()
* void **set_entity_unique_id**(value: int)

Instance-specific unique identifier. This ID distinguishes individual instances of entities in the world. Required for save functionality to work correctly. Each entity instance in the world must have a unique ID.

---

#### entity_name
{: #entity_name }

String **entity_name** = `"NAME"`
* String **get_entity_name**()
* void **set_entity_name**(value: String)

Display name of the entity shown in the UI. Used in nameplates, combat logs, and other UI elements where the entity needs to be identified.

---

#### entity_type
{: #entity_type }

int **entity_type** = `0`
* int **get_entity_type**()
* void **set_entity_type**(value: int)

Defines the basic type of the entity. Affects AI behavior, combat interactions, and UI display.
* `0`: Companion - Player-controlled ally with full ability sets
* `1`: Pet - AI-controlled companion creature
* `2`: Minion - Basic enemy unit
* `3`: Boss - Complex enemy with unique abilities
* `4`: NPC - Non-combat interactive entity

Note: The entity_type directly influences the team assignment during initialization.

---

#### level
{: #level }

int **level** = `1`
* int **get_level**()
* void **set_level**(value: int)

Current level of the entity. Affects base stats, combat calculations, and interaction possibilities. Valid range is 1-10.

---

#### resource_colour
{: #resource_colour }

Color **resource_colour** = `Color("3f92ff")`
* Color **get_resource_colour**()
* void **set_resource_colour**(value: Color)

Color used for the entity's resource bar in the UI. Customizes the appearance of the resource meter in nameplates and other UI elements. Default is a bright blue color.

---

#### pull_range
{: #pull_range }

float **pull_range** = `0.0`
* float **get_pull_range**()
* void **set_pull_range**(value: float)

Distance at which the entity will engage in combat with enemies. When another entity enters this range:
* The entity will enter combat state
* Initial aggro is generated
* AI will begin combat routines

Note: Only active if the entity has AI combat capabilities.

---

#### attack_range
{: #attack_range }

float **attack_range** = `0.0`
* float **get_attack_range**()
* void **set_attack_range**(value: float)

Maximum distance at which the entity can perform basic attacks. Used for:
* AI positioning calculations
* Auto-attack range checks
* Combat movement decisions

Note: This range is separate from ability-specific ranges, which are defined in the ability data.

---

#### always_immobile
{: #always_immobile }

bool **always_immobile** = `false`
* bool **is_always_immobile**()
* void **set_always_immobile**(value: bool)

If `true`, the entity cannot move from its position. Useful for:
* Stationary NPCs
* Fixed position enemies
* Environmental entities

Note: This is different from temporary immobilization effects (like root or stun).

---

#### does_not_face_direction
{: #does_not_face_direction }

bool **does_not_face_direction** = `false`
* bool **get_does_not_face_direction**()
* void **set_does_not_face_direction**(value: bool)

If `true`, the entity will not rotate to face targets or movement direction. Used for:
* Entities that should maintain a fixed orientation
* Special NPCs or environmental entities
* Entities with non-standard movement behavior

See also: face_direction() method for manual rotation control.

## Immunity Properties

#### physical_damage_immunity
{: #physical_damage_immunity }

bool **physical_damage_immunity** = `false`
* bool **is_physical_damage_immune**()
* void **set_physical_damage_immune**(value: bool)

If `true`, the entity takes no damage from physical attacks. Affects:
* Basic attacks
* Physical abilities
* Environmental physical damage

Note: Does not affect magical damage sources.

---

#### magical_damage_immunity
{: #magical_damage_immunity }

bool **magical_damage_immunity** = `false`
* bool **is_magical_damage_immune**()
* void **set_magical_damage_immune**(value: bool)

If `true`, the entity takes no damage from magical attacks. Affects:
* Spell damage
* Magical abilities
* Environmental magical damage

Note: Does not affect physical damage sources.

---

#### flee_immunity
{: #flee_immunity }

bool **flee_immunity** = `false`
* bool **is_flee_immune**()
* void **set_flee_immune**(value: bool)

If `true`, the entity cannot be affected by fear or flee effects. When immune:
* Fear effects are ignored
* Entity maintains normal AI behavior
* Existing flee effects are removed
* Sets 15-second immunity timer when gained through effects

Note: Duration can be checked through flee_immune_timer.

---

#### disorient_immunity
{: #disorient_immunity }

bool **disorient_immunity** = `false`
* bool **is_disorient_immune**()
* void **set_disorient_immune**(value: bool)

If `true`, the entity cannot be disoriented. When immune:
* Disorienting effects are ignored
* Entity maintains normal control
* Existing disorient effects are removed
* Sets 15-second immunity timer when gained through effects

Note: Duration can be checked through disorient_immune_timer.

---

#### rooted_immunity
{: #rooted_immunity }

bool **rooted_immunity** = `false`
* bool **is_root_immune**()
* void **set_root_immune**(value: bool)

If `true`, the entity cannot be rooted in place. When immune:
* Root effects are ignored
* Entity maintains full mobility
* Existing root effects are removed
* Sets 15-second immunity timer when gained through effects

Note: Duration can be checked through rooted_immune_timer.

---

#### forceful_displacement_immunity
{: #forceful_displacement_immunity }


bool **forceful_displacement_immunity** = `false`
* bool **is_forceful_displacement_immune**()
* void **set_forceful_displacement_immune**(value: bool)

If `true`, the entity cannot be forcefully moved. Prevents:
* Knockback effects
* Pull effects
* Push effects
* Other forced movement abilities

Note: Does not affect voluntary movement or teleports.

---

#### silance_immunity
{: #silance_immunity }

bool **silance_immunity** = `false`
* bool **is_silance_immune**()
* void **set_silance_immune**(value: bool)

If `true`, the entity cannot be silenced. When immune:
* Silence effects are ignored
* Spell casting remains available
* Existing silence effects are removed
* Sets 15-second immunity timer when gained through effects

Note: Duration can be checked through silance_immune_timer.

---

#### blind_immunity
{: #blind_immunity }

bool **blind_immunity** = `false`
* bool **is_blind_immune**()
* void **set_blind_immune**(value: bool)

If `true`, the entity cannot be blinded. When immune:
* Blind effects are ignored
* Physical abilities remain available
* Existing blind effects are removed
* Sets 15-second immunity timer when gained through effects

Note: Duration can be checked through blind_immune_timer.

---

#### cripple_immunity
{: #cripple_immunity }

bool **cripple_immunity** = `false`
* bool **is_cripple_immune**()
* void **set_cripple_immune**(value: bool)

If `true`, the entity cannot be crippled. When immune:
* Movement speed reduction effects are ignored
* Normal movement speed is maintained
* Existing cripple effects are removed
* Sets 15-second immunity timer when gained through effects

Note: Duration can be checked through cripple_immune_timer.

---

#### incapacitated_immunity
{: #incapacitated_immunity }

bool **incapacitated_immunity** = `false`
* bool **is_incapacitated_immune**()
* void **set_incapacitated_immune**(value: bool)

If `true`, the entity cannot be incapacitated. When immune:
* Stun effects are ignored
* Entity maintains normal control
* Existing incapacitate effects are removed
* Sets 15-second immunity timer when gained through effects

Note: Duration can be checked through incapacitated_immune_timer.

## Node Path Properties

#### rig
{: #rig }

RigController **rig**
* RigController **get_rig**()
* void **set_rig**(value: RigController)

Reference to the entity's visual representation controller. Manages:
* Mesh instances and materials
* Animation playback
* Visual effects and highlights
* Equipment attachments
* Outline effects for selection and targeting

Note: Must be set for entity to be visible and animated.

---

#### entity_collision_shape
{: #entity_collision_shape }

CollisionShape3D **entity_collision_shape**
* CollisionShape3D **get_entity_collision_shape**()
* void **set_entity_collision_shape**(value: CollisionShape3D)

Physics collision shape for the entity. Defines:
* Physical boundaries for collision detection
* Area for ability targeting
* Space occupied in the world
* Interaction boundaries

Note: Required for proper physics and collision handling.

---

#### entity_stats
{: #entity_stats }

EntityStatsContainer **entity_stats**
* EntityStatsContainer **get_entity_stats**()
* void **set_entity_stats**(value: EntityStatsContainer)

Container managing all entity statistics and attributes. Handles:
* Base, major, and minor stats
* Health and resource management
* Combat calculations
* Damage and healing processing
* Stat modifications

Note: Core component required for entity functionality.

---

#### ai
{: #ai }

StateMachine **ai**
* StateMachine **get_ai**()
* void **set_ai**(value: StateMachine)

AI state machine controlling entity behavior. Manages:
* Movement and action states
* Combat behavior
* Decision making
* Target selection
* State transitions

Note: Optional for player-controlled entities.

---

#### aggro_table
{: #aggro_table }

AggroTable **aggro_table**
* AggroTable **get_aggro_table**()
* void **set_aggro_table**(value: AggroTable)

System for tracking threat levels from other entities. Manages:
* Threat calculation
* Target priority
* Combat engagement
* Aggro decay
* Target switching

Note: Only used by AI-controlled combat entities.

---

#### ability_container
{: #ability_container }

AbilityContainer **ability_container**
* AbilityContainer **get_ability_container**()
* void **set_ability_container**(value: AbilityContainer)

Container managing entity abilities and their usage. Handles:
* Ability creation and initialization
* Cooldown management
* Resource costs
* Usage validation
* Global cooldown

Note: Required for entities that can use abilities.

---

#### pet_container
{: #pet_container }

PetsContainer **pet_container**
* PetsContainer **get_pet_container**()
* void **set_pet_container**(value: PetsContainer)

Container managing pet entities. Handles:
* Pet tracking
* Pet addition/removal
* Pet state management
* Integration with follower system

Note: Only required for entities that can have pets.

---

#### pet_follower_system
{: #pet_follower_system }

DynamicFollowerSystem **pet_follower_system**
* DynamicFollowerSystem **get_pet_follower_system**()
* void **set_pet_follower_system**(value: DynamicFollowerSystem)

System controlling pet movement and formation. Manages:
* Formation positioning
* Following behavior
* Movement updates
* Position adjustments

Note: Required if entity uses the pet system.

---

#### effects_container
{: #effects_container }


EffectsContainer **effects_container**
* EffectsContainer **get_effects_container**()
* void **set_effects_container**(value: EffectsContainer)

Container managing active effects on the entity. Handles:
* Effect application
* Effect removal
* Effect tracking
* Effect updates
* Effect stacking

Note: Required for entities that can have status effects.

---

#### full_body_cam
{: #full_body_cam }

Camera3D **full_body_cam**
* Camera3D **get_full_body_cam**()
* void **set_full_body_cam**(value: Camera3D)

Camera for full body view of the entity. Used for:
* Character preview
* Equipment view
* Animation preview
* Customization view

Note: Optional, used primarily for player characters.

---

#### face_cam
{: #face_cam }

Camera3D **face_cam**
* Camera3D **get_face_cam**()
* void **set_face_cam**(value: Camera3D)

Camera for close-up view of entity's face. Used for:
* Portrait views
* Dialog scenes
* Facial customization
* Expression display

Note: Optional, used primarily for player characters.

---

#### nameplate
{: #nameplate }

Nameplate **nameplate**
* Nameplate **get_nameplate**()
* void **set_nameplate**(value: Nameplate)

UI element displaying entity information. Shows:
* Entity name
* Health/resource bars
* Status effects
* Cast bars
* Combat text

Note: Required for visible entities in game world.

---

#### damage_number_origin
{: #damage_number_origin }

DamageNumbers **damage_number_origin**
* DamageNumbers **get_damage_number_origin**()
* void **set_damage_number_origin**(value: DamageNumbers)

Point of origin for floating combat text. Used for:
* Damage numbers
* Healing numbers
* Status effect text
* Combat feedback

Note: Required for combat feedback visualization.

---

#### debug_checker
{: #debug_checker }


MarginContainer **debug_checker**
* MarginContainer **get_debug_checker**()
* void **set_debug_checker**(value: MarginContainer)

Container for debug information display. Shows:
* Entity state
* Current properties
* Debug statistics
* Development info

Note: Only visible when debug mode is enabled.

---

#### debug_timer
{: #debug_timer }


Timer **debug_timer**
* Timer **get_debug_timer**()
* void **set_debug_timer**(value: Timer)

Timer for debug update frequency. Controls:
* Debug info refresh rate
* Development testing
* Performance monitoring

Note: Only active when debug mode is enabled.

---

#### equipment_data
{: #equipment_data }

EquipmentInventoryData **equipment_data**
* EquipmentInventoryData **get_equipment_data**()
* void **set_equipment_data**(value: EquipmentInventoryData)

Manager for entity equipment slots. Handles:
* Equipment slots
* Equipment stats
* Equipment visualization
* Equipment changes

Note: Required for entities that can equip items.

---

#### inventory_data
{: #inventory_data }

InventoryData **inventory_data**
* InventoryData **get_inventory_data**()
* void **set_inventory_data**(value: InventoryData)

Manager for entity inventory. Handles:
* Item storage
* Item management
* Inventory slots
* Item interactions

Note: Required for entities that can carry items.

## General Properties

#### target
{: #target }

Entity **target**
* Entity **get_target**()
* void **set_target**(value: Entity)

Currently selected target for the entity. Used for:
* Ability targeting
* AI decision making
* Combat interactions
* Movement calculations
* UI target display

Note: Can be locked using target_locked flag.

---

#### target_position
{: #target_position }


Vector3 **target_position**
* Vector3 **get_target_position**()
* void **set_target_position**(value: Vector3)

Current world position of the entity's target. Used for:
* Movement pathfinding
* Range calculations
* Position updating
* AI navigation

Note: Updated automatically when target moves.

Pretty sure this is defunct - if not it should be, very taxing don't see why we need it

---

#### target_locked
{: #target_locked }

#### target_locked
{: #target_locked }

bool **target_locked**
* bool **is_target_locked**()
* void **set_target_locked**(value: bool)

If `true`, the entity's target cannot be changed. Controls:
* Target switching prevention
* Forced target maintenance
* AI target selection
* Manual target changes

Note: Used for abilities requiring specific target focus.

---

#### team
{: #team }

Team **team**
* Team **get_team**()
* void **set_team**(value: Team)

Entity's current team allegiance. Determines:
* Combat interactions
* AI behavior
* Targeting restrictions
* UI elements appearance
* Effect applications

See also: Team enumeration for possible values.

---

#### casting_ability
{: #casting_ability }

Ability **casting_ability**
* Ability **get_casting_ability**()
* void **set_casting_ability**(value: Ability)

Currently casting ability, if any. Tracks:
* Active cast
* Cast interruption
* Cast progress
* Cast requirements

Note: Null when not casting an ability.

---

#### animation_player
{: #animation_player }

AnimationPlayer **animation_player**
* AnimationPlayer **get_animation_player**()
* void **set_animation_player**(value: AnimationPlayer)

Controller for entity animations. Manages:
* Movement animations
* Combat animations
* Ability animations
* State transitions
* Animation blending

Note: Required for visual entity movement and actions.

## State Flags

#### dead
{: #dead }

bool **dead** = `false`
* bool **is_dead**()
* void **set_dead**(value: bool)

If `true`, the entity is defeated. When dead:
* All movement stops
* Actions are prevented
* Combat state ends
* Collision is disabled
* Death animation plays
* All effects are removed

Note: Can only be revived through specific abilities or events.

---

#### currently_moving
{: #currently_moving }

bool **currently_moving** = `false`
* bool **is_currently_moving**()
* void **set_currently_moving**(value: bool)

If `true`, the entity is in motion. Affects:
* Movement animations
* State transitions
* AI decisions
* Ability usage
* Formation updates

Note: Updated automatically during movement processing.

---

#### in_combat
{: #in_combat }

bool **in_combat** = `false`
* bool **is_in_combat**()
* void **set_in_combat**(value: bool)

If `true`, the entity is engaged in combat. Affects:
* AI behavior
* Health regeneration
* Combat animations
* UI elements
* State decisions

Note: Influences various systems including regeneration and AI.

---

#### casting
{: #casting }

bool **casting** = `false`
* bool **is_casting**()
* void **set_casting**(value: bool)

If `true`, the entity is casting an ability. During casting:
* Movement may be restricted
* Other abilities are locked
* Cast bar is shown
* Can be interrupted
* Animation plays

Note: Works in conjunction with casting_ability property.

---

#### immobile
{: #immobile }

bool **immobile** = `false`
* bool **is_immobile**()
* void **set_immobile**(value: bool)

If `true`, the entity cannot move. Different from always_immobile:
* Temporary state
* Can be caused by effects
* Can be removed
* Allows rotation
* Combat viable

Note: Used for temporary movement restrictions.

---

#### active_movement_effect
{: #active_movement_effect }

Effect **active_movement_effect** = `null`
* Effect **get_active_movement_effect**()
* void **set_active_movement_effect**(value: Effect)

Current effect modifying movement, if any. Tracks:
* Movement speed changes
* Movement restrictions
* Special movement types
* Movement animations
* Effect duration

Note: Only one movement effect can be active at a time.

---

#### falling
{: #falling }

bool **falling** = `false`
* bool **is_falling**()
* void **set_falling**(value: bool)

If `true`, the entity is in mid-air. During falling:
* Gravity is applied
* Fall animation plays
* Movement is limited
* States are restricted
* Landing is checked

Note: Automatically handled by movement system.

---

#### walking
{: #walking }

bool **walking** = `false`
* bool **is_walking**()
* void **set_walking**(value: bool)

If `true`, entity is moving at walk speed. Affects:
* Movement speed
* Animation state
* Sound effects
* Combat status
* Energy usage

Note: Alternative to running state.

---

#### flying
{: #flying }

bool **flying** = `false`
* bool **is_flying**()
* void **set_flying**(value: bool)

If `true`, entity is in flight mode. During flight:
* Gravity is ignored
* Different movement rules
* Special animations
* Unique interactions
* Height tracking

Note: Only available to specific entity types.

## Status Effect Flags

#### incapacitated
{: #incapacitated }

bool **incapacitated** = `false`
* bool **is_incapacitated**()
* void **set_incapacitated**(value: bool)

If `true`, entity is stunned. During incapacitation:
* All actions prevented
* Movement blocked
* Abilities blocked
* AI suspended
* Stun animation plays

Note: Can be prevented by incapacitated_immunity.

---

#### flee
{: #flee }

bool **flee** = `false`
* bool **is_fleeing**()
* void **set_flee**(value: bool)

If `true`, entity is forced to flee. During flee:
* Forced movement away from source
* Cannot use abilities
* AI overridden
* Run animation plays
* Combat state maintained

Note: Can be prevented by flee_immunity.

---

#### disorient
{: #disorient }

bool **disorient** = `false`
* bool **is_disoriented**()
* void **set_disoriented**(value: bool)

If `true`, entity is disoriented. While disoriented:
* Movement is erratic
* Ability usage fails
* AI disrupted
* Special animation plays
* Combat effectiveness reduced

Note: Can be prevented by disorient_immunity.

---

#### rooted
{: #rooted }

bool **rooted** = `false`
* bool **is_rooted**()
* void **set_rooted**(value: bool)

If `true`, entity cannot move. While rooted:
* Movement prevented
* Position locked
* Can still rotate
* Can use abilities
* Special animation plays

Note: Can be prevented by rooted_immunity.

---

#### silance
{: #silance }

bool **silance** = `false`
* bool **is_silenced**()
* void **set_silenced**(value: bool)

If `true`, entity cannot cast spells. While silenced:
* Magical abilities blocked
* Current casts interrupted
* Physical abilities allowed
* Special effects shown
* UI indicator displayed

Note: Can be prevented by silance_immunity.

---

#### blind
{: #blind }


bool **blind** = `false`
* bool **is_blind**()
* void **set_blind**(value: bool)

If `true`, entity cannot use physical abilities. While blinded:
* Physical abilities blocked
* Basic attacks fail
* Magical abilities allowed
* Special effects shown
* UI indicator displayed

Note: Can be prevented by blind_immunity.

---

#### cripple
{: #cripple }


bool **cripple** = `false`
* bool **is_crippled**()
* void **set_crippled**(value: bool)

If `true`, entity has reduced movement. While crippled:
* Movement speed reduced
* Special animation plays
* Movement effects shown
* Combat effectiveness reduced
* UI indicator displayed

Note: Can be prevented by cripple_immunity.

## Status Effect Immunity Flags

#### incapacitated_immune
{: #incapacitated_immune }

bool **incapacitated_immune** = `false`
* bool **is_incapacitated_immune**()
* void **set_incapacitated_immune**(value: bool)

Current immunity to incapacitation effects. When immune:
* Stun effects blocked
* Current stuns removed
* 15-second timer started
* Immunity UI shown
* Prevents new applications

Note: Timer managed by incapacitated_immune_timer.

---

#### flee_immune
{: #flee_immune }

bool **flee_immune** = `false`
* bool **is_flee_immune**()
* void **set_flee_immune**(value: bool)

Current immunity to flee effects. When immune:
* Fear effects blocked
* Current fears removed
* 15-second timer started
* Immunity UI shown
* Prevents new applications

Note: Timer managed by flee_immune_timer.

---

#### disorient_immune
{: #disorient_immune }

bool **disorient_immune** = `false`
* bool **is_disorient_immune**()
* void **set_disorient_immune**(value: bool)

Current immunity to disorientation effects. When immune:
* Disorient effects blocked
* Current disorients removed
* 15-second timer started
* Immunity UI shown
* Prevents new applications

Note: Timer managed by disorient_immune_timer.

---

#### root_immune
{: #root_immune }

bool **root_immune** = `false`
* bool **is_root_immune**()
* void **set_root_immune**(value: bool)

Current immunity to root effects. When immune:
* Root effects blocked
* Current roots removed
* 15-second timer started
* Immunity UI shown
* Prevents new applications

Note: Timer managed by root_immune_timer.

---

#### silance_immune
{: #silance_immune }

bool **silance_immune** = `false`
* bool **is_silance_immune**()
* void **set_silance_immune**(value: bool)

Current immunity to silence effects. When immune:
* Silence effects blocked
* Current silences removed
* 15-second timer started
* Immunity UI shown
* Prevents new applications

Note: Timer managed by silance_immune_timer.

---

#### blind_immune
{: #blind_immune }

bool **blind_immune** = `false`
* bool **is_blind_immune**()
* void **set_blind_immune**(value: bool)

Current immunity to blind effects. When immune:
* Blind effects blocked
* Current blinds removed
* 15-second timer started
* Immunity UI shown
* Prevents new applications

Note: Timer managed by blind_immune_timer.

---

#### cripple_immune
{: #cripple_immune }

bool **cripple_immune** = `false`
* bool **is_cripple_immune**()
* void **set_cripple_immune**(value: bool)

Current immunity to cripple effects. When immune:
* Cripple effects blocked
* Current cripples removed
* 15-second timer started
* Immunity UI shown
* Prevents new applications

Note: Timer managed by cripple_immune_timer.


## Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Called when node enters scene tree. Calls _initialize_entity() to set up all entity systems.

---

#### _initialize_entity
{: #_initialize_entity }

void **_initialize_entity**()

Initializes all components and systems:
* Connects signals 
* Sets team
* Sets up rig, animations, stats
* Initializes immunities, effects, pets
* Sets up abilities and AI
* Initializes nameplate

---

#### _connect_entity_signals
{: #_connect_entity_signals }

void **_connect_entity_signals**()

Connects necessary signals:
* Target changes with PlayerManager
* Animation finished
* Debug signals
* Damage taken signals

---

#### _set_entity_team
{: #_set_entity_team }

void **_set_entity_team**()

Sets team based on entity_type:
* Companion (0) -> ALLY
* Pet (1) -> ALLY  
* Minion (2) -> ENEMY
* Boss (3) -> ENEMY
* NPC (4) -> NEUTRAL

---

#### _setup_rig
{: #_setup_rig }

void **_setup_rig**()

Sets up entity's rig:
* Assigns entity reference
* Connects signals
* Creates remote transforms 
* Builds mesh instances
* Sets initial highlight state

---

#### _setup_animations
{: #_setup_animations }

void **_setup_animations**()

Sets up animation system:
* Sets up entity animation player
* Configures animations
* Starts idle animation

---

#### _setup_stats
{: #_setup_stats }

void **_setup_stats**()

Initializes stats container:
* Assigns entity reference
* Sets up base stats

---

#### _setup_ai
{: #_setup_ai }

void **_setup_ai**()

Sets up AI system:
* Initializes AI state machine
* Sets up combat script

---

#### _setup_pet_container
{: #_setup_pet_container }

void **_setup_pet_container**()

Initializes pet system:
* Sets up leader
* Configures follower system

---

#### setup_nameplate
{: #setup_nameplate }

void **setup_nameplate**()

Sets up entity's nameplate and initializes debug display.

---

#### _setup_effects
{: #_setup_effects }

void **_setup_effects**()

Initializes effects container and assigns entity reference.

---

#### _setup_immunities
{: #_setup_immunities }

void **_setup_immunities**()

Sets up immunity flags based on exported variables:
* Flee immunity
* Incapacitate immunity
* Disorient immunity
* Root immunity
* Silence immunity
* Blind immunity
* Cripple immunity

---

#### _setup_ability_container
{: #_setup_ability_container }

void **_setup_ability_container**()

Initializes ability container:
* Assigns user reference
* Sets up node structure
* Generates ability nodes

---

#### face_direction
{: #face_direction }

void **face_direction**(look_at_direction: Vector3)

Forces entity to face direction if does_not_face_direction is false.

Parameters:
* look_at_direction: Vector3 - World position to face

---

#### set_target
{: #set_target }

void **set_target**(new_target: Entity)

Sets current target if not target_locked:
* Updates target reference
* Updates target position
* Emits target update signal
* Updates player target if needed

Parameters:
* new_target: Entity - New target entity

---

#### animation_finished
{: #animation_finished }

void **animation_finished**(_animation: String)

Handles animation completion:
* Sets animation speed
* Plays appropriate idle animation

Parameters:
* _animation: String - Completed animation name

---

#### change_combat_state
{: #change_combat_state }

void **change_combat_state**(value: bool)

Changes combat state and emits signal.

Parameters:
* value: bool - New combat state

---

#### die
{: #die }

void **die**()

Handles entity death:
* Sets dead state
* Stops movement/combat
* Removes effects/collision
* Plays death animation
* Updates UI
* Emits signals

---

#### _on_entity_taken_damage
{: #_on_entity_taken_damage }

void **_on_entity_taken_damage**(damage_taken: int, is_tick_damage: bool, was_crit: bool)

Processes damage taken:
* Displays damage numbers
* Plays audio/animations
* Updates combat state

Parameters:
* damage_taken: int - Amount of damage
* is_tick_damage: bool - If from periodic effect
* was_crit: bool - If critical hit

---

#### cast_interrupted
{: #cast_interrupted }

void **cast_interrupted**()

Interrupts current cast if interruptible:
* Checks interrupt shield
* Cancels cast if appropriate
* Emits interrupt signal

---

#### stop_cast
{: #stop_cast }

void **stop_cast**()

Forces immediate cast stop regardless of interrupt protection.

---

#### entity_fleed
{: #entity_fleed }

void **entity_fleed**()

Applies flee effect:
* Sets flee state
* Applies immunity
* Starts timer
* Plays animation

---

#### flee_immune_timer_end
{: #flee_immune_timer_end }

void **flee_immune_timer_end**()

Ends flee immunity timer and removes immunity.

---

#### entity_disorientated
{: #entity_disorientated }

void **entity_disorientated**()

Applies disorient effect:
* Sets disorient state
* Applies immunity
* Starts timer
* Plays animation

---

#### disorient_immune_timer_end
{: #disorient_immune_timer_end }

void **disorient_immune_timer_end**()

Ends disorient immunity timer and removes immunity.

---

#### entity_rooted
{: #entity_rooted }

void **entity_rooted**()

Applies root effect:
* Sets root state
* Applies immunity
* Starts timer

---

#### rooted_immune_timer_end
{: #rooted_immune_timer_end }

void **rooted_immune_timer_end**()

Ends root immunity timer and removes immunity.

---

#### entity_silanced
{: #entity_silanced }

void **entity_silanced**()

Applies silence effect:
* Sets silence state
* Applies immunity
* Starts timer

---

#### silance_immune_timer_end
{: #silance_immune_timer_end }

void **silance_immune_timer_end**()

Ends silence immunity timer and removes immunity.

---

#### entity_blinded
{: #entity_blinded }

void **entity_blinded**()

Applies blind effect:
* Sets blind state
* Applies immunity
* Starts timer

---

#### blind_immune_timer_end
{: #blind_immune_timer_end }

void **blind_immune_timer_end**()

Ends blind immunity timer and removes immunity.

---

#### entity_crippled
{: #entity_crippled }

void **entity_crippled**()

Applies cripple effect:
* Sets cripple state
* Applies immunity
* Starts timer

---

#### cripple_immune_timer_end
{: #cripple_immune_timer_end }

void **cripple_immune_timer_end**()

Ends cripple immunity timer and removes immunity.

---

#### set_current_target_on
{: #set_current_target_on }

void **set_current_target_on**()

Highlights entity as current target:
* Updates nameplate border
* Shows target marker

---

#### set_current_target_off
{: #set_current_target_off }

void **set_current_target_off**()

Removes current target highlight:
* Resets nameplate border
* Hides target marker

---

#### debug_display
{: #debug_display }

void **debug_display**()

Toggles debug display based on GameManager debug mode.

---

#### connect_to_effect
{: #connect_to_effect }

void **connect_to_effect**(ability_id: int, effect_id: int, start_callback: Callable, end_callback: Callable)

Connects callbacks to specific effects.

Parameters:
* ability_id: int - Ability containing effect
* effect_id: int - Effect to connect
* start_callback: Callable - Effect start callback
* end_callback: Callable - Effect end callback

---

#### _on_tree_exiting
{: #_on_tree_exiting }

void **_on_tree_exiting**()

Handles cleanup when entity is removed from scene. Emits entity_being_set_free signal.