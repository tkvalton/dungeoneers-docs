---
layout: default
title: Companion
parent: Entity
nav_order: 1
has_children: true
permalink: /systems/entities/entity-class/companion
---

# Companion

Inherits: [Entity](../entity-class/)

## Description

Companion represents a player-controlled character in the game. It extends the base Entity class with specific features for player characters, including class specialization, experience and leveling systems, and player-specific interactions.

Key features:
- Implements player class system with associated stats and abilities
- Manages experience points and leveling
- Handles player-specific input for ability usage
- Supports different roles (tank, healer, damage-dealer)
- Integrates with the game's UI and interaction systems

## Child Classes
- [Acoloyte](./acoloyte.md)
- [Barbarian](./barbarian.md)
- [Druid](./druid.md)
- [Mage](./mage.md)
- [Scoundrel](./scoundrel.md)
- [Templar](./templar.md)

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| CompanionDatabase.Companion_Class | [player_class_name](#player_class_name) | - | The companion's character class |
| CompanionDatabase.Primary_Stats | [first_stat](#first_stat) | - | Primary stat priority one |
| CompanionDatabase.Primary_Stats | [second_stat](#second_stat) | - | Primary stat priority two |
| Color | [class_colour](#class_colour) | - | Color associated with the class |

### Variables

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| int | [experience](#experience) | - | Current experience amount |
| int | [experience_requirement](#experience_requirement) | - | Required XP for next level |
| bool | [is_current_player](#is_current_player) | false | If true, currently selected player |
| bool | [follow_stance](#follow_stance) | false | AI state for following player |
| bool | [attack_stance](#attack_stance) | true | AI state for attacking |
| float | [interaction_range](#interaction_range) | 3.5 | Raycast length for interaction |
| CompanionDatabase.Spec_Role | [role](#role) | - | Role of current spec |

### Node References

| Type | Property | Description |
|------|----------|-------------|
| RayCast3D | [interact_ray](#interact_ray) | $AI/Interactions/InteractRay |
| Marker3D | [drop_location](#drop_location) | $AI/Interactions/DropLocation |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Called when companion enters scene tree |
| void | [_setup_ai](#_setup_ai) | Sets up AI system |
| void | [_companion_setup](#_companion_setup) | Sets up companion-specific features |
| void | [setup_specilization](#setup_specilization) | Sets up specialization |
| void | [connect_companion_signals](#connect_companion_signals) | Connects companion signals |
| void | [set_specilization](#set_specilization) | Handles specialization setup |
| void | [update_experience](#update_experience) | Updates XP and handles leveling |
| void | [interact](#interact) | Performs interaction |
| Vector3 | [get_drop_position](#get_drop_position) | Gets item drop position |
| void | [_on_tree_exiting](#_on_tree_exiting) | Handles cleanup on removal |

## Property Descriptions

### Exported Properties

#### player_class_name
{: #player_class_name }

CompanionDatabase.Companion_Class **player_class_name**
* CompanionDatabase.Companion_Class **get_player_class_name**()
* void **set_player_class_name**(value: CompanionDatabase.Companion_Class)

The companion's class type, determining available abilities and specializations.

---

#### first_stat
{: #first_stat }

CompanionDatabase.Primary_Stats **first_stat**
* CompanionDatabase.Primary_Stats **get_first_stat**()
* void **set_first_stat**(value: CompanionDatabase.Primary_Stats)

Primary attribute for class performance calculations.

---

#### second_stat
{: #second_stat }

CompanionDatabase.Primary_Stats **second_stat**
* CompanionDatabase.Primary_Stats **get_second_stat**()
* void **set_second_stat**(value: CompanionDatabase.Primary_Stats)

Secondary attribute for class performance calculations.

---

#### class_colour
{: #class_colour }

Color **class_colour**
* Color **get_class_colour**()
* void **set_class_colour**(value: Color)

UI color associated with companion's class.

### State Properties

#### experience
{: #experience }

int **experience**
* int **get_experience**()
* void **set_experience**(value: int)

Current experience points accumulated.

---

#### experience_requirement
{: #experience_requirement }

int **experience_requirement**
* int **get_experience_requirement**()
* void **set_experience_requirement**(value: int)

Experience points needed for next level.

---

#### is_current_player
{: #is_current_player }

bool **is_current_player** = `false`
* bool **get_is_current_player**()
* void **set_is_current_player**(value: bool)

Whether this companion is currently player-controlled.

---

#### follow_stance
{: #follow_stance }

bool **follow_stance** = `false`
* bool **get_follow_stance**()
* void **set_follow_stance**(value: bool)

AI state for following player.

---

#### attack_stance
{: #attack_stance }

bool **attack_stance** = `true`
* bool **get_attack_stance**()
* void **set_attack_stance**(value: bool)

AI state for combat engagement.

---

#### interaction_range
{: #interaction_range }

float **interaction_range** = `3.5`
* float **get_interaction_range**()
* void **set_interaction_range**(value: float)

Maximum distance for interacting with objects.

---

#### role
{: #role }

CompanionDatabase.Spec_Role **role**
* CompanionDatabase.Spec_Role **get_role**()
* void **set_role**(value: CompanionDatabase.Spec_Role)

Current combat role based on specialization.

### Node References

#### interact_ray
{: #interact_ray }

RayCast3D **interact_ray**
* RayCast3D **get_interact_ray**()
* void **set_interact_ray**(value: RayCast3D)

Raycast for detecting interactive objects.

---

#### drop_location
{: #drop_location }

Marker3D **drop_location**
* Marker3D **get_drop_location**()
* void **set_drop_location**(value: Marker3D)

Position marker for item drops.

## Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Extends parent _ready() and calls _companion_setup().

---

#### _setup_ai
{: #_setup_ai }

void **_setup_ai**()

Sets up AI system with reference to self.

---

#### _companion_setup
{: #_companion_setup }

void **_companion_setup**()

Sets up companion-specific features:
* Connects signals
* Sets initial level
* Updates XP UI
* Sets up specialization

---

#### setup_specilization
{: #setup_specilization }

void **setup_specilization**()

Empty function for specialization setup.

---

#### connect_companion_signals
{: #connect_companion_signals }

void **connect_companion_signals**()

Connects experience gain signal to update_experience.

---

#### set_specilization
{: #set_specilization }

void **set_specilization**(_value: int)

Empty function for setting specialization.

---

#### update_experience
{: #update_experience }

void **update_experience**(value: int)

Updates companion's experience and handles leveling:
* Adds experience
* Checks for level up
* Updates UI
* Shows level up message

Parameters:
* value: int - Experience points to add

---

#### interact
{: #interact }

void **interact**()

Performs interaction with raycast target:
* Plays interact animation
* Calls player_interact() on target

---

#### get_drop_position
{: #get_drop_position }

Vector3 **get_drop_position**()

Returns global position of drop_location marker.

---

#### _on_tree_exiting
{: #_on_tree_exiting }

void **_on_tree_exiting**()

Extends parent cleanup when removing companion.