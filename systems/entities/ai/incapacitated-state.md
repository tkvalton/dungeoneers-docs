---
layout: default
title: Incapacitated State
parent: AI
nav_order: 7
permalink: /systems/entities/ai/incapacitated-state
---

# IncapacitatedState

Inherits: [State](./state.md)

## Description

IncapacitatedState represents a state where the entity is temporarily unable to act. This could be due to stuns, knockdowns, or other crowd control effects. This state manages the entity's movement restrictions and visual representation while incapacitated.

Key features:
- Manages the entity's incapacitated animation
- Stops the entity's movement
- Checks for conditions to transition out of the incapacitated state

## Properties

### Inherited Properties
All properties are inherited from the base [State](./state.md) class:
- entity: Entity
- state_machine: StateMachine

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [enter](#enter) | Called when entering the incapacitated state |
| void | [update](#update) | Called every frame to update the incapacitated state |
| void | [exit](#exit) | Called when exiting the incapacitated state |

# Method Descriptions

#### enter
{: #enter }

void **enter**()

Called when entering the incapacitated state. Performs the following:
- Plays the stun animation
- Sets entity velocity to zero
- Stops entity movement

---

#### update
{: #update }

void **update**(delta: float)

Called every frame to update the incapacitated state. Handles state transitions:
- Changes to "dead" state if entity dies
- Changes to "inactive" state if entity is no longer incapacitated

Parameters:
* delta: float - Time elapsed since last frame (unused)

---

#### exit
{: #exit }

void **exit**()

Called when exiting the incapacitated state. Currently performs no cleanup actions.