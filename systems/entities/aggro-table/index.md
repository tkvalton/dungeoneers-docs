---
layout: default
title: Aggro Table
parent: Entity System
nav_order: 7
has_children: true
permalink: /systems/entities/aggro-table/
---

# AggroTable

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description

AggroTable manages the aggression (aggro) system for entities like Minions or Bosses. It tracks and calculates aggression levels towards players, influencing target selection and combat behavior.

Key features:
- Maintains an aggro table storing aggression values for each player
- Provides methods for adding, decaying, and resetting aggro
- Handles target selection based on highest aggro
- Manages combat state transitions based on aggro levels
- Responds to entity death or freeing events

## Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Entity | [entity](#entity) | null | The entity (Minion or Boss) that owns this aggro table |
| Dictionary | [aggro_table](#aggro_table) | {} | Dictionary to store player aggro amounts |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Initializes the AggroTable |
| void | [receive_aggro_from_player](#receive_aggro_from_player) | Adds aggro for a player and updates entity's target |
| Entity | [select_target_player](#select_target_player) | Selects the player with the highest aggro as target |
| void | [decay_aggro](#decay_aggro) | Reduces aggro for all players over time |
| void | [reset_target_aggro](#reset_target_aggro) | Resets the aggro for a specific player |
| bool | [all_aggro_null](#all_aggro_null) | Checks if all aggro values are null |
| Entity | [get_highest_aggro_target](#get_highest_aggro_target) | Returns the player with the highest aggro |
| void | [clear_aggro](#clear_aggro) | Clears all aggro values |
| void | [_on_entity_died_or_freed](#_on_entity_died_or_freed) | Handles entity death or freeing event |

## Property Descriptions

#### entity
{: #entity }

Entity **entity** = `null`
* Entity **get_entity**()
* void **set_entity**(value: Entity)

Reference to the entity (Minion or Boss) that owns this aggro table. Set automatically on _ready to the parent node.

---

#### aggro_table
{: #aggro_table }

Dictionary **aggro_table** = `{}`
* Dictionary **get_aggro_table**()
* void **set_aggro_table**(value: Dictionary)

Dictionary storing aggro values for each player. Keys are Entity objects (players) and values are integers representing aggro amount.

## Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Initializes the AggroTable:
* Sets entity reference to parent node
* Connects to PlayerManager's entity_being_set_free signal

---

#### receive_aggro_from_player
{: #receive_aggro_from_player }

void **receive_aggro_from_player**(player: Entity, aggro_amount: int)

Adds aggro for a player and updates entity's target if needed.

Parameters:
* player: Entity - Player generating aggro
* aggro_amount: int - Amount of aggro to add

---

#### select_target_player
{: #select_target_player }

Entity **select_target_player**()

Returns the player with the highest aggro value. Returns null if no players have aggro.

---

#### decay_aggro
{: #decay_aggro }

void **decay_aggro**(decay_factor: float = 0.95)

Reduces aggro for all players by multiplying their aggro by decay_factor. Removes players whose aggro falls below 1.

Parameters:
* decay_factor: float - Multiplier for aggro reduction (default: 0.95)

---

#### reset_target_aggro
{: #reset_target_aggro }

void **reset_target_aggro**(player: Entity)

Removes all aggro for a specific player and updates entity's target if needed.

Parameters:
* player: Entity - Player whose aggro should be reset

---

#### all_aggro_null
{: #all_aggro_null }

bool **all_aggro_null**()

Returns true if aggro table is empty (no players have aggro).

---

#### get_highest_aggro_target
{: #get_highest_aggro_target }

Entity **get_highest_aggro_target**()

Returns the player with the highest aggro. Alias for select_target_player().

---

#### clear_aggro
{: #clear_aggro }

void **clear_aggro**()

Removes all entries from the aggro table and sets entity's target to null.

---

#### _on_entity_died_or_freed
{: #_on_entity_died_or_freed }

void **_on_entity_died_or_freed**(freed_entity: Entity)

Handles cleanup when an entity dies or is freed from the scene.

Parameters:
* freed_entity: Entity - Entity that died or was freed