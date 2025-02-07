---
layout: default
title: Nameplate
parent: Entity System
nav_order: 11
has_children: true
permalink: /systems/entities/nameplate/
---

---
layout: default
title: Nameplate
parent: UI System
nav_order: 1
permalink: /systems/ui/nameplate/
---

# Nameplate

Inherits: [MarginContainer](https://docs.godotengine.org/en/stable/classes/class_margincontainer.html)

## Description

Nameplate manages the display of entity nameplates in the game, showing health, resource, cast bars, and status effects (buffs/debuffs).

Key features:
- Displays entity name, health, and resource bars
- Shows active buffs and debuffs
- Manages cast bar for abilities
- Updates dynamically based on entity state
- Supports different styles for normal entities and bosses
- Configurable through game settings

## Constants

| Name | Type | Description |
|------|------|-------------|
| _3D_HEALTH_BARS_BACKGROUND_PLAIN | StyleBoxFlat | Default nameplate background |
| _3D_HEALTH_BARS_BACKGROUND_TARGETED | StyleBoxFlat | Background when entity is targeted |
| _3D_HEALTH_BARS_BACKGROUND_MOUSE_HOVER | StyleBoxFlat | Background on mouse hover |
| _3D_HEALTH_BARS_FILL_GREEN | StyleBoxFlat | Green health bar fill style |
| _3D_HEALTH_BARS_FILL_RED | StyleBoxFlat | Red health bar fill style |

## Properties

### Exported Properties
| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | boss | false | Flag if nameplate belongs to a boss entity |

### State Properties
| Type | Property | Default | Description |
|------|----------|---------|-------------|
| Entity | nameplate_owner | null | Entity that owns the nameplate |
| bool | casting | false | Whether entity is casting |
| Array[Aura] | active_auras | [] | Currently active auras |
| Array[Aura] | buff_slots | [] | Available buff slots |
| Array[Aura] | debuff_slots | [] | Available debuff slots |
| bool | cast_bar_enabled | false | Whether cast bar is enabled |

### UI Elements
| Type | Property | Description |
|------|----------|-------------|
| Label | name_label | Entity name display |
| ProgressBar | health_bar | Health bar display |
| Label | health | Health text display |
| ProgressBar | resource_bar | Resource bar display |
| Label | resource | Resource text display |
| ProgressBar | cast_bar | Cast bar display |
| Label | cast_bar_ability_name | Casting ability name |
| Label | cast_bar_timer_text | Cast timer display |
| Timer | cast_bar_timer | Cast duration timer |
| GridContainer | buff_grid | Grid for buff icons |
| GridContainer | debuff_grid | Grid for debuff icons |

# Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_ready](#_ready) | Sets up aura slot arrays |
| void | [nameplate_setup](#nameplate_setup) | Initializes nameplate for entity |
| void | [connect_signals](#connect_signals) | Connects entity signals |
| void | [_physics_process](#_physics_process) | Updates cast bar |
| void | [update_health](#update_health) | Updates health display |
| void | [update_resource](#update_resource) | Updates resource display |
| void | [add_exisiting_auras](#add_exisiting_auras) | Adds existing auras |
| void | [create_aura](#create_aura) | Creates new aura |
| void | [remove_aura](#remove_aura) | Removes specified aura |
| void | [update_current_aura](#update_current_aura) | Updates existing aura |
| void | [cast_bar_active](#cast_bar_active) | Activates cast bar |
| void | [cast_bar_stop](#cast_bar_stop) | Stops cast bar |
| void | [start_timer](#start_timer) | Starts cast timer |
| void | [on_timer_timeout](#on_timer_timeout) | Handles timer completion |
| void | [set_nameplate_border_colour](#set_nameplate_border_colour) | Updates border style |
| void | [set_health_bar_colour](#set_health_bar_colour) | Updates health bar color |
| void | [set_resource_bar_colour](#set_resource_bar_colour) | Updates resource bar color |
| void | [_on_nameplate_update](#_on_nameplate_update) | Updates settings |
| void | [_on_interrupt](#_on_interrupt) | Handles interruption |

## Property Descriptions

## Constants

#### _3D_HEALTH_BARS_BACKGROUND_PLAIN
{: #_3d_health_bars_background_plain }

StyleBoxFlat **_3D_HEALTH_BARS_BACKGROUND_PLAIN**

Default background stylebox for nameplates.

---

#### _3D_HEALTH_BARS_BACKGROUND_TARGETED
{: #_3d_health_bars_background_targeted }

StyleBoxFlat **_3D_HEALTH_BARS_BACKGROUND_TARGETED**

Background stylebox used when entity is current target.

---

#### _3D_HEALTH_BARS_BACKGROUND_MOUSE_HOVER
{: #_3d_health_bars_background_mouse_hover }

StyleBoxFlat **_3D_HEALTH_BARS_BACKGROUND_MOUSE_HOVER**

Background stylebox used on mouse hover.

---

#### _3D_HEALTH_BARS_FILL_GREEN
{: #_3d_health_bars_fill_green }

StyleBoxFlat **_3D_HEALTH_BARS_FILL_GREEN**

Green fill stylebox for health bars.

---

#### _3D_HEALTH_BARS_FILL_RED
{: #_3d_health_bars_fill_red }

StyleBoxFlat **_3D_HEALTH_BARS_FILL_RED**

Red fill stylebox for health bars.

## Exported Properties

#### boss
{: #boss }

bool **boss** = `false`
* bool **is_boss**()
* void **set_boss**(value: bool)

Defines whether nameplate belongs to a boss entity, affecting UI layout and aura slots.

## State Properties

#### nameplate_owner
{: #nameplate_owner }

Entity **nameplate_owner**
* Entity **get_nameplate_owner**()
* void **set_nameplate_owner**(value: Entity)

Reference to entity this nameplate represents.

---

#### casting
{: #casting }

bool **casting** = `false`
* bool **is_casting**()
* void **set_casting**(value: bool)

Current casting state of entity.

---

#### active_auras
{: #active_auras }

Array[Aura] **active_auras**
* Array[Aura] **get_active_auras**()
* void **set_active_auras**(value: Array[Aura])

Currently active auras displayed on nameplate.

---

#### buff_slots
{: #buff_slots }

Array[Aura] **buff_slots**
* Array[Aura] **get_buff_slots**()
* void **set_buff_slots**(value: Array[Aura])

Available slots for beneficial effects. Size varies based on entity type.

---

#### debuff_slots
{: #debuff_slots }

Array[Aura] **debuff_slots**
* Array[Aura] **get_debuff_slots**()
* void **set_debuff_slots**(value: Array[Aura])

Available slots for harmful effects. Size varies based on entity type.

---

#### cast_bar_enabled
{: #cast_bar_enabled }

bool **cast_bar_enabled**
* bool **is_cast_bar_enabled**()
* void **set_cast_bar_enabled**(value: bool)

Controls cast bar visibility based on settings.

## UI Elements

#### name_label
{: #name_label }

Label **name_label**
* Label **get_name_label**()
* void **set_name_label**(value: Label)

Displays entity name.

---

#### health_bar
{: #health_bar }

ProgressBar **health_bar**
* ProgressBar **get_health_bar**()
* void **set_health_bar**(value: ProgressBar)

Visual health bar indicator.

---

#### health
{: #health }

Label **health**
* Label **get_health**()
* void **set_health**(value: Label)

Numerical health display.

---

#### resource_bar
{: #resource_bar }

ProgressBar **resource_bar**
* ProgressBar **get_resource_bar**()
* void **set_resource_bar**(value: ProgressBar)

Visual resource bar indicator.

---

#### resource
{: #resource }

Label **resource**
* Label **get_resource**()
* void **set_resource**(value: Label)

Numerical resource display.

---

#### cast_bar
{: #cast_bar }

ProgressBar **cast_bar**
* ProgressBar **get_cast_bar**()
* void **set_cast_bar**(value: ProgressBar)

Cast progress indicator.

---

#### cast_bar_ability_name
{: #cast_bar_ability_name }

Label **cast_bar_ability_name**
* Label **get_cast_bar_ability_name**()
* void **set_cast_bar_ability_name**(value: Label)

Displays current casting ability name.

---

#### cast_bar_timer_text
{: #cast_bar_timer_text }

Label **cast_bar_timer_text**
* Label **get_cast_bar_timer_text**()
* void **set_cast_bar_timer_text**(value: Label)

Displays remaining cast time.

---

#### cast_bar_timer
{: #cast_bar_timer }

Timer **cast_bar_timer**
* Timer **get_cast_bar_timer**()
* void **set_cast_bar_timer**(value: Timer)

Controls cast duration timing.

---

#### buff_grid
{: #buff_grid }

GridContainer **buff_grid**
* GridContainer **get_buff_grid**()
* void **set_buff_grid**(value: GridContainer)

Layout container for buff icons.

---

#### debuff_grid
{: #debuff_grid }

GridContainer **debuff_grid**
* GridContainer **get_debuff_grid**()
* void **set_debuff_grid**(value: GridContainer)

Layout container for debuff icons.

# Method Descriptions

## _ready
{: #_ready }

void **_ready**()

Sets up aura slot arrays based on entity type. Boss entities get more aura slots than regular entities.

---

## nameplate_setup
{: #nameplate_setup }

void **nameplate_setup**(entity: Entity)

Initializes the nameplate for a given entity, setting up health bars, resource bars, and connecting signals.

Parameters:
- **entity**: Entity to create nameplate for

---

## connect_signals
{: #connect_signals }

void **connect_signals**()

Connects all required entity signals for health, resource, casting, and effect updates.

---

## _physics_process
{: #_physics_process }

void **_physics_process**(delta: float)

Updates cast bar timer text and progress during casting.

Parameters:
- **delta**: Time elapsed since last frame

---

## update_health
{: #update_health }

void **update_health**(new_health: int)

Updates health bar and text display when entity health changes.

Parameters:
- **new_health**: New health value to display

---

## update_resource
{: #update_resource }

void **update_resource**(new_resource: int)

Updates resource bar and text display when entity resource changes.

Parameters:
- **new_resource**: New resource value to display

---

## add_exisiting_auras
{: #add_exisiting_auras }

void **add_exisiting_auras**()

Creates aura displays for any effects already active on the entity when nameplate is created.

---

## create_aura
{: #create_aura }

void **create_aura**(effect: Effect)

Creates a new aura display for an applied effect.

Parameters:
- **effect**: Effect to create aura for

---

## remove_aura
{: #remove_aura }

void **remove_aura**(effect: Effect)

Removes aura display when an effect expires.

Parameters:
- **effect**: Effect to remove aura for

---

## update_current_aura
{: #update_current_aura }

void **update_current_aura**(effect: Effect)

Updates an existing aura display when effect changes.

Parameters:
- **effect**: Effect to update aura for

---

## cast_bar_active
{: #cast_bar_active }

void **cast_bar_active**(ability: Ability, duration: float)

Activates and configures cast bar for ability casting.

Parameters:
- **ability**: Ability being cast
- **duration**: Cast time duration

---

## cast_bar_stop
{: #cast_bar_stop }

void **cast_bar_stop**()

Stops and hides cast bar when casting ends or is interrupted.

---

## start_timer
{: #start_timer }

void **start_timer**(wait_time: float)

Starts cast bar timer with specified duration.

Parameters:
- **wait_time**: Timer duration in seconds

---

## on_timer_timeout
{: #on_timer_timeout }

void **on_timer_timeout**()

Handles cast timer completion by hiding cast bar elements.

---

## set_nameplate_border_colour
{: #set_nameplate_border_colour }

void **set_nameplate_border_colour**(on_off: int)

Updates nameplate border style based on targeting state.

Parameters:
- **on_off**: State flag (0: normal, 1: targeted, 2: mouse hover)

---

## set_health_bar_colour
{: #set_health_bar_colour }

void **set_health_bar_colour**()

Updates health bar color based on class color settings.

---

## set_resource_bar_colour
{: #set_resource_bar_colour }

void **set_resource_bar_colour**()

Updates resource bar color based on entity's resource type.

---

## _on_nameplate_update
{: #_on_nameplate_update }

void **_on_nameplate_update**()

Updates nameplate visibility and features based on current settings.

---

## _on_interrupt
{: #_on_interrupt }

void **_on_interrupt**()

Plays interrupt animation when entity casting is interrupted.