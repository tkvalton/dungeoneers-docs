---
layout: default
title: Idle State
parent: AI
nav_order: 13
permalink: /systems/entities/ai/idle-state
---

# Idle State

Inherits: [MovementState](../ai/movement-state)

## Description
IdleState represents the idle behavior of an entity.
In this state, the entity is not moving but may transition to other states based on input or conditions.

Key features:
- Handles the entity's idle animation
- Checks for conditions to transition to other states (e.g., walking, running)
- Applies gravity to the entity