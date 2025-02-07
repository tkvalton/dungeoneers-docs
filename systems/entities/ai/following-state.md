---
layout: default
title: following State
parent: AI
nav_order: 8
permalink: /systems/entities/ai/following-state
---

# FollowingState

Inherits: [State](./state.md)

## Description

FollowingState represents the state when an entity is following another entity or a specific position. It's typically used for companions or pets that need to stay close to their owner or designated position.

Key features:
- Updates the entity's navigation target to follow the designated position
- Manages transitions to other states based on combat status or proximity to target
- Handles different following behaviors for companions and pets

## Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Vector3 | [target_position](#target_position) | Vector3.ZERO | Position the entity is following |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [update](#update) | Updates state logic each frame |

## Property Descriptions

#### target_position
{: #target_position }

Vector3 **target_position** = `Vector3.ZERO`
* Vector3 **get_target_position**()
* void **set_target_position**(value: Vector3)

Position in world space that the entity is currently following. For pets, this is determined by their summoner's pet follower system.

## Method Descriptions

#### update
{: #update }

void **update**(_delta: float)

Updates state logic each frame:
* Checks for state transitions (dead, in combat, current player)
* Updates target position for pets
* Manages movement and navigation
* Transitions to inactive when close to target

Parameters:
* _delta: float - Time elapsed since last frame