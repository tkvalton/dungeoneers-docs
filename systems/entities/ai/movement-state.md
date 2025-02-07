---
layout: default
title: Movement State
parent: AI
nav_order: 12
permalink: /systems/entities/ai/movement-state
---

# MovementState

Inherits: [State](./state.md)

## Description

MovementState is a base class for states that involve entity movement. It provides common functionality for handling movement, gravity, and animations.

Key features:
- Applies gravity to the entity
- Handles basic movement logic
- Manages movement animations

## Properties

### Base Properties
| Type | Property | Default | Description |
|------|----------|---------|-------------|
| float | [gravity](#gravity) | ProjectSettings physics/3d/default_gravity | Gravity force applied to entity |

### Inherited Properties
All properties are inherited from the base [State](./state.md) class:
- entity: Entity
- state_machine: StateMachine

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [handle_movement](#handle_movement) | Handles entity movement logic |
| void | [apply_gravity](#apply_gravity) | Applies gravity to the entity |
| void | [move_to_point](#move_to_point) | Moves entity towards a target point |
| void | [play_animation](#play_animation) | Plays specified animation |
| void | [play_idle_animation](#play_idle_animation) | Plays idle animation based on combat state |
| void | [play_falling_animation](#play_falling_animation) | Plays falling animation |
| void | [play_land_animation](#play_land_animation) | Plays landing animation |

# Property Descriptions

#### gravity
{: #gravity }

float **gravity** = `ProjectSettings.get_setting("physics/3d/default_gravity")`
* float **get_gravity**()
* void **set_gravity**(value: float)

Gravity force applied to the entity during movement. Uses project default gravity setting.

# Method Descriptions

#### handle_movement
{: #handle_movement }

void **handle_movement**(delta: float)

Handles entity movement logic including:
- Floor checks
- Flying state checks
- Falling state transitions
- Movement restrictions

Parameters:
* delta: float - Time elapsed since last frame

---

#### apply_gravity
{: #apply_gravity }

void **apply_gravity**(delta: float)

Applies gravity to the entity when not on floor.

Parameters:
* delta: float - Time elapsed since last frame

---

#### move_to_point
{: #move_to_point }

void **move_to_point**(speed_multiplier: float = 1.0)

Moves entity towards a target point. Handles:
- Cast restrictions
- Distance calculations
- Movement speed
- Direction facing
- Formation updates for companions

Parameters:
* speed_multiplier: float - Multiplier for movement speed

---

#### play_animation
{: #play_animation }

void **play_animation**(animation: NodeUtility.AnimationName)

Plays specified animation if not already playing.

Parameters:
* animation: NodeUtility.AnimationName - Animation to play

---

#### play_idle_animation
{: #play_idle_animation }

void **play_idle_animation**(in_combat: bool)

Plays appropriate idle animation based on combat state.

Parameters:
* in_combat: bool - Whether entity is in combat

---

#### play_falling_animation
{: #play_falling_animation }

void **play_falling_animation**()

Plays falling animation if not already playing.

---

#### play_land_animation
{: #play_land_animation }

void **play_land_animation**()

Plays landing animation based on fall impact (currently defaults to soft landing).