---
layout: default
title: Chasing State
parent: AI
nav_order: 5
permalink: /systems/entities/ai/chasing-state
---

# Chasing State

Inherits: [State](../ai/state)

## Description
ChasingState represents the state when an entity is pursuing a target.
It manages the entity's movement towards the target and transitions to other states based on conditions.

Key features:
- Updates the entity's navigation target to follow the current target
- Manages transitions to other states (e.g., dead, target search, attacking)
- Handles the desired distance for attacking