---
layout: default
title: Target Search State
parent: AI
nav_order: 4
permalink: /systems/entities/ai/target-search-state
---

# TargetSearchState

Inherits: [State](./state.md)

## Description

TargetSearchState represents the behavior of an entity actively searching for a target. It manages target selection, aggro tables, and combat state transitions.

Key features:
- Implements target search logic for different entity types (e.g., Minion, Boss, Companion)
- Manages aggro tables for certain entity types
- Handles combat entrance and exit

## Properties

### State Properties
| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Timer | [delayed_exit_timer](#delayed_exit_timer) | null | Timer for delayed combat exit |
| Timer | [search_cooldown_timer](#search_cooldown_timer) | null | Timer between target searches |
| float | [last_search_time](#last_search_time) | 0.0 | Time of last target search |
| float | [cache_duration](#cache_duration) | 1.0 | Duration to cache search results |

### Inherited Properties
All properties are inherited from the base [State](./state.md) class:
- entity: Entity
- state_machine: StateMachine

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Initializes timers |
| void | [enter](#enter) | Enters search state |
| void | [update](#update) | Updates search state |
| void | [exit](#exit) | Exits search state |
| void | [search_for_target](#search_for_target) | Main target search logic |
| Entity | [find_non_aggro_target](#find_non_aggro_target) | Finds targets for companions/pets |
| Entity | [reset_and_select_aggro_target](#reset_and_select_aggro_target) | Selects targets for minions/bosses |
| Entity | [find_new_aggro_target](#find_new_aggro_target) | Finds new aggro-based targets |
| void | [start_delayed_combat_exit](#start_delayed_combat_exit) | Initiates combat exit |
| void | [_on_delayed_combat_exit_timeout](#_on_delayed_combat_exit_timeout) | Handles exit timeout |
| void | [handle_non_aggro_combat_exit](#handle_non_aggro_combat_exit) | Exits for companions/pets |
| void | [handle_aggro_combat_exit](#handle_aggro_combat_exit) | Exits for minions/bosses |
| void | [exit_combat](#exit_combat) | Exits combat state |

# Property Descriptions

#### delayed_exit_timer
{: #delayed_exit_timer }

Timer **delayed_exit_timer**
* Timer **get_delayed_exit_timer**()
* void **set_delayed_exit_timer**(value: Timer)

One-shot timer for delayed combat exit processing.

---

#### search_cooldown_timer
{: #search_cooldown_timer }

Timer **search_cooldown_timer**
* Timer **get_search_cooldown_timer**()
* void **set_search_cooldown_timer**(value: Timer)

One-shot timer controlling search frequency.

---

#### last_search_time
{: #last_search_time }

float **last_search_time** = `0.0`
* float **get_last_search_time**()
* void **set_last_search_time**(value: float)

Timestamp of last target search execution.

---

#### cache_duration
{: #cache_duration }

float **cache_duration** = `1.0`
* float **get_cache_duration**()
* void **set_cache_duration**(value: float)

Duration in seconds to cache search results.

# Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Initializes and configures exit and cooldown timers.

---

#### enter
{: #enter }

void **enter**()

Validates current target or initiates search.

---

#### update
{: #update }

void **update**(delta: float)

Checks for state transitions based on death or target acquisition.

Parameters:
* delta: float - Time since last frame

---

#### exit
{: #exit }

void **exit**()

Stops all active timers.

---

#### search_for_target
{: #search_for_target }

void **search_for_target**()

Executes main target search logic based on entity type.

---

#### find_non_aggro_target
{: #find_non_aggro_target }

Entity **find_non_aggro_target**()

Finds targets for companions/pets using range-based detection.

Returns: Entity or null if no target found

---

#### reset_and_select_aggro_target
{: #reset_and_select_aggro_target }

Entity **reset_and_select_aggro_target**()

Selects targets for minions/bosses using aggro tables.

Returns: Entity or null if no target found

---

#### find_new_aggro_target
{: #find_new_aggro_target }

Entity **find_new_aggro_target**()

Finds new targets using pack information and range detection.

Returns: Entity or null if no target found

---

#### start_delayed_combat_exit
{: #start_delayed_combat_exit }

void **start_delayed_combat_exit**()

Starts delayed exit timer (0.1 seconds).

---

#### _on_delayed_combat_exit_timeout
{: #_on_delayed_combat_exit_timeout }

void **_on_delayed_combat_exit_timeout**()

Routes combat exit handling based on entity type.

---

#### handle_non_aggro_combat_exit
{: #handle_non_aggro_combat_exit }

void **handle_non_aggro_combat_exit**()

Manages combat exit for companions/pets.

---

#### handle_aggro_combat_exit
{: #handle_aggro_combat_exit }

void **handle_aggro_combat_exit**()

Manages combat exit for minions/bosses.

---

#### exit_combat
{: #exit_combat }

void **exit_combat**()

Exits combat and transitions to inactive state.