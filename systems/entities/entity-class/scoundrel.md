---
layout: default
title: Scoundrel
parent: Companion
nav_order: 5
permalink: /systems/entities/entity-class/scoundrel
---

# Scoundrel

Inherits: [Companion](../companion/)

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| CompanionDatabase.Scoundrel_Specs | [specilization](#specilization) | - | Current scoundrel specialization |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [set_specilization](#set_specilization) | Sets specialization type |
| void | [setup_specilization](#setup_specilization) | Configures spec abilities and role |

## Method Descriptions 

#### set_specilization
{: #set_specilization }

void **set_specilization**(value: int)

Sets specialization based on value:
* 1: ROGUE
* 2: BARD
* 3: MARKSMAN

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