---
layout: default
title: Ability Container
parent: Entity System
nav_order: 4
has_children: true
permalink: /systems/entities/ability-container/
---

# Ability Container

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Child Classes
- [CompanionAbilityContainer](./companion-ability-container.md)

## Description
AbilityContainer serves as the base class for managing abilities for entities in the game. 
It provides core functionality for ability usage, including attempt validation, cooldown management, and global cooldown (GCD) handling.

 Key features:
 - Manages a collection of abilities for an entity
 - Creates ability node trees using [AbilityData]()
 - Handles ability use attempts and validates conditions
 - Manages global cooldown (GCD) for abilities
 - Provides signals for ability use attempts (approved and rejected)