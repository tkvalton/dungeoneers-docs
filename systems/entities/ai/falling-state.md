---
layout: default
title: Falling State
parent: AI
nav_order: 16
permalink: /systems/entities/ai/falling-state
---

# Falling State

Inherits: [MovementState](../ai/movement-state)

## Description
FallingState represents the state when an entity is in mid-air, typically after walking off an edge.
It manages the entity's falling animation and transition back to ground-based states.

Key features:
- Plays the falling animation
- Applies gravity to the entity
- Manages transitions to ground-based states when landing