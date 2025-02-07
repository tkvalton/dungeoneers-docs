---
layout: default
title: Entity System
nav_order: 2
has_children: true
permalink: /systems/entities/
---

# Entity System

## Overview
The Entity System is the core framework that manages all player and npc objects within Dungeoneers. It provides a robust foundation for creating and managing various types of entities including companions, minions, bosses, and NPCs. Each entity is composed of multiple components that handle different aspects of functionality, from visual representation to combat mechanics.

## Components

### Core Components

#### [Entity Base Class](./entity-class/)
The foundational class for all game objects, providing core functionality for:
- Movement and physics interactions
- Combat mechanics including damage and healing
- Effects and status condition management
- Integration with AI and targeting systems
- Support for various entity types (Companion, Minion, Boss, NPC)

#### [Rig Controller](./rig-controller/)
Manages the visual representation and animations:
- Handles mesh instances and their materials
- Controls outline effects for selection and targeting
- Manages attachment points for weapons and VFX
- Controls casting VFX and transparency effects
- Integrates with the game's selection and targeting systems

#### [Stats Container](./stats-container/)
Handles all entity attributes and statistics:
- Manages base, major, and minor stats
- Controls health and resource management
- Processes damage application and mitigation
- Handles healing and regeneration
- Provides methods for stat modification

### Combat & Abilities

#### [Ability Container](./ability-container/)
Manages all entity abilities and their usage:
- Controls ability collections for each entity
- Handles ability use attempts and validation
- Manages global cooldown (GCD)
- Creates ability scenes using AbilityData
- Provides signals for ability use attempts

#### [Effects Container](./effects-container/)
Handles status effects and buffs:
- Maintains active effects list
- Manages effect application and removal
- Provides effect querying and management
- Tracks effect durations and stacks

### AI & Behavior

#### [AI System](./ai-system/)
Controls entity behavior and decision-making:
- Manages state machines for movement and actions
- Handles combat positioning and targeting
- Controls ability usage and decision-making
- Manages different AI behaviors per entity type

#### [Aggro Table](./aggro-table/)
Manages combat targeting and threat:
- Maintains aggression values for each target
- Handles target selection and priority
- Manages combat state transitions
- Responds to combat events

### Pet Systems

#### [Pet Container](./pet-container/)
Manages pet entities and their relationships:
- Maintains active pets list
- Integrates with follower system
- Handles pet addition and removal

#### [Pet Follow System](./pet-follower/)
Controls pet movement and formations:
- Manages dynamic follower formations
- Updates positions based on leader movement
- Handles formation parameters
- Ensures proper following behavior

### Equipment & Interface

#### [Equipment Data](./equipment-data/)
Manages entity equipment and inventory:
- Handles equipment slots (helm, chest, legs, etc.)
- Manages equipment stats and effects
- Controls equipment visualization

#### [Nameplate](./nameplate/)
Manages entity UI elements:
- Displays health and resource bars
- Shows buffs and debuffs
- Manages cast bar for abilities
- Updates based on entity state

## Implementation Details

Each component is designed to be modular and self-contained while maintaining efficient communication through a robust signal system. Components can be enabled or disabled based on entity type requirements, allowing for flexible entity configurations.

### Entity Types
- **Companions**: Player-controlled allies with full ability sets and equipment
- **Minions**: Basic enemy units with simplified AI and combat behavior
- **Bosses**: Complex enemies with unique abilities and combat patterns
- **NPCs**: Non-combat entities for world interaction

### Hierarchy
The Entity System follows a clear hierarchical structure where the base Entity class provides core functionality, and specific entity types extend this with additional features through component composition.

## Examples
[Detailed code examples and implementation guides will be added in subsequent documentation]