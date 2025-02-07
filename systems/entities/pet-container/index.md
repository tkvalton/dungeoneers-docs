---
layout: default
title: Pet Container
parent: Entity System
nav_order: 8
has_children: true
permalink: /systems/entities/pet-container/
---

# Pet Container

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description
PetsContainer manages the pets owned by an entity. It keeps track of active pets
and integrates with a follow system to manage pet movement and behavior.

Key features:
- Maintains a list of active pets for an entity
- Integrates with a dynamic follower system for pet movement
- Handles adding and removing pets from the entity
