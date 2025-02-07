---
layout: default
title: dead State
parent: AI
nav_order: 10
permalink: /systems/entities/ai/dead-state
---

# Chasing State

Inherits: [State](../ai/state)

## Description
DeadState represents the state when an entity has been defeated.
It manages the entity's death animation and prevents further actions until revival.

Key features:
- Plays the death animation
- Stops all movement and actions
- Handles potential revival transitions