---
layout: default
title: Running State
parent: AI
nav_order: 14
permalink: /systems/entities/ai/running-state
---

# RunningState

Inherits: [MovementState](./movement-state.md)

## Description

RunningState represents an entity moving at full speed. It manages transition logic between different movement states and handles running animations.

Key features:
- Controls full-speed movement behavior
- Manages running animation state
- Handles transitions to idle and walking states
- Applies gravity and movement calculations

## Properties

### Inherited Properties
All properties are inherited from [MovementState](./movement-state.md):
- gravity: float

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [enter](#enter) | Called when entering running state |
| void | [update](#update) | Updates running state each frame |
| void | [physics_update](#physics_update) | Handles physics calculations |

# Method Descriptions

#### enter
{: #enter }

void **enter**()

Initializes running state:
- Disables walking flag
- Plays running animation

---

#### update
{: #update }

void **update**(delta: float)

Updates running state:
- Handles movement logic
- Checks for state transitions to idle or walking

Parameters:
* delta: float - Time since last frame

---

#### physics_update
{: #physics_update }

void **physics_update**(delta: float)

Handles physics updates:
- Moves entity at full speed
- Applies gravity effects

Parameters:
* delta: float - Time since last frame
