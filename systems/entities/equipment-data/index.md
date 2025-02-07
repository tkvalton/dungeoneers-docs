---
layout: default
title: Equipment Data
parent: Entity System
nav_order: 10
has_children: true
permalink: /systems/entities/equipment-data/
---

# EquipmentInventoryData

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description

EquipmentInventoryData manages the equipment inventory for an entity, including all equippable slots and their contents. It handles operations such as equipping, unequipping, and interacting with equipment items.

Key features:
- Manages various equipment slots (helm, chest, legs, etc.)
- Tracks equipment slot contents and state
- Links equipment data to entity owner

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Array[EquipmentSlotData] | [slots](#slots) | [] | Equipment slot array |

### General Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Entity | [inventory_owner](#inventory_owner) | null | Owner entity reference |

## Equipment Slot Types

Equipment slots are indexed as follows:
- 0: Head
- 1: Chest
- 2: Legs
- 3: Gloves
- 4: Belt
- 5: Boots
- 6: Jewelry
- 7: Main Hand
- 8: Off Hand

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Initializes inventory |
| void | [clear_all_equipment](#clear_all_equipment) | Clears all slots |

## Property Descriptions

#### slots
{: #slots }

Array[EquipmentSlotData] **slots** = `[]`
* Array[EquipmentSlotData] **get_slots**()
* void **set_slots**(value: Array[EquipmentSlotData])

Array containing equipment slot data. Fixed size of 9 slots.

---

#### inventory_owner
{: #inventory_owner }

Entity **inventory_owner**
* Entity **get_inventory_owner**()
* void **set_inventory_owner**(value: Entity)

Reference to entity that owns this equipment inventory.

## Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Initializes the equipment inventory:
* Sets inventory owner
* Ensures 9 slots exist
* Initializes missing slots
* Sets slot types and owner references

---

#### clear_all_equipment
{: #clear_all_equipment }

void **clear_all_equipment**()

Clears all equipment slots by calling clear() on each slot.