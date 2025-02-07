---
layout: default
title: Target Search State
parent: AI
nav_order: 4
permalink: /systems/entities/ai/target-search-state
---

# Target Search State

Inherits: [State](../ai/state)

## Description
TargetSearchState represents the behavior of an entity actively searching for a target.
It manages the process of finding and selecting targets, and handles transitions to other states.

Key features:
- Implements target search logic for different entity types (e.g., Minion, Boss, Companion)
- Manages aggro tables for certain entity types
- Handles combat entrance and exit