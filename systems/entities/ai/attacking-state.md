---
layout: default
title: Attacking State
parent: AI
nav_order: 6
permalink: /systems/entities/ai/attacking-state
---

# Attacking State

Inherits: [State](../ai/state)

## Description
AttackingState represents the state when an entity is actively attacking a target.
It manages the attack timing and transitions to other states based on conditions.

Key features:
- Controls the entity's attack cycle using a timer
- Manages transitions to other states (e.g., dead, target search, chasing)
- Handles the entity's orientation towards the target

A timer use to call the entity to attack