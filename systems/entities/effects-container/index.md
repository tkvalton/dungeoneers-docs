---
layout: default
title: Effects Container
parent: Entity System
nav_order: 5
has_children: true
permalink: /systems/entities/effects-container/
---

# EffectsContainer

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description

EffectsContainer manages all active effects on an entity. It handles the addition, removal, and tracking of various effects that can be applied to entities in the game.

Key features:
- Maintains a list of all active effects on the entity
- Handles the application and removal of effects
- Provides methods for querying and managing effects

## Properties

### General Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Entity | [entity](#entity) | null | Owner entity reference |
| Array[Effect] | [active_effects](#active_effects) | [] | Currently active effects |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [gained_effect](#gained_effect) | Adds new effect |
| void | [lost_effect](#lost_effect) | Removes effect |
| void | [remove_all_effects](#remove_all_effects) | Clears all effects |
| Effect | [get_effect](#get_effect) | Gets effect by ID |
| Effect | [get_effect_from_caller](#get_effect_from_caller) | Gets effect by ID and source |

## Property Descriptions

#### entity
{: #entity }

Entity **entity**
* Entity **get_entity**()
* void **set_entity**(value: Entity)

Reference to the entity these effects are applied to.

---

#### active_effects
{: #active_effects }

Array[Effect] **active_effects** = `[]`
* Array[Effect] **get_active_effects**()
* void **set_active_effects**(value: Array[Effect])

Array of all currently active effects on the entity.

## Method Descriptions

#### gained_effect
{: #gained_effect }

void **gained_effect**(effect: Effect)

Adds new effect and emits signal.

Parameters:
* effect: Effect - Effect to add

---

#### lost_effect
{: #lost_effect }

void **lost_effect**(effect: Effect)

Removes effect and emits signal.

Parameters:
* effect: Effect - Effect to remove

---

#### remove_all_effects
{: #remove_all_effects }

void **remove_all_effects**()

Removes all active effects from the entity.

---

#### get_effect
{: #get_effect }

Effect **get_effect**(effect_id: int)

Gets effect by ID.

Parameters:
* effect_id: int - ID to search for

Returns: Effect or null if not found

---

#### get_effect_from_caller
{: #get_effect_from_caller }

Effect **get_effect_from_caller**(effect_id: int, caller: Entity)

Gets effect by ID and originator.

Parameters:
* effect_id: int - ID to search for
* caller: Entity - Originating entity

Returns: Effect or null if not found