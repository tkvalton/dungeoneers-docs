---
layout: default
title: Pet Follow System
parent: Entity System
nav_order: 9
has_children: true
permalink: /systems/entities/pet-follow-manager/
---

# Dynamic Follower System (Pet Follow System)

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description
DynamicFollowerSystem manages a group of followers in a dynamic formation around a leader.
It calculates and updates follower positions based on the leader's movement and predefined formation parameters.

Key features:
- Maintains a dynamic formation of followers around a leader
- Allows for customizable formation parameters (distance, angle spread, etc.)
- Uses noise to add slight randomness to follower positions for natural movement
- Ensures followers stay within defined distance limits from the leader
- Provides methods to add/remove followers and update the formation
- Emits signals when the formation is updated for external systems to react
