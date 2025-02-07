---
layout: default
title: Pet
parent: Entity
nav_order: 4
permalink: /systems/entities/entity-class/pet
---

# Pet

Inherits: [Entity](../entity-class/)

## Properties

### Variables

| Type | Property | Description |
|------|----------|-------------|
| Entity | [summoner](#summoner) | The owner of the pet |
| Effect | [effect](#effect) | The effect that summoned the pet |
| bool | [follow_stance](#follow_stance) | If the pet follows its owner |
| Timer | [summon_timer](#summon_timer) | Init timer for VFX/animations |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Sets up pet on scene entry |
| void | [summon_timer_timeout](#summon_timer_timeout) | Handles summon animation completion |
| void | [_on_entity_died](#_on_entity_died) | Handles pet death |
| void | [_on_summoner_died](#_on_summoner_died) | Handles owner death |
| void | [summon_duration_timer](#summon_duration_timer) | Sets up pet duration |
| void | [summon_finished](#summon_finished) | Cleans up on summon end |
| void | [die](#die) | Handles pet death and cleanup |

## Method Descriptions

#### _ready
{: #_ready }

void **_ready**()

Initial setup:
* Starts invisible
* Sets up summon timer
* Connects to summoner's target
* Inherits target from summoner

---

#### summon_timer_timeout
{: #summon_timer_timeout }

void **summon_timer_timeout**()

When summon completes:
* Plays jump animation
* Makes pet visible
* Enables following
* Enters combat if summoner in combat

---

#### _on_entity_died
{: #_on_entity_died }

void **_on_entity_died**()

On pet death:
* Exits combat
* Removes effects
* Updates AI state

---

#### _on_summoner_died
{: #_on_summoner_died }

void **_on_summoner_died**()

When summoner dies:
* Exits combat
* Ends summon

---

#### summon_duration_timer
{: #summon_duration_timer }

void **summon_duration_timer**(duration: float)

Sets up duration timer if duration > 0.

Parameters:
* duration: float - How long pet exists

---

#### summon_finished
{: #summon_finished }

void **summon_finished**()

End of summon cleanup:
* Fades out
* Removes from pet container
* Frees instance

---

#### die
{: #die }

void **die**()

Death handling:
* Removes from pet container
* Calls parent die()
* Ends summon