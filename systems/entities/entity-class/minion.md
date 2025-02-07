---
layout: default
title: Minion
parent: Entity
nav_order: 2
permalink: /systems/entities/entity-class/minion
---

# Minion

Inherits: [Entity](../entity-class/)

## Description

Minion represents an enemy NPC in the game. It extends the base Entity class with features specific to AI-controlled adversaries, including patrol behavior and combat audio cues.

Key features:
- Implements patrol system for idle behavior
- Manages combat-related audio (pulled, hurt, death sounds)
- Integrates with the game's AI system for enemy behavior
- Handles enemy-specific death and despawn logic

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | [has_patrol](#has_patrol) | - | Whether minion follows patrol path |
| Marker3D | [spawn_point](#spawn_point) | - | Initial spawn location |
| PatrolPath | [patrol_path](#patrol_path) | - | Path for patrol behavior |

### Variables

| Type | Property | Description |
|------|----------|-------------|
| MinionPackContainer | [pack_container](#pack_container) | Container managing minion's group |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Called when minion enters scene tree |

## Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Extends parent _ready() initialization.