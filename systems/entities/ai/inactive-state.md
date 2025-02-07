---
layout: default
title: Inactive State
parent: AI
nav_order: 3
permalink: /systems/entities/ai/inactive-state
---

# InactiveState

Inherits: [State](./state.md)

## Description

InactiveState represents a state where the entity is not actively engaged in any action. It handles transitions to other states based on various conditions.

Key features:
- Manages idle animations for combat and non-combat situations
- Handles returning to spawn point for certain entity types
- Checks for conditions to transition to other states (e.g., dead, incapacitated, chasing)

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [enter](#enter) | Called when entering the inactive state |
| void | [update](#update) | Updates state logic each frame |
| void | [return_to_spawn](#return_to_spawn) | Handles returning to spawn point |
| void | [_on_spawn_reached](#_on_spawn_reached) | Called when spawn point is reached |
| void | [exit](#exit) | Called when exiting the inactive state |

## Method Descriptions

#### enter
{: #enter }

void **enter**()

Initializes inactive state:
* Updates combat status based on target distance
* Sets appropriate idle animation
* Initiates spawn return for Minions/Bosses

---

#### update
{: #update }

void **update**(_delta: float)

Updates state logic each frame and handles transitions:
* Dead state if entity is dead
* Incapacitated state if stunned
* Chasing/attacking if has target
* Patrolling if available and not in combat

Parameters:
* _delta: float - Time elapsed since last frame

---

#### return_to_spawn
{: #return_to_spawn }

void **return_to_spawn**()

Manages entity return to spawn point:
* Sets navigation target
* Enables movement
* Handles signal connections

---

#### _on_spawn_reached
{: #_on_spawn_reached }

void **_on_spawn_reached**()

Stops movement when spawn point is reached.

---

#### exit
{: #exit }

void **exit**()

Cleans up spawn point navigation signal connections.