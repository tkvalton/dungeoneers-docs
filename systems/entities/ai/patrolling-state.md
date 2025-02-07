---
layout: default
title: Patrolling State
parent: AI
nav_order: 9
permalink: /systems/entities/ai/patrolling-state
---

# PatrollingState

Inherits: [State](./state.md)

## Description

PatrollingState represents the behavior of an entity following a predefined patrol path. It manages the entity's movement between patrol points and handles transitions to other states.

Key features:
- Controls the entity's movement along a patrol path
- Manages transitions between patrol points
- Handles combat interruptions and returns to patrolling after combat

## Properties

### State Properties
| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | [current_point_reached](#current_point_reached) | false | Flag indicating current patrol point reached |
| Timer | [patrol_delay_timer](#patrol_delay_timer) | null | Timer for wait time between points |
| Vector3 | [last_patrol_position](#last_patrol_position) | Vector3.ZERO | Position of last reached patrol point |

### Inherited Properties
All properties are inherited from the base [State](./state.md) class:
- entity: Entity
- state_machine: StateMachine

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Initializes the patrol state |
| void | [enter](#enter) | Called when entering patrol state |
| void | [exit](#exit) | Called when exiting patrol state |
| void | [update](#update) | Updates patrol state each frame |
| void | [_on_last_position_reached](#_on_last_position_reached) | Handles reaching last position |
| void | [_get_next_patrol_marker](#_get_next_patrol_marker) | Gets next patrol point |
| void | [_on_patrol_target_reached](#_on_patrol_target_reached) | Handles reaching patrol point |
| void | [continue_patrol](#continue_patrol) | Continues patrol after delay |
| void | [_on_patrol_delay_timer_timeout](#_on_patrol_delay_timer_timeout) | Handles delay timer timeout |

# Property Descriptions

#### current_point_reached
{: #current_point_reached }

bool **current_point_reached** = `false`
* bool **is_current_point_reached**()
* void **set_current_point_reached**(value: bool)

Flag indicating whether entity has reached current patrol point.

---

#### patrol_delay_timer
{: #patrol_delay_timer }

Timer **patrol_delay_timer**
* Timer **get_patrol_delay_timer**()
* void **set_patrol_delay_timer**(value: Timer)

Timer controlling wait time between patrol points. One-shot timer.

---

#### last_patrol_position
{: #last_patrol_position }

Vector3 **last_patrol_position**
* Vector3 **get_last_patrol_position**()
* void **set_last_patrol_position**(value: Vector3)

Last reached patrol point position. Initially set to spawn point.

# Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Initializes patrol state:
- Creates patrol delay timer
- Connects timer timeout
- Sets initial patrol position

---

#### enter
{: #enter }

void **enter**()

Called when entering patrol state:
- Sets navigation target to last position
- Connects position reached signal

---

#### exit
{: #exit }

void **exit**()

Called when exiting patrol state:
- Stops delay timer
- Disables walking
- Saves last position

---

#### update
{: #update }

void **update**(delta: float)

Updates patrol state:
- Checks for death state
- Handles combat interruption

Parameters:
* delta: float - Time since last frame

---

#### _on_last_position_reached
{: #_on_last_position_reached }

void **_on_last_position_reached**()

Handles reaching last patrol position by getting next marker.

---

#### _get_next_patrol_marker
{: #_get_next_patrol_marker }

void **_get_next_patrol_marker**()

Gets next patrol marker:
- Handles patrol path completion
- Sets new navigation target
- Updates movement flags

---

#### _on_patrol_target_reached
{: #_on_patrol_target_reached }

void **_on_patrol_target_reached**()

Handles reaching patrol target:
- Updates marker status
- Stops movement
- Updates pack status

---

#### continue_patrol
{: #continue_patrol }

void **continue_patrol**()

Starts delay timer for patrol continuation if not in combat.

---

#### _on_patrol_delay_timer_timeout
{: #_on_patrol_delay_timer_timeout }

void **_on_patrol_delay_timer_timeout**()

Gets next patrol marker when delay timer expires.