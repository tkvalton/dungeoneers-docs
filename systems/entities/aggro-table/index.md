---
layout: default
title: Aggro Table
parent: Entity System
nav_order: 7
has_children: true
permalink: /systems/entities/aggro-table/
---

# Aggro Table

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description
AggroTable manages the aggression (aggro) system for entities like Minions or Bosses.
It tracks and calculates aggression levels towards players, influencing target selection and combat behavior.

Key features:
- Maintains an aggro table storing aggression values for each player
- Provides methods for adding, decaying, and resetting aggro
- Handles target selection based on highest aggro
- Manages combat state transitions based on aggro levels
- Responds to entity death or freeing events