---
layout: default
title: Chasing State
parent: AI
nav_order: 5
permalink: /systems/entities/ai/chasing-state
---

# ChasingState

Inherits: [State](./state.md)

## Description

ChasingState represents the state when an entity is pursuing a target. It manages the entity's movement towards the target and transitions to other states based on conditions.

Key features:
- Updates the entity's navigation target to follow the current target
- Manages transitions to other states (e.g., dead, target search, attacking)
- Handles the desired distance for attacking

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [enter](#enter) | Called when entering the chasing state |
| void | [exit](#exit) | Called when exiting the chasing state |
| void | [update](#update) | Updates state logic each frame |
| void | [update_desired_distance](#update_desired_distance) | Updates the desired attack distance |
| bool | [is_in_attack_range](#is_in_attack_range) | Checks if target is in attack range |

## Method Descriptions

#### enter
{: #enter }

void **enter**()

Sets up initial chasing state:
* Enables entity movement
* Updates desired attack distance

---

#### exit
{: #exit }

void **exit**()

Placeholder for state exit behavior.

---

#### update
{: #update }

void **update**(_delta: float)

Updates state logic each frame:
* Checks for state transitions (dead, no target)
* Updates desired distance and navigation target
* Transitions to attacking state when in range

Parameters:
* _delta: float - Time elapsed since last frame

---

#### update_desired_distance
{: #update_desired_distance }

void **update_desired_distance**()

Sets the navigation agent's desired distance to 90% of the basic attack's maximum range.

---

#### is_in_attack_range
{: #is_in_attack_range }

bool **is_in_attack_range**()

Checks if entity's target is within 90% of basic attack range. Returns false if no target exists.