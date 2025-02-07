---
layout: default
title: AttackingState
parent: AI
nav_order: 6
permalink: /systems/entities/ai/attacking-state
---

# AttackingState

Inherits: [State](./state.md)

## Description

AttackingState represents the state when an entity is actively attacking a target. It manages the attack timing and transitions to other states based on conditions.

Key features:
- Controls the entity's attack cycle using a timer
- Manages transitions to other states (e.g., dead, target search, chasing)
- Handles the entity's orientation towards the target

## Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Timer | [attack_timer](#attack_timer) | null | Timer that controls attack frequency |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Creates and configures the attack timer |
| void | [enter](#enter) | Called when entering the attacking state |
| void | [exit](#exit) | Called when exiting the attacking state |
| void | [update](#update) | Updates state logic each frame |
| void | [_on_attack_timer_timeout](#_on_attack_timer_timeout) | Handles attack timer completion |
| bool | [is_in_attack_range](#is_in_attack_range) | Checks if target is in attack range |

## Property Descriptions

#### attack_timer
{: #attack_timer }

Timer **attack_timer** = `null`
* Timer **get_attack_timer**()
* void **set_attack_timer**(value: Timer)

Timer that triggers entity attacks at regular intervals. Configured with a 0.5 second interval and non-one-shot behavior.

## Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Creates and initializes the attack timer:
* Sets up non-one-shot behavior
* Connects timeout signal
* Adds timer to scene tree

---

#### enter
{: #enter }

void **enter**()

Starts the attack timer with a 0.5 second interval when entering the state.

---

#### exit
{: #exit }

void **exit**()

Stops the attack timer when exiting the state.

---

#### update
{: #update }

void **update**(_delta: float)

Updates state logic each frame:
* Checks for state transitions (dead, no target)
* Updates entity facing direction
* Handles casting immobilization
* Manages combat range transitions

Parameters:
* _delta: float - Time elapsed since last frame

---

#### _on_attack_timer_timeout
{: #_on_attack_timer_timeout }

void **_on_attack_timer_timeout**()

Triggered when attack timer completes:
* Checks for incapacitation
* Verifies target and range
* Initiates attack through combat script

---

#### is_in_attack_range
{: #is_in_attack_range }

bool **is_in_attack_range**()

Checks if entity's target is within basic attack range. Returns false if no target exists.