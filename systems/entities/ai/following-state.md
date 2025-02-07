---
layout: default
title: following State
parent: AI
nav_order: 8
permalink: /systems/entities/ai/following-state
---

# Following State

Inherits: [State](../ai/state)

## Description
FollowingState represents the state when an entity is following another entity or a specific position.
It's typically used for companions or pets that need to stay close to their owner or designated position.

Key features:
- Updates the entity's navigation target to follow the designated position
- Manages transitions to other states based on combat status or proximity to target
- Handles different following behaviors for companions and pets