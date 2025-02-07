---
layout: default
title: Boss
parent: Entity
nav_order: 3
permalink: /systems/entities/entity-class/boss
---

# Boss

Inherits: [Entity](../entity-class/)

## Description

Boss represents a powerful enemy entity in the game, typically used for significant encounters or battles. It extends the base Entity class with features specific to boss fights, including specialized audio and integration with a boss fight management system.

Key features:
- Integrates with a BossFight management system
- Manages boss-specific audio cues (pulled, hurt, death sounds)
- Implements boss-specific death and despawn logic
- Designed for creating memorable and challenging enemy encounters

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| BossFight | [boss_fight](#boss_fight) | - | The fight timings |

### Variables

| Type | Property | Description |
|------|----------|-------------|
| BossContainer | [boss_container](#boss_container) | Container managing this boss |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Called when boss enters scene tree |

## Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Extends parent _ready() initialization.