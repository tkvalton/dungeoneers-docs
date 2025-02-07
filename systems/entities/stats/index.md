---
layout: default
title: Stats
parent: Entity System
nav_order: 3
permalink: /systems/entities/stats/
---

# EntityStatsContainer

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description

EntityStatsContainer manages all stats and attributes for an entity. It serves as the central system for handling stat calculations, modifications, and interactions such as taking damage or healing.

Key features:
- Manages base, major, and minor stats for entities
- Handles health and resource management
- Processes damage application, including avoidance and mitigation
- Manages healing and resource regeneration
- Provides methods for modifying and querying stats

## Enumerations

#### ResourceType
{: #resourcetype }
- START_EMPTY = 0 — Resource starts at 0
- START_FULL = 1 — Resource starts at maximum

## Constants

| Name | Value | Description |
|------|-------|-------------|
| STAT_TYPES | Dictionary | Categories of stats: BASE, MAJOR, MINOR, HIDDEN |

## Properties

### Base Stats

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| int | [max_health](#max_health) | 100 | Maximum health points |
| int | [health](#health) | max_health | Current health points |
| int | [health_regen](#health_regen) | 0 | Health regeneration per tick |
| ResourceType | [resource_type](#resource_type) | START_EMPTY | Resource fill state on init |
| Texture2D | [points_icon](#points_icon) | null | Icon for point-style resources |
| int | [resource_max](#resource_max) | 0 | Maximum resource points |
| int | [resource_regen](#resource_regen) | 0 | Resource regeneration per tick |
| float | [resource_regen_tick](#resource_regen_tick) | 1.0 | Resource regen tick rate |
| float | [movement_speed](#movement_speed) | 0.0 | Base movement speed |

### Major Stats

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| int | [strength](#strength) | 0 | Physical power stat |
| int | [agility](#agility) | 0 | Speed and finesse stat |
| int | [dexterity](#dexterity) | 0 | Accuracy and coordination stat |
| int | [endurance](#endurance) | 0 | Stamina and toughness stat |
| int | [intellect](#intellect) | 0 | Magical power stat |
| int | [wisdom](#wisdom) | 0 | Mental resistance stat |
| int | [charisma](#charisma) | 0 | Social influence stat |

### Minor Stats

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| int | [physical_attack](#physical_attack) | 0 | Physical damage bonus |
| float | [physical_critical_strike](#physical_critical_strike) | 0.0 | Physical crit chance % |
| float | [attack_speed](#attack_speed) | 0.0 | Attack speed multiplier |
| int | [magical_attack](#magical_attack) | 0 | Magical damage bonus |
| float | [magical_critical_strike](#magical_critical_strike) | 0.0 | Magical crit chance % |
| float | [cast_speed](#cast_speed) | 0.0 | Cast speed multiplier |
| float | [dodge](#dodge) | 0.0 | Dodge chance % |
| float | [parry](#parry) | 0.0 | Parry chance % |
| float | [shield_block](#shield_block) | 0.0 | Block damage reduction % |
| float | [shield_block_chance](#shield_block_chance) | 0.0 | Block chance % |
| float | [physical_defense](#physical_defense) | 0.0 | Physical damage reduction % |
| float | [magical_defense](#magical_defense) | 0.0 | Magical damage reduction % |

### Hidden Stats

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| int | [damage_absorbtion_shield_max](#damage_absorbtion_shield_max) | 0 | Maximum absorb shield |
| int | [damage_absorbtion_shield](#damage_absorbtion_shield) | 0 | Current absorb shield |
| int | [healing_absorbtion_shield_max](#healing_absorbtion_shield_max) | 0 | Maximum healing shield |
| int | [healing_absorbtion_shield](#healing_absorbtion_shield) | 0 | Current healing shield |
| float | [damage_taken_percentage_increase](#damage_taken_percentage_increase) | 0.0 | Damage taken increase % |
| float | [damage_taken_percentage_decrease](#damage_taken_percentage_decrease) | 0.0 | Damage taken decrease % |
| float | [damage_done_percentage_increase](#damage_done_percentage_increase) | 0.0 | Damage done increase % |
| float | [damage_done_percentage_decrease](#damage_done_percentage_decrease) | 0.0 | Damage done decrease % |
| float | [healing_taken_percentage_increase](#healing_taken_percentage_increase) | 0.0 | Healing taken increase % |
| float | [healing_taken_percentage_decrease](#healing_taken_percentage_decrease) | 0.0 | Healing taken decrease % |
| float | [healing_done_percentage_increase](#healing_done_percentage_increase) | 0.0 | Healing done increase % |
| float | [healing_done_percentage_decrease](#healing_done_percentage_decrease) | 0.0 | Healing done decrease % |

### General Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Entity | [entity](#entity) | null | Owner entity reference |
| Entity | [damage_reflect_target](#damage_reflect_target) | null | Damage reflection target |
| float | [damage_reflect_percentage](#damage_reflect_percentage) | 0.0 | Damage reflection amount % |
| Array[AbsorbEffect] | [absorb_effects](#absorb_effects) | [] | Active absorption effects |
| Dictionary | [stats](#stats) | {} | All stat data storage |

### Node References

| Type | Property | Description |
|------|----------|-------------|
| Timer | [health_tick](#health_tick) | Health regeneration timer |
| Timer | [resource_tick](#resource_tick) | Resource regeneration timer |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [setup_stats](#setup_stats) | Initializes all stats |
| void | [initialize_stats](#initialize_stats) | Creates stat dictionary |
| void | [set_initial_stats](#set_initial_stats) | Sets starting values |
| void | [setup_timers](#setup_timers) | Configures regen timers |
| void | [regen_health](#regen_health) | Handles health regeneration |
| void | [regen_resource](#regen_resource) | Handles resource regeneration |
| void | [modify_resource](#modify_resource) | Changes resource amount |
| void | [add_absorb_effect](#add_absorb_effect) | Adds absorption effect |
| void | [remove_absorb_effect](#remove_absorb_effect) | Removes absorption effect |
| void | [take_damage](#take_damage) | Processes incoming damage |
| int | [calculate_mitigated_damage](#calculate_mitigated_damage) | Applies defense reduction |
| bool | [try_avoid_damage](#try_avoid_damage) | Checks avoidance chances |
| int | [calculate_blocked_damage](#calculate_blocked_damage) | Calculates block amount |
| bool | [dodge_roll](#dodge_roll) | Performs dodge check |
| bool | [parry_roll](#parry_roll) | Performs parry check |
| bool | [block_roll](#block_roll) | Performs block check |
| int | [apply_absorb_effects](#apply_absorb_effects) | Processes absorption |
| int | [apply_damage_modifiers](#apply_damage_modifiers) | Applies damage mods |
| void | [reflect_damage](#reflect_damage) | Handles damage reflection |
| void | [apply_final_damage](#apply_final_damage) | Applies final damage |
| void | [take_heal](#take_heal) | Processes healing |
| int | [apply_healing_modifiers](#apply_healing_modifiers) | Applies healing mods |
| void | [dodged](#dodged) | Handles dodge event |
| void | [parried](#parried) | Handles parry event |
| void | [blocked](#blocked) | Handles block event |
| Variant | [get_stat](#get_stat) | Gets stat value |
| Variant | [get_stat_component](#get_stat_component) | Gets stat component |
| void | [set_stat](#set_stat) | Sets stat value |
| void | [update_stat_total](#update_stat_total) | Updates total value |
| float | [get_major_stat_modifier](#get_major_stat_modifier) | Gets stat modifier |
| void | [modify_stat_base](#modify_stat_base) | Modifies base value |
| void | [modify_stat_bonus](#modify_stat_bonus) | Modifies bonus value |
| void | [modify_stat_multiplier](#modify_stat_multiplier) | Modifies multiplier |

# Property Descriptions

## Base Stats

#### max_health
{: #max_health }

int **max_health** = `100`
* int **get_max_health**()
* void **set_max_health**(value: int)

Maximum health points the entity can have. Acts as a cap for healing and regeneration.

---

#### health
{: #health }

int **health** = `max_health`
* int **get_health**()
* void **set_health**(value: int)

Current health points. Entity dies when this reaches 0.

---

#### health_regen
{: #health_regen }

int **health_regen** = `0`
* int **get_health_regen**()
* void **set_health_regen**(value: int)

Amount of health regenerated per tick. Out of combat regeneration is 10x for minions and bosses.

---

#### resource_type
{: #resource_type }

ResourceType **resource_type** = `START_EMPTY`
* ResourceType **get_resource_type**()
* void **set_resource_type**(value: ResourceType)

Determines if resource starts empty or full on initialization.

---

#### points_icon
{: #points_icon }

Texture2D **points_icon**
* Texture2D **get_points_icon**()
* void **set_points_icon**(value: Texture2D)

Icon used for point-style resources instead of bars.

---

#### resource_max
{: #resource_max }

int **resource_max** = `0`
* int **get_resource_max**()
* void **set_resource_max**(value: int)

Maximum resource points available for abilities.

---

#### resource_regen
{: #resource_regen }

int **resource_regen** = `0`
* int **get_resource_regen**()
* void **set_resource_regen**(value: int)

Resource points regenerated per tick.

---

#### resource_regen_tick
{: #resource_regen_tick }

float **resource_regen_tick** = `1.0`
* float **get_resource_regen_tick**()
* void **set_resource_regen_tick**(value: float)

Time in seconds between resource regeneration ticks.

---

#### movement_speed
{: #movement_speed }

float **movement_speed** = `0.0`
* float **get_movement_speed**()
* void **set_movement_speed**(value: float)

Base movement speed of the entity.

## Major Stats

#### strength
{: #strength }

int **strength** = `0`
* int **get_strength**()
* void **set_strength**(value: int)

Physical power stat affecting physical damage and carrying capacity.

---

#### agility
{: #agility }

int **agility** = `0`
* int **get_agility**()
* void **set_agility**(value: int)

Speed and finesse stat affecting attack speed and dodge.

---

#### dexterity
{: #dexterity }

int **dexterity** = `0`
* int **get_dexterity**()
* void **set_dexterity**(value: int)

Accuracy and coordination stat affecting physical critical strikes and parry.

---

#### endurance
{: #endurance }

int **endurance** = `0`
* int **get_endurance**()
* void **set_endurance**(value: int)

Stamina and toughness stat affecting health and physical defense.

---

#### intellect
{: #intellect }

int **intellect** = `0`
* int **get_intellect**()
* void **set_intellect**(value: int)

Magical power stat affecting spell damage and magical critical strikes.

---

#### wisdom
{: #wisdom }

int **wisdom** = `0`
* int **get_wisdom**()
* void **set_wisdom**(value: int)

Mental resistance stat affecting magical defense and resource regeneration.

---

#### charisma
{: #charisma }

int **charisma** = `0`
* int **get_charisma**()
* void **set_charisma**(value: int)

Social influence stat affecting interaction outcomes and certain abilities.

## Minor Stats

#### physical_attack
{: #physical_attack }

int **physical_attack** = `0`
* int **get_physical_attack**()
* void **set_physical_attack**(value: int)

Additional physical damage bonus.

---

#### physical_critical_strike
{: #physical_critical_strike }

float **physical_critical_strike** = `0.0`
* float **get_physical_critical_strike**()
* void **set_physical_critical_strike**(value: float)

Chance to critically hit with physical attacks, as percentage.

---

#### attack_speed
{: #attack_speed }

float **attack_speed** = `0.0`
* float **get_attack_speed**()
* void **set_attack_speed**(value: float)

Speed multiplier for physical attacks.

---

#### magical_attack
{: #magical_attack }

int **magical_attack** = `0`
* int **get_magical_attack**()
* void **set_magical_attack**(value: int)

Additional magical damage bonus.

---

#### magical_critical_strike
{: #magical_critical_strike }

float **magical_critical_strike** = `0.0`
* float **get_magical_critical_strike**()
* void **set_magical_critical_strike**(value: float)

Chance to critically hit with magical attacks, as percentage.

---

#### cast_speed
{: #cast_speed }

float **cast_speed** = `0.0`
* float **get_cast_speed**()
* void **set_cast_speed**(value: float)

Speed multiplier for spell casting.

---

#### dodge
{: #dodge }

float **dodge** = `0.0`
* float **get_dodge**()
* void **set_dodge**(value: float)

Chance to completely avoid incoming attacks, as percentage.

---

#### parry
{: #parry }

float **parry** = `0.0`
* float **get_parry**()
* void **set_parry**(value: float)

Chance to parry incoming melee attacks, as percentage.

---

#### shield_block
{: #shield_block }

float **shield_block** = `0.0`
* float **get_shield_block**()
* void **set_shield_block**(value: float)

Percentage of damage reduced when block is successful.

---

#### shield_block_chance
{: #shield_block_chance }

float **shield_block_chance** = `0.0`
* float **get_shield_block_chance**()
* void **set_shield_block_chance**(value: float)

Chance to block incoming physical attacks, as percentage.

---

#### physical_defense
{: #physical_defense }

float **physical_defense** = `0.0`
* float **get_physical_defense**()
* void **set_physical_defense**(value: float)

Percentage reduction to incoming physical damage.

---

#### magical_defense
{: #magical_defense }

float **magical_defense** = `0.0`
* float **get_magical_defense**()
* void **set_magical_defense**(value: float)

Percentage reduction to incoming magical damage.

## Hidden Stats

#### damage_absorbtion_shield_max
{: #damage_absorbtion_shield_max }

int **damage_absorbtion_shield_max** = `0`
* int **get_damage_absorbtion_shield_max**()
* void **set_damage_absorbtion_shield_max**(value: int)

Maximum amount of damage that can be absorbed by shield effects.

---

#### damage_absorbtion_shield
{: #damage_absorbtion_shield }

int **damage_absorbtion_shield** = `0`
* int **get_damage_absorbtion_shield**()
* void **set_damage_absorbtion_shield**(value: int)

Current amount of damage absorption remaining.

---

#### healing_absorbtion_shield_max
{: #healing_absorbtion_shield_max }

int **healing_absorbtion_shield_max** = `0`
* int **get_healing_absorbtion_shield_max**()
* void **set_healing_absorbtion_shield_max**(value: int)

Maximum amount of healing that can be absorbed by shield effects.

---

#### healing_absorbtion_shield
{: #healing_absorbtion_shield }

int **healing_absorbtion_shield** = `0`
* int **get_healing_absorbtion_shield**()
* void **set_healing_absorbtion_shield**(value: int)

Current amount of healing absorption remaining.

---

#### damage_taken_percentage_increase
{: #damage_taken_percentage_increase }

float **damage_taken_percentage_increase** = `0.0`
* float **get_damage_taken_percentage_increase**()
* void **set_damage_taken_percentage_increase**(value: float)

Percentage increase to all damage taken.

---

#### damage_taken_percentage_decrease
{: #damage_taken_percentage_decrease }

float **damage_taken_percentage_decrease** = `0.0`
* float **get_damage_taken_percentage_decrease**()
* void **set_damage_taken_percentage_decrease**(value: float)

Percentage reduction to all damage taken.

---

#### damage_done_percentage_increase
{: #damage_done_percentage_increase }

float **damage_done_percentage_increase** = `0.0`
* float **get_damage_done_percentage_increase**()
* void **set_damage_done_percentage_increase**(value: float)

Percentage increase to all damage dealt.

---

#### damage_done_percentage_decrease
{: #damage_done_percentage_decrease }

float **damage_done_percentage_decrease** = `0.0`
* float **get_damage_done_percentage_decrease**()
* void **set_damage_done_percentage_decrease**(value: float)

Percentage reduction to all damage dealt.

---

#### healing_taken_percentage_increase
{: #healing_taken_percentage_increase }

float **healing_taken_percentage_increase** = `0.0`
* float **get_healing_taken_percentage_increase**()
* void **set_healing_taken_percentage_increase**(value: float)

Percentage increase to healing received.

---

#### healing_taken_percentage_decrease
{: #healing_taken_percentage_decrease }

float **healing_taken_percentage_decrease** = `0.0`
* float **get_healing_taken_percentage_decrease**()
* void **set_healing_taken_percentage_decrease**(value: float)

Percentage reduction to healing received.

---

#### healing_done_percentage_increase
{: #healing_done_percentage_increase }

float **healing_done_percentage_increase** = `0.0`
* float **get_healing_done_percentage_increase**()
* void **set_healing_done_percentage_increase**(value: float)

Percentage increase to healing dealt.

---

#### healing_done_percentage_decrease
{: #healing_done_percentage_decrease }

float **healing_done_percentage_decrease** = `0.0`
* float **get_healing_done_percentage_decrease**()
* void **set_healing_done_percentage_decrease**(value: float)

Percentage reduction to healing dealt.

## General Properties

#### entity
{: #entity }

Entity **entity**
* Entity **get_entity**()
* void **set_entity**(value: Entity)

Reference to the entity these stats belong to.

---

#### damage_reflect_target
{: #damage_reflect_target }

Entity **damage_reflect_target** = `null`
* Entity **get_damage_reflect_target**()
* void **set_damage_reflect_target**(value: Entity)

Entity that receives reflected damage.

---

#### damage_reflect_percentage
{: #damage_reflect_percentage }

float **damage_reflect_percentage** = `0.0`
* float **get_damage_reflect_percentage**()
* void **set_damage_reflect_percentage**(value: float)

Percentage of damage reflected to target.

---

#### absorb_effects
{: #absorb_effects }

Array[AbsorbEffect] **absorb_effects** = `[]`
* Array[AbsorbEffect] **get_absorb_effects**()
* void **set_absorb_effects**(value: Array[AbsorbEffect])

Currently active absorption effects.

---

#### stats
{: #stats }

Dictionary **stats** = `{}`
* Dictionary **get_stats**()
* void **set_stats**(value: Dictionary)

Storage for all stat data including base, bonus, and multiplier values.

## Node References

#### health_tick
{: #health_tick }

Timer **health_tick**
* Timer **get_health_tick**()
* void **set_health_tick**(value: Timer)

Timer controlling health regeneration ticks.

---

#### resource_tick
{: #resource_tick }

Timer **resource_tick**
* Timer **get_resource_tick**()
* void **set_resource_tick**(value: Timer)

Timer controlling resource regeneration ticks.

# Method Descriptions

#### setup_stats
{: #setup_stats }

void **setup_stats**()

Sets up initial stats system by:
* Initializing stat dictionary
* Setting initial values
* Setting up regeneration timers

---

#### initialize_stats
{: #initialize_stats }

void **initialize_stats**()

Creates stat dictionary with all categories:
* Base Stats (health, resource, movement)
* Major Stats (strength, agility, etc.)
* Minor Stats (attack, defense, etc.)
* Hidden Stats (modifiers, absorptions)

---

#### set_initial_stats
{: #set_initial_stats }

void **set_initial_stats**()

Sets starting values for all stats:
* Basic stats from exported variables
* Resource based on resource_type
* Major stats from properties
* Minor stats from properties
* Hidden stats from properties

---

#### setup_timers
{: #setup_timers }

void **setup_timers**()

Configures regeneration timers:
* Health tick every 2 seconds
* Resource tick based on resource_regen_tick
* Connects timer signals

---

#### regen_health
{: #regen_health }

void **regen_health**()

Handles health regeneration:
* Checks for dead/combat state
* Applies regen amount
* 10x regen for non-combat minions/bosses
* Emits health change signal

---

#### regen_resource
{: #regen_resource }

void **regen_resource**()

Handles resource regeneration:
* Checks for dead state
* Applies regen amount
* Emits resource change signal

---

#### modify_resource
{: #modify_resource }

void **modify_resource**(resource_cost: int)

Modifies current resource amount:
* Clamps between 0 and maximum
* Emits resource change signal

Parameters:
* resource_cost: int - Amount to modify (positive or negative)

---

#### add_absorb_effect
{: #add_absorb_effect }

void **add_absorb_effect**(effect: AbsorbEffect)

Adds absorption effect to active effects list.

Parameters:
* effect: AbsorbEffect - Effect to add

---

#### remove_absorb_effect
{: #remove_absorb_effect }

void **remove_absorb_effect**(effect: AbsorbEffect)

Removes absorption effect from active effects list.

Parameters:
* effect: AbsorbEffect - Effect to remove

---

#### take_damage
{: #take_damage }

void **take_damage**(damage: int, damage_type: int, damage_source: Entity, ability_name: String, is_tick_damage: bool, was_crit: bool, can_be_avoided: bool)

Processes incoming damage with full mitigation pipeline:
* Applies defense mitigation
* Checks avoidance
* Applies damage modifiers
* Processes blocks and absorbs
* Handles damage reflection
* Applies final damage
* Handles death state
* Updates combat log

Parameters:
* damage: int - Raw damage amount
* damage_type: int - Type (0: Physical, 1: Magical, 2: True)
* damage_source: Entity - Damage source entity
* ability_name: String - Name of damage source ability
* is_tick_damage: bool - If damage is from DOT effect
* was_crit: bool - If damage was critical hit
* can_be_avoided: bool - If damage can be dodged/parried

---

#### calculate_mitigated_damage
{: #calculate_mitigated_damage }

int **calculate_mitigated_damage**(damage: int, defense_stat: String)

Calculates damage after defense reduction.

Parameters:
* damage: int - Initial damage
* defense_stat: String - Defense stat to use

Returns: Final damage after mitigation

---

#### try_avoid_damage
{: #try_avoid_damage }

bool **try_avoid_damage**(damage: int, damage_source: Entity, ability_name: String)

Attempts damage avoidance through dodge or parry.

Parameters:
* damage: int - Damage amount
* damage_source: Entity - Damage source
* ability_name: String - Ability name

Returns: True if damage was avoided

---

#### calculate_blocked_damage
{: #calculate_blocked_damage }

int **calculate_blocked_damage**(physical_damage: int)

Calculates damage reduction from shield block.

Parameters:
* physical_damage: int - Damage amount

Returns: Amount of damage blocked

---

#### dodge_roll
{: #dodge_roll }

bool **dodge_roll**()

Performs dodge chance check.

Returns: True if dodge successful

---

#### parry_roll
{: #parry_roll }

bool **parry_roll**()

Performs parry chance check.

Returns: True if parry successful

---

#### block_roll
{: #block_roll }

bool **block_roll**()

Performs block chance check.

Returns: True if block successful

---

#### apply_absorb_effects
{: #apply_absorb_effects }

int **apply_absorb_effects**(damage: int)

Applies active absorption effects to damage.

Parameters:
* damage: int - Damage amount

Returns: Amount of damage absorbed

---

#### apply_damage_modifiers
{: #apply_damage_modifiers }

int **apply_damage_modifiers**(damage: int)

Applies damage increase/decrease modifiers.

Parameters:
* damage: int - Initial damage

Returns: Modified damage amount

---

#### reflect_damage
{: #reflect_damage }

void **reflect_damage**(damage: int, source: Entity, ability: String, is_tick: bool, was_crit: bool, can_avoid: bool)

Reflects portion of damage to target.

Parameters:
* damage: int - Damage amount
* source: Entity - Original damage source
* ability: String - Ability name
* is_tick: bool - If damage is DOT
* was_crit: bool - If damage was critical
* can_avoid: bool - If damage can be avoided

---

#### apply_final_damage
{: #apply_final_damage }

void **apply_final_damage**(damage: int, source: Entity, ability: String, blocked_amount: int, absorbed_amount: int, is_tick: bool, was_crit: bool)

Applies final processed damage:
* Updates health
* Emits signals
* Updates combat log
* Handles death state

Parameters:
* damage: int - Final damage amount
* source: Entity - Damage source
* ability: String - Ability name
* blocked_amount: int - Damage blocked
* absorbed_amount: int - Damage absorbed
* is_tick: bool - If damage is DOT
* was_crit: bool - If damage was critical

---

#### take_heal
{: #take_heal }

void **take_heal**(heal_amount: int, heal_source: Entity, ability_name: String, critical_hit: bool)

Processes incoming healing:
* Applies healing modifiers
* Handles overhealing
* Updates combat log
* Emits signals

Parameters:
* heal_amount: int - Amount to heal
* heal_source: Entity - Healing source
* ability_name: String - Ability name
* critical_hit: bool - If heal was critical

---

#### apply_healing_modifiers
{: #apply_healing_modifiers }

int **apply_healing_modifiers**(heal_amount: int)

Applies healing increase/decrease modifiers.

Parameters:
* heal_amount: int - Initial healing amount

Returns: Modified healing amount

---

#### dodged
{: #dodged }

void **dodged**(total_mitigated_damage: int)

Handles dodge event:
* Plays dodge animation
* Emits dodge signal

Parameters:
* total_mitigated_damage: int - Damage avoided

---

#### parried
{: #parried }

void **parried**(total_mitigated_damage: int)

Handles parry event:
* Plays parry animation
* Emits parry signal

Parameters:
* total_mitigated_damage: int - Damage avoided

---

#### blocked
{: #blocked }

void **blocked**(total_mitigated_damage: int)

Handles block event:
* Plays block animation
* Emits block signal

Parameters:
* total_mitigated_damage: int - Damage blocked

---

#### get_stat
{: #get_stat }

Variant **get_stat**(stat_name: String, component: String = "total")

Gets value of specified stat component.

Parameters:
* stat_name: String - Name of stat
* component: String - Component to get (default: "total")

Returns: Stat value

---

#### get_stat_component
{: #get_stat_component }

Variant **get_stat_component**(stat_name: String, component: String)

Helper function to get specific stat component.

Parameters:
* stat_name: String - Name of stat
* component: String - Component to get

Returns: Component value

---

#### set_stat
{: #set_stat }

void **set_stat**(stat_name: String, value: Variant)

Sets base value of specified stat.

Parameters:
* stat_name: String - Name of stat
* value: Variant - New value

---

#### update_stat_total
{: #update_stat_total }

void **update_stat_total**(stat_name: String, stat_type: String)

Updates total value of stat based on components.

Parameters:
* stat_name: String - Name of stat
* stat_type: String - Type category of stat

---

#### get_major_stat_modifier
{: #get_major_stat_modifier }

float **get_major_stat_modifier**(stat_name: String, stat_type: String)

Gets modifier value from associated major stat.

Parameters:
* stat_name: String - Name of stat
* stat_type: String - Type category of stat

Returns: Modifier value

---

#### modify_stat_base
{: #modify_stat_base }

void **modify_stat_base**(stat_to_modify: String, amount_to_modify: int)

Modifies base value of stat.

Parameters:
* stat_to_modify: String - Name of stat
* amount_to_modify: int - Modification amount

---

#### modify_stat_bonus
{: #modify_stat_bonus }

void **modify_stat_bonus**(stat_to_modify: String, amount_to_modify: int)

Modifies bonus value of stat.

Parameters:
* stat_to_modify: String - Name of stat
* amount_to_modify: int - Modification amount

---

#### modify_stat_multiplier
{: #modify_stat_multiplier }

void **modify_stat_multiplier**(stat_to_modify: String, amount_to_modify: float)

Modifies multiplier value of stat.

Parameters:
* stat_to_modify: String - Name of stat
* amount_to_modify: float - Modification amount