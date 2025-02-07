---
layout: default
title: State Machine
parent: AI
nav_order: 1
permalink: /systems/entities/ai/state-machine
---

# Target Search State

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description
StateMachine manages the state system for entities in the game.
It handles transitions between different movement and action states,
coordinates AI behavior, and manages combat interactions.

Key features:
- Manages separate movement and action states
- Dynamically creates state nodes based on configuration
- Handles state transitions and updates
- Coordinates with combat scripts for AI behavior
- Manages detection areas for entity interactions
- Provides flexibility for different entity types (e.g., companions, bosses)