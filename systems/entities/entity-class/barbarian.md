---
layout: default
title: Barbarian
parent: Companion
nav_order: 2
permalink: /systems/entities/entity-class/barbarian
---

---
layout: default
title: Barbarian
parent: Companion
nav_order: 2
permalink: /systems/entities/entity-class/barbarian
---

# Barbarian 
Inherits: [Companion](../companion/)

## Properties

### Exported Properties
| Type | Property | Default | Description |
|------|----------|---------|-------------|
| CompanionDatabase.Barbarian_Specs | [specilization](#specilization) | - | Current barbarian specialization |

## Methods
| Return Type | Method | Description |
|------------|---------|-------------|
| void | [set_specilization](#set_specilization) | Sets specialization type |
| void | [setup_specilization](#setup_specilization) | Configures spec abilities and role |

## Property Descriptions

### Exported Properties

#### specilization
{: #specilization }

CompanionDatabase.Barbarian_Specs **specilization**
* CompanionDatabase.Barbarian_Specs **get_specilization**()
* void **set_specilization**(value: CompanionDatabase.Barbarian_Specs)

Defines the Barbarian's current specialization path:
- JUGGERNAUT: Focus on defense and crowd control, tank
- BERSERKER: High damage output and rage mechanics, damage dealer
- SHAMAN: Elemental and ancestral magic, damage dealer

## Method Descriptions

#### set_specilization
{: #set_specilization }

void **set_specilization**(value: int)

Sets specialization based on value:
* 1: JUGGERNAUT
* 2: BERSERKER
* 3: SHAMAN

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