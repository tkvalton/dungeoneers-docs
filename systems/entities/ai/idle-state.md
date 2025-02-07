---
layout: default
title: Idle State
parent: AI
nav_order: 13
permalink: /systems/entities/ai/idle-state
---

# IdleState

Inherits: [MovementState](./movement-state.md)

## Description

IdleState represents the idle behavior of an entity. In this state, the entity is not moving but may transition to other states based on input or conditions.

Key features:
- Handles the entity's idle animation
- Checks for conditions to transition to other states (e.g., walking, running)
- Applies gravity to the entity

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [enter](#enter) | Called when entering the idle state |
| void | [update](#update) | Updates state logic each frame |
| void | [physics_update](#physics_update) | Updates physics each frame |

## Method Descriptions

#### enter
{: #enter }

void **enter**()

Sets up idle state:
* Stops movement
* Plays appropriate idle animation based on combat status

---

#### update
{: #update }

void **update**(delta: float)

Handles movement and state transitions:
* Processes movement input
* Transitions to walking/running states when moving

Parameters:
* delta: float - Time elapsed since last frame

---

#### physics_update
{: #physics_update }

void **physics_update**(delta: float)

Applies gravity to the entity each physics frame.

Parameters:
* delta: float - Time elapsed since last physics frame