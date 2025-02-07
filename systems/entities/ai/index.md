---
layout: default
title: AI
parent: Entity System
nav_order: 6
has_children: true
permalink: /systems/entities/ai/
---

# AI System

## Description
The ai system is controlled by a central StateMachine which will build states depending on the exported properties on setup.
States all in inherit from a base State class, all states related to locomotion inherit from a MovementState class.

## AI Classes
- [StateMachine](./state-machine.md)

- [State](./state.md)
- [InactiveState](./inactive-state.md)
- [TargetSearchState](./target-search-state.md)
- [ChasingState](./chasing-state.md)
- [AttackingState](./attacking-state.md)
- [IncapacitatedState](./incapacitated-state.md)
- [FollowingState](./following-state.md)
- [PatrollingState](./patrolling-state.md)
- [DeadState](./dead-state.md)
- [PlayerCommandState](./player-command-state.md)

- [MovementState](./movement-state.md)
- [IdleState](./idle-state.md)
- [RunningState](./running-state.md)
- [WalkingState](./walking-state.md)
- [FallingState](./falling-state.md)

