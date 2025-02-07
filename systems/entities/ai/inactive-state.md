---
layout: default
title: Inactive State
parent: AI
nav_order: 3
permalink: /systems/entities/ai/inactive-state
---

# Inactive State

Inherits: [State](../ai/state)

## Description
InactiveState represents a state where the entity is not actively engaged in any action.
It handles transitions to other states based on various conditions.

Key features:
- Manages idle animations for combat and non-combat situations
- Handles returning to spawn point for certain entity types
- Checks for conditions to transition to other states (e.g., dead, incapacitated, chasing)