---
layout: default
title: Walking State
parent: AI
nav_order: 15
permalink: /systems/entities/ai/walking-state
---

# WalkingState

Inherits: [MovementState](./movement-state.md)

## Description

WalkingState represents an entity moving at reduced speed. It manages transitions between idle and running states and controls walking animations. Walking movement is set to 25% of running speed.

Key features:
- Controls reduced-speed movement behavior
- Manages walking animation state
- Handles transitions to idle and running states
- Applies gravity and movement calculations

## Properties

### Inherited Properties
All properties are inherited from [MovementState](./movement-state.md):
- gravity: float

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [enter](#enter) | Called when entering walking state |
| void | [update](#update) | Updates walking state each frame |
| void | [physics_update](#physics_update) | Handles physics calculations |
| void | [exit](#exit) | Called when exiting walking state |

# Method Descriptions

#### enter
{: #enter }

void **enter**()

Enables walking flag and plays walking animation.

---

#### update
{: #update }

void **update**(delta: float)

Updates walking state and checks for transitions to idle or running states.

Parameters:
* delta: float - Time since last frame

---

#### physics_update
{: #physics_update }

void **physics_update**(delta: float)

Moves entity at 25% speed and applies gravity.

Parameters:
* delta: float - Time since last frame

---

#### exit
{: #exit }

void **exit**()

Disables walking flag.