---
layout: default
title: Stats
parent: Entity System
nav_order: 3
has_children: true
permalink: /systems/entities/stats/
---

# Entity Stats Container

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description
EntityStatsContainer manages all stats and attributes for an entity. It handles
stat calculations, modifications, and interactions such as taking damage or healing.

Key features:
- Manages base, major, and minor stats for entities
- Handles health and resource management
- Processes damage application, including avoidance and mitigation
- Manages healing and resource regeneration
- Provides methods for modifying and querying stats