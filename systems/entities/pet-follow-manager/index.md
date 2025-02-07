---
layout: default
title: Pet Follow System
parent: Entity System
nav_order: 9
has_children: true
permalink: /systems/entities/pet-follow-manager/
---

# DynamicFollowerSystem

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description

DynamicFollowerSystem manages a group of followers in a dynamic formation around a leader. It calculates and updates follower positions based on the leader's movement and predefined formation parameters.

Key features:
- Maintains a dynamic formation of followers around a leader
- Allows for customizable formation parameters (distance, angle spread, etc.)
- Uses noise to add slight randomness to follower positions for natural movement
- Ensures followers stay within defined distance limits from the leader
- Provides methods to add/remove followers and update the formation
- Emits signals when the formation is updated

## Signals

| Signal | Description |
|--------|-------------|
| formation_updated | Emitted when formation positions are recalculated |

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Node3D | [leader](#leader) | null | Entity that followers follow |
| float | [follow_distance](#follow_distance) | 3.0 | Ideal follower distance |
| float | [min_distance](#min_distance) | 1.5 | Minimum follower distance |
| float | [max_distance](#max_distance) | 5.0 | Maximum follower distance |
| float | [angle_spread](#angle_spread) | PI/2 | Formation spread angle |
| float | [update_interval](#update_interval) | 0.1 | Update check frequency |
| float | [movement_threshold](#movement_threshold) | 0.1 | Minimum movement distance |

### General Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Array[Entity] | [followers](#followers) | [] | Current followers |
| Dictionary | [target_positions](#target_positions) | {} | Follower target positions |
| FastNoiseLite | [noise](#noise) | null | Position noise generator |
| Vector3 | [last_leader_position](#last_leader_position) | Vector3.ZERO | Last leader position |

### Node References

| Type | Property | Description |
|------|----------|-------------|
| Timer | [update_timer](#update_timer) | Formation update timer |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Initializes the system |
| void | [add_follower](#add_follower) | Adds new follower |
| void | [remove_follower](#remove_follower) | Removes follower |
| void | [update_formation](#update_formation) | Recalculates positions |
| Vector3 | [get_target_position](#get_target_position) | Gets follower position |
| void | [_on_update_timer_timeout](#_on_update_timer_timeout) | Checks leader movement |
| void | [set_leader](#set_leader) | Changes formation leader |

# Property Descriptions

## Exported Properties

#### leader
{: #leader }

Node3D **leader**
* Node3D **get_leader**()
* void **set_leader**(value: Node3D)

Entity that followers track and form around.

---

#### follow_distance
{: #follow_distance }

float **follow_distance** = `3.0`
* float **get_follow_distance**()
* void **set_follow_distance**(value: float)

Target distance followers maintain from leader.

---

#### min_distance
{: #min_distance }

float **min_distance** = `1.5`
* float **get_min_distance**()
* void **set_min_distance**(value: float)

Minimum allowed distance between follower and leader.

---

#### max_distance
{: #max_distance }

float **max_distance** = `5.0`
* float **get_max_distance**()
* void **set_max_distance**(value: float)

Maximum allowed distance between follower and leader.

---

#### angle_spread
{: #angle_spread }

float **angle_spread** = `PI/2`
* float **get_angle_spread**()
* void **set_angle_spread**(value: float)

Formation spread angle in radians (PI/2 is 90 degrees).

---

#### update_interval
{: #update_interval }

float **update_interval** = `0.1`
* float **get_update_interval**()
* void **set_update_interval**(value: float)

Time between leader movement checks in seconds.

---

#### movement_threshold
{: #movement_threshold }

float **movement_threshold** = `0.1`
* float **get_movement_threshold**()
* void **set_movement_threshold**(value: float)

Minimum leader movement distance to trigger update.

## General Properties

#### followers
{: #followers }

Array[Entity] **followers** = `[]`
* Array[Entity] **get_followers**()
* void **set_followers**(value: Array[Entity])

Array of entities currently following the leader.

---

#### target_positions
{: #target_positions }

Dictionary **target_positions** = `{}`
* Dictionary **get_target_positions**()
* void **set_target_positions**(value: Dictionary)

Maps followers to their current target positions.

---

#### noise
{: #noise }

FastNoiseLite **noise**
* FastNoiseLite **get_noise**()
* void **set_noise**(value: FastNoiseLite)

Noise generator for natural position variation.

---

#### last_leader_position
{: #last_leader_position }

Vector3 **last_leader_position** = `Vector3.ZERO`
* Vector3 **get_last_leader_position**()
* void **set_last_leader_position**(value: Vector3)

Last recorded world position of leader.

## Node References

#### update_timer
{: #update_timer }

Timer **update_timer**
* Timer **get_update_timer**()
* void **set_update_timer**(value: Timer)

Timer controlling formation update checks.

## Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Initializes the follower system:
* Sets up noise generator
* Configures update timer
* Records initial leader position

---

#### add_follower
{: #add_follower }

void **add_follower**(follower: Entity)

Adds new follower to formation.

Parameters:
* follower: Entity - Follower to add

---

#### remove_follower
{: #remove_follower }

void **remove_follower**(follower: Entity)

Removes follower from formation.

Parameters:
* follower: Entity - Follower to remove

---

#### update_formation
{: #update_formation }

void **update_formation**()

Updates formation positions:
* Calculates base positions by angle
* Adds noise for natural movement
* Ensures distance constraints
* Emits formation_updated signal

---

#### get_target_position
{: #get_target_position }

Vector3 **get_target_position**(follower: Entity)

Gets target position for specific follower.

Parameters:
* follower: Entity - Follower to get position for

Returns: Target world position

---

#### _on_update_timer_timeout
{: #_on_update_timer_timeout }

void **_on_update_timer_timeout**()

Checks for leader movement:
* Compares current/last positions
* Updates formation if moved enough
* Updates last position

---

#### set_leader
{: #set_leader }

void **set_leader**(new_leader: Node3D)

Changes formation leader.

Parameters:
* new_leader: Node3D - New leader entity