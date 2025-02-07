---
layout: default
title: Acolyte
parent: Companion
nav_order: 1
permalink: /systems/entities/entity-class/acolyte
---

# Acolyte

Inherits: [Companion](../companion/)

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| CompanionDatabase.Acolyte_Specs | [specilization](#specilization) | - | Current acolyte specialization |

### Node References

| Type | Property | Description |
|------|----------|-------------|
| MeshInstance3D | [scythe](#scythe) | %Scythe reference |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Called when acolyte enters scene tree |
| void | [set_specilization](#set_specilization) | Sets specialization type |
| void | [setup_specilization](#setup_specilization) | Configures spec abilities and role |
| void | [connect_necromancer_signals](#connect_necromancer_signals) | Connects ability signals |
| void | [_on_ability_use](#_on_ability_use) | Handles ability usage |

## Property Descriptions

### Exported Properties

#### specilization
{: #specilization }

CompanionDatabase.Acolyte_Specs **specilization**
* CompanionDatabase.Acolyte_Specs **get_specilization**()
* void **set_specilization**(value: CompanionDatabase.Acolyte_Specs)

Defines the Acolyte's current specialization path:
- NECROMANCER: Focus on death magic and minion control
- BLOODWEAVER: Manipulation of blood and life force
- WARLOCK: Dark magic and curses

### Node References

#### scythe
{: #scythe }

MeshInstance3D **scythe**
* MeshInstance3D **get_scythe**()
* void **set_scythe**(value: MeshInstance3D)

Reference to the Acolyte's scythe weapon mesh, used for attack animations.

## Method Descriptions 

#### set_specilization
{: #set_specilization }

void **set_specilization**(value: int)

Sets specialization based on value:
* 1: NECROMANCER
* 2: BLOODWEAVER  
* 3: WARLOCK

---

#### setup_specilization
{: #setup_specilization }

void **setup_specilization**()

Sets up specialization:
* Sets role from CompanionDatabase.CLASS_SPEC_ROLES
* Configures resource type and color
* Loads and sets up basic attacks
* Loads and sets up active abilities  
* Loads and sets up passive abilities
* Configures combat AI script

---

#### connect_necromancer_signals
{: #connect_necromancer_signals }

void **connect_necromancer_signals**()

Connects ability use attempt signal to _on_ability_use.

---

#### _on_ability_use
{: #_on_ability_use }

void **_on_ability_use**(_user: Entity, ability: Ability)

Handles ability usage:
* ID 38: Plays scythe attack animation