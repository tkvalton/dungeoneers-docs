---
layout: default
title: Rig
parent: Entity System
nav_order: 2
has_children: true
permalink: /systems/entities/rig/
---

# Rig

Inherits: [Node3D](https://docs.godotengine.org/en/stable/classes/class_node3d.html)

## Child Classes
- [EntityRig](./entity-rig.md)
- [ModularCompanionRig](./modular-companion-rig.md)

## Description
RigController manages the visual representation, animations, and attachments
for entities in the game. It handles mesh instances, outline effects, remote
transforms for VFX, and various visual states of the entity.

Key features:
- Manages mesh instances and their materials
- Handles outline effects for selection and targeting
- Manages attachment points for weapons and VFX
- Controls casting VFX and transparency effects
- Integrates with the game's selection and targeting systems
- Holds the AnimationPlayer for the entity