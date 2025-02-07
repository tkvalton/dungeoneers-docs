---
layout: default
title: State
parent: AI
nav_order: 2
permalink: /systems/entities/ai/state
---

# State

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description

State is the base class for all states in the game's state machine system. It defines the interface and basic functionality that all states should implement. Specific states will inherit from this class and override its methods as needed.

Key features:
- Provides a common interface for all states
- Holds references to the state machine and the entity it's controlling
- Defines basic methods for state entry, exit, update, and input handling

## Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| StateMachine | [state_machine](#state_machine) | null | Reference to the state machine this state belongs to |
| Entity | [entity](#entity) | null | Reference to the entity this state is controlling |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [enter](#enter) | Called when entering the state |
| void | [exit](#exit) | Called when exiting the state |
| void | [update](#update) | Called every frame to update the state |
| void | [physics_update](#physics_update) | Called every physics frame to update the state |
| void | [handle_input](#handle_input) | Called to handle input in this state |

## Property Descriptions

#### state_machine
{: #state_machine }

StateMachine **state_machine** = `null`
* StateMachine **get_state_machine**()
* void **set_state_machine**(value: StateMachine)

Reference to the state machine that owns and manages this state.

---

#### entity
{: #entity }

Entity **entity** = `null`
* Entity **get_entity**()
* void **set_entity**(value: Entity)

Reference to the entity whose behavior this state controls.

## Method Descriptions

#### enter
{: #enter }

void **enter**()

Called when the state machine transitions to this state. Override to define state entry behavior.

---

#### exit
{: #exit }

void **exit**()

Called when the state machine transitions away from this state. Override to define state exit behavior.

---

#### update
{: #update }

void **update**(_delta: float)

Called every frame to update the state logic.

Parameters:
* _delta: float - Time elapsed since last frame

---

#### physics_update
{: #physics_update }

void **physics_update**(_delta: float)

Called every physics frame to update the state physics.

Parameters:
* _delta: float - Time elapsed since last physics frame

---

#### handle_input
{: #handle_input }

void **handle_input**(_event: InputEvent)

Called to process input events while in this state.

Parameters:
* _event: InputEvent - Input event to handle