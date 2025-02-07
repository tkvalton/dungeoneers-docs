---
layout: default
title: Patrolling State
parent: AI
nav_order: 9
permalink: /systems/entities/ai/patrolling-state
---

# Patrolling State

Inherits: [State](../ai/state)

## Description
PatrollingState represents the behavior of an entity following a predefined patrol path.
It manages the entity's movement between patrol points and handles transitions to other states.

Key features:
- Controls the entity's movement along a patrol path
- Manages transitions between patrol points
- Handles combat interruptions and returns to patrolling after combat