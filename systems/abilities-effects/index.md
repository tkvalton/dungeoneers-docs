---
layout: default
title: Abilities & Effects
nav_order: 3
has_children: true
permalink: /systems/abilities-effects/
---

# Abilities & Effects System

## Overview
The Abilities & Effects System handles all abilites and effects.

Abilites are a node tree made up of a parent [Ability](./ability) along with with a [Target Strategy](./target-strategy), [Use Strategy](./use-strategy) and a collection of [Effect](./effect) nodes. [Ability](./ability) nodes hold a resource [AbilityData](./ability/ability-data) which will contain all exported data for the ability including it's chosen [Target Strategy](./target-strategy), [Use Strategy](./use-strategy) and an array of [EffectData](./effect/effect-data).

The [Ability](./ability) when called to setup will instaniate it's required children of set class by the [AbilityData](./ability/ability-data).


## Components

### Ability Classes

#### [Ability](./ability)
The foundational class for all abilities.

#### [Target Strategy](./target-strategy)
The foundational class for all abilities target strategies.
Contains all the logic required for the targeting of an active ability.

#### [Use Strategy](./use-strategy)
The foundational class for all abilities use strategies.
Contains all the logic required for the use of an active ability.

### Effects Classes

#### [Effect](./effect)
The foundational class for all effects.

#### [Time Strategy](./time-strategy)
The foundational class for all effects time strategies.
Contains all the logic required for the process of an effect.
