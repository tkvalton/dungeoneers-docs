---
layout: default
title: State
parent: AI
nav_order: 2
permalink: /systems/entities/ai/state
---

# Target Search State

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description
State is the base class for all states in the game's state machine system.
It defines the interface and basic functionality that all states should implement.
Specific states will inherit from this class and override its methods as needed.

Key features:
- Provides a common interface for all states
- Holds references to the state machine and the entity it's controlling
- Defines basic methods for state entry, exit, update, and input handling