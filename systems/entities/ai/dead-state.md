---
layout: default
title: dead State
parent: AI
nav_order: 10
permalink: /systems/entities/ai/dead-state
---

# DeadState

Inherits: [State](./state.md)

## Description

DeadState represents the state when an entity has been defeated. It manages the entity's death animation and prevents further actions until revival.

Key features:
- Plays the death animation
- Stops all movement and actions
- Handles potential revival transitions

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [enter](#enter) | Called when entering the dead state |
| void | [update](#update) | Updates state logic each frame |
| void | [exit](#exit) | Called when exiting the dead state |
| void | [handle_input](#handle_input) | Handles input while in dead state |

## Method Descriptions

#### enter
{: #enter }

void **enter**()

Initializes dead state:
* Plays death animation
* Stops movement
* Sets dead status
* Emits death signal for Minions

---

#### update
{: #update }

void **update**(_delta: float)

Checks for revival conditions and transitions to inactive state if revived.

Parameters:
* _delta: float - Time elapsed since last frame

---

#### exit
{: #exit }

void **exit**()

Handles revival:
* Clears dead status
* Resets pull state for Minions

---

#### handle_input
{: #handle_input }

void **handle_input**(_event: InputEvent)

Ignores all input while in dead state.

Parameters:
* _event: InputEvent - Input event to ignore