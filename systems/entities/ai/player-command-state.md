---
layout: default
title: Player Command State
parent: AI
nav_order: 11
permalink: /systems/entities/ai/player-command-state
---

# PlayerCommandState

Inherits: [State](./state.md)

## Description

PlayerCommandState manages the execution of player-issued commands, handling command timing and state transitions.

## Properties

### State Properties
| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Timer | [command_timer](#command_timer) | null | Timer for command duration |
| Timer | [return_to_inactive_timer](#return_to_inactive_timer) | null | Timer for state transition delay |

### Inherited Properties
All properties are inherited from the base [State](./state.md) class:
- entity: Entity
- state_machine: StateMachine

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Initializes timers |
| void | [enter](#enter) | Enters command state |
| void | [exit](#exit) | Exits command state |
| void | [update](#update) | Updates command state |
| void | [_on_command_timer_timeout](#_on_command_timer_timeout) | Handles command timeout |
| void | [_start_return_to_inactive](#_start_return_to_inactive) | Initiates inactive transition |
| void | [_on_return_to_inactive_timeout](#_on_return_to_inactive_timeout) | Handles transition timeout |

# Property Descriptions

#### command_timer
{: #command_timer }

Timer **command_timer**
* Timer **get_command_timer**()
* void **set_command_timer**(value: Timer)

One-shot timer controlling command duration (4 seconds).

---

#### return_to_inactive_timer
{: #return_to_inactive_timer }

Timer **return_to_inactive_timer**
* Timer **get_return_to_inactive_timer**()
* void **set_return_to_inactive_timer**(value: Timer)

One-shot timer for transition delay (1 second).

# Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Initializes and configures command and transition timers.

---

#### enter
{: #enter }

void **enter**()

Sets movement flags, navigation distance, and starts command timer.

---

#### exit
{: #exit }

void **exit**()

Stops movement and all timers.

---

#### update
{: #update }

void **update**(delta: float)

Checks for state transitions based on:
- Death state
- Incapacitation
- Navigation completion

Parameters:
* delta: float - Time since last frame

---

#### _on_command_timer_timeout
{: #_on_command_timer_timeout }

void **_on_command_timer_timeout**()

Initiates return to inactive state on command timeout.

---

#### _start_return_to_inactive
{: #_start_return_to_inactive }

void **_start_return_to_inactive**()

Stops movement and starts transition timer.

---

#### _on_return_to_inactive_timeout
{: #_on_return_to_inactive_timeout }

void **_on_return_to_inactive_timeout**()

Changes to inactive state after transition delay.