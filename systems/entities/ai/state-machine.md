---
layout: default
title: State Machine
parent: AI
nav_order: 1
permalink: /systems/entities/ai/state-machine
---

---
layout: default
title: StateMachine
parent: State System
nav_order: 1
permalink: /systems/states/state-machine/
---

# StateMachine

Inherits: [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)

## Description

StateMachine manages the state system for entities in the game. It handles transitions between different movement and action states, coordinates AI behavior, and manages combat interactions.

Key features:
- Manages separate movement and action states
- Dynamically creates state nodes based on configuration
- Handles state transitions and updates
- Coordinates with combat scripts for AI behavior
- Manages detection areas for entity interactions
- Provides flexibility for different entity types (e.g., companions, bosses)

## Properties

### Exported Properties

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| String | initial_movement_state | "idle" | Initial movement state to be set on startup |
| String | initial_action_state | "inactive" | Initial action state to be set on startup |
| Node | combat_script | null | Reference to the combat script that handles AI behavior |

### Movement State Flags

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | has_idle_state | true | Enable idle movement state |
| bool | has_walking_state | true | Enable walking movement state |
| bool | has_running_state | true | Enable running movement state |
| bool | has_falling_state | true | Enable falling movement state |

### Action State Flags

| Type | Property | Default | Description |
|------|----------|---------|-------------|
| bool | has_inactive_state | true | Enable inactive action state |
| bool | has_incapacitated_state | true | Enable incapacitated action state |
| bool | has_following_state | true | Enable following action state |
| bool | has_patrolling_state | true | Enable patrolling action state |
| bool | has_chasing_state | true | Enable chasing action state |
| bool | has_attacking_state | true | Enable attacking action state |
| bool | has_target_search_state | true | Enable target search action state |
| bool | has_dead_state | true | Enable dead action state |
| bool | has_player_command_state | true | Enable player command action state |

### General Properties

| Type | Property | Description |
|------|----------|-------------|
| State | current_movement_state | Currently active movement state |
| State | current_action_state | Currently active action state |
| Dictionary | movement_states | Dictionary storing all movement states |
| Dictionary | action_states | Dictionary storing all action states |
| Entity | entity | Reference to the controlled entity |
| Area3D | pull_range_area | Detection area for pull range |
| Area3D | attack_range_area | Detection area for attack range |

## Methods

| Return Type | Method | Description |
|------------|---------|-------------|
| void | [_setup_ai](#_setup_ai) | Initializes the AI system |
| void | [create_state_nodes](#create_state_nodes) | Creates state nodes based on enabled states |
| void | [create_state_if_enabled](#create_state_if_enabled) | Creates a state node if enabled |
| void | [initialize_states](#initialize_states) | Initializes created state nodes |
| void | [setup_signals_connections](#setup_signals_connections) | Sets up entity signal connections |
| void | [set_detection_radius](#set_detection_radius) | Creates detection areas |
| Area3D | [create_detection_area](#create_detection_area) | Creates an Area3D for detection |
| void | [_on_pull_range_body_entered](#_on_pull_range_body_entered) | Handles pull range entry |
| void | [_physics_process](#_physics_process) | Updates current states |
| void | [_unhandled_input](#_unhandled_input) | Handles input events |
| void | [change_movement_state](#change_movement_state) | Changes movement state |
| void | [change_action_state](#change_action_state) | Changes action state |
| State | [get_movement_state](#get_movement_state) | Gets movement state by name |
| State | [get_action_state](#get_action_state) | Gets action state by name |
| void | [_on_entity_death](#_on_entity_death) | Handles entity death |
| void | [_on_formation_updated](#_on_formation_updated) | Updates following state |
| void | [handle_player_command_input](#handle_player_command_input) | Handles player commands |

# Property Descriptions

## Exported Properties

#### initial_movement_state
{: #initial_movement_state }

String **initial_movement_state** = `"idle"`
* String **get_initial_movement_state**()
* void **set_initial_movement_state**(value: String)

Initial movement state to be set when the state machine starts. Must correspond to an enabled movement state.

---

#### initial_action_state
{: #initial_action_state }

String **initial_action_state** = `"inactive"`
* String **get_initial_action_state**()
* void **set_initial_action_state**(value: String)

Initial action state to be set when the state machine starts. Must correspond to an enabled action state.

---

#### combat_script
{: #combat_script }

Node **combat_script**
* Node **get_combat_script**()
* void **set_combat_script**(value: Node)

Reference to the combat script that handles AI behavior and combat decisions.

## Movement State Flags

#### has_idle_state
{: #has_idle_state }

bool **has_idle_state** = `true`
* bool **get_has_idle_state**()
* void **set_has_idle_state**(value: bool)

When true, enables idle movement state for stationary behavior.

---

#### has_walking_state
{: #has_walking_state }

bool **has_walking_state** = `true`
* bool **get_has_walking_state**()
* void **set_has_walking_state**(value: bool)

When true, enables walking movement state for slower movement.

---

#### has_running_state
{: #has_running_state }

bool **has_running_state** = `true`
* bool **get_has_running_state**()
* void **set_has_running_state**(value: bool)

When true, enables running movement state for faster movement.

---

#### has_falling_state
{: #has_falling_state }

bool **has_falling_state** = `true`
* bool **get_has_falling_state**()
* void **set_has_falling_state**(value: bool)

When true, enables falling movement state for airborne behavior.

## Action State Flags

#### has_inactive_state
{: #has_inactive_state }

bool **has_inactive_state** = `true`
* bool **get_has_inactive_state**()
* void **set_has_inactive_state**(value: bool)

When true, enables inactive action state for idle behavior.

---

#### has_incapacitated_state
{: #has_incapacitated_state }

bool **has_incapacitated_state** = `true`
* bool **get_has_incapacitated_state**()
* void **set_has_incapacitated_state**(value: bool)

When true, enables incapacitated action state for stunned behavior.

---

#### has_following_state
{: #has_following_state }

bool **has_following_state** = `true`
* bool **get_has_following_state**()
* void **set_has_following_state**(value: bool)

When true, enables following action state for companion/pet behavior.

---

#### has_patrolling_state
{: #has_patrolling_state }

bool **has_patrolling_state** = `true`
* bool **get_has_patrolling_state**()
* void **set_has_patrolling_state**(value: bool)

When true, enables patrolling action state for guard/patrol behavior.

---

#### has_chasing_state
{: #has_chasing_state }

bool **has_chasing_state** = `true`
* bool **get_has_chasing_state**()
* void **set_has_chasing_state**(value: bool)

When true, enables chasing action state for pursuit behavior.

---

#### has_attacking_state
{: #has_attacking_state }

bool **has_attacking_state** = `true`
* bool **get_has_attacking_state**()
* void **set_has_attacking_state**(value: bool)

When true, enables attacking action state for combat behavior.

---

#### has_target_search_state
{: #has_target_search_state }

bool **has_target_search_state** = `true`
* bool **get_has_target_search_state**()
* void **set_has_target_search_state**(value: bool)

When true, enables target search action state for finding new targets.

---

#### has_dead_state
{: #has_dead_state }

bool **has_dead_state** = `true`
* bool **get_has_dead_state**()
* void **set_has_dead_state**(value: bool)

When true, enables dead action state for death behavior.

---

#### has_player_command_state
{: #has_player_command_state }

bool **has_player_command_state** = `true`
* bool **get_has_player_command_state**()
* void **set_has_player_command_state**(value: bool)

When true, enables player command action state for player-controlled behavior.

## General Properties

#### current_movement_state
{: #current_movement_state }

State **current_movement_state**
* State **get_current_movement_state**()
* void **set_current_movement_state**(value: State)

Reference to currently active movement state instance.

---

#### current_action_state
{: #current_action_state }

State **current_action_state**
* State **get_current_action_state**()
* void **set_current_action_state**(value: State)

Reference to currently active action state instance.

---

#### movement_states
{: #movement_states }

Dictionary **movement_states**
* Dictionary **get_movement_states**()
* void **set_movement_states**(value: Dictionary)

Dictionary storing all movement state instances, keyed by lowercase state name.

---

#### action_states
{: #action_states }

Dictionary **action_states**
* Dictionary **get_action_states**()
* void **set_action_states**(value: Dictionary)

Dictionary storing all action state instances, keyed by lowercase state name.

---

#### entity
{: #entity }

Entity **entity**
* Entity **get_entity**()
* void **set_entity**(value: Entity)

Reference to the entity this state machine is controlling.

---

#### pull_range_area
{: #pull_range_area }

Area3D **pull_range_area**
* Area3D **get_pull_range_area**()
* void **set_pull_range_area**(value: Area3D)

Area3D for detecting entities within pull range. Used for initiating combat.

---

#### attack_range_area
{: #attack_range_area }

Area3D **attack_range_area**
* Area3D **get_attack_range_area**()
* void **set_attack_range_area**(value: Area3D)

Area3D for detecting entities within attack range. Used for combat decisions.

# Method Descriptions

#### _setup_ai
{: #_setup_ai }

void **_setup_ai**(ai_entity: Entity)

Initializes the AI system for the given entity. Sets up states, detection areas, and signals.

Parameters:
* ai_entity: Entity - Entity to control

---

#### create_state_nodes
{: #create_state_nodes }

void **create_state_nodes**()

Creates state nodes based on enabled flags. Creates separate nodes for movement and action states.

---

#### create_state_if_enabled
{: #create_state_if_enabled }

void **create_state_if_enabled**(is_enabled: bool, state_name: String, state_class: GDScript, parent_node: Node)

Creates a state node if the corresponding flag is enabled.

Parameters:
* is_enabled: bool - Whether state is enabled
* state_name: String - Name of state
* state_class: GDScript - Class to instantiate
* parent_node: Node - Parent for new state

---

#### initialize_states
{: #initialize_states }

void **initialize_states**()

Initializes all created state nodes and adds them to respective dictionaries.

---

#### setup_signals_connections
{: #setup_signals_connections }

void **setup_signals_connections**()

Sets up signal connections for the entity, including death and formation updates.

---

#### set_detection_radius
{: #set_detection_radius }

void **set_detection_radius**()

Creates detection areas for pull and attack ranges if ranges are set.

---

#### create_detection_area
{: #create_detection_area }

Area3D **create_detection_area**(radius: float, area_name: String)

Creates an Area3D node for detection with specified radius.

Parameters:
* radius: float - Detection radius
* area_name: String - Name for area node

Returns: Area3D node

---

#### _on_pull_range_body_entered
{: #_on_pull_range_body_entered }

void **_on_pull_range_body_entered**(body: Node3D)

Handles entities entering pull range. Initiates combat if appropriate.

Parameters:
* body: Node3D - Entity entering range

---

#### _physics_process
{: #_physics_process }

void **_physics_process**(delta: float)

Updates current states every physics frame.

Parameters:
* delta: float - Time since last frame

---

#### _unhandled_input
{: #_unhandled_input }

void **_unhandled_input**(event: InputEvent)

Handles unhandled input events for current states.

Parameters:
* event: InputEvent - Input event to handle

---

#### change_movement_state
{: #change_movement_state }

void **change_movement_state**(state_name: String)

Changes current movement state if not dead.

Parameters:
* state_name: String - Name of new state

---

#### change_action_state
{: #change_action_state }

void **change_action_state**(state_name: String)

Changes current action state if not dead.

Parameters:
* state_name: String - Name of new state

---

#### get_movement_state
{: #get_movement_state }

State **get_movement_state**(state_name: String)

Retrieves movement state by name.

Parameters:
* state_name: String - Name of state

Returns: State or null if not found

---

#### get_action_state
{: #get_action_state }

State **get_action_state**(state_name: String)

Retrieves action state by name.

Parameters:
* state_name: String - Name of state

Returns: State or null if not found

---

#### _on_entity_death
{: #_on_entity_death }

void **_on_entity_death**(_entity: Entity)

Changes to dead state when entity dies.

Parameters:
* _entity: Entity - Dead entity

---

#### _on_formation_updated
{: #_on_formation_updated }

void **_on_formation_updated**()

Updates following state when formation changes.

---

#### handle_player_command_input
{: #handle_player_command_input }

void **handle_player_command_input**()

Changes to player command state for current player.