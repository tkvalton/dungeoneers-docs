---
layout: default
title: Pet Container
parent: Entity System
nav_order: 8
has_children: true
permalink: /systems/entities/pet-container/
---

# PetsContainer

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description

PetsContainer manages the pets owned by an entity. It serves as a central system for tracking active pets and managing their movement through a follower system.

Key features:
- Maintains a list of active pets for an entity
- Integrates with a dynamic follower system for pet movement
- Handles adding and removing pets from the entity

## Properties

### General Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Array[Pet] | [active_pets](#active_pets) | [] | Currently active pets |
| DynamicFollowerSystem | [follow_system](#follow_system) | null | Pet movement system |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [gained_pet](#gained_pet) | Adds new pet |
| void | [lost_pet](#lost_pet) | Removes pet |

## Property Descriptions

#### active_pets
{: #active_pets }

Array[Pet] **active_pets** = `[]`
* Array[Pet] **get_active_pets**()
* void **set_active_pets**(value: Array[Pet])

Array of currently active pets owned by the entity.

---

#### follow_system
{: #follow_system }

DynamicFollowerSystem **follow_system**
* DynamicFollowerSystem **get_follow_system**()
* void **set_follow_system**(value: DynamicFollowerSystem)

Reference to the system managing pet movement and formation.

## Method Descriptions

#### gained_pet
{: #gained_pet }

void **gained_pet**(pet: Pet)

Adds a new pet to the container.

Parameters:
* pet: Pet - Pet to add

Implementation:
* Adds to active_pets array
* Adds to follow system if mobile

---

#### lost_pet
{: #lost_pet }

void **lost_pet**(pet: Pet)

Removes a pet from the container.

Parameters:
* pet: Pet - Pet to remove

Implementation:
* Removes from active_pets array
* Removes from follow system if mobile