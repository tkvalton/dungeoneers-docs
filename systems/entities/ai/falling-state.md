---
layout: default
title: Falling State
parent: AI
nav_order: 16
permalink: /systems/entities/ai/falling-state
---

# FallingState

Inherits: [MovementState](./movement-state.md)

## Description

FallingState represents the state when an entity is in mid-air, typically after walking off an edge. It manages the entity's falling animation and transition back to ground-based states.

Key features:
- Plays the falling animation
- Applies gravity to the entity
- Manages transitions to ground-based states when landing

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [enter](#enter) | Called when entering the falling state |
| void | [update](#update) | Updates state logic each frame |
| void | [physics_update](#physics_update) | Updates physics each frame |
| void | [exit](#exit) | Called when exiting the falling state |

## Method Descriptions

#### enter
{: #enter }

void **enter**()

Sets up falling state:
* Sets falling flag
* Plays falling animation

---

#### update
{: #update }

void **update**(_delta: float)

Checks for landing and transitions to appropriate movement state:
* Walking state if moving slowly
* Running state if moving quickly
* Idle state if not moving

Parameters:
* _delta: float - Time elapsed since last frame

---

#### physics_update
{: #physics_update }

void **physics_update**(delta: float)

Applies gravity to the entity each physics frame.

Parameters:
* delta: float - Time elapsed since last physics frame

---

#### exit
{: #exit }

void **exit**()

Handles landing:
* Clears falling flag
* Plays landing animation