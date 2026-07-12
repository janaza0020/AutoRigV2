# AutoRig V2 Architecture

> Software Architecture Documentation

Version : 2.0

Status : Designing

---

# Vision

AutoRig V2 is not intended to be a single Human Auto Rig addon.

The long-term objective is to become a **modular rig generation framework**
capable of generating multiple rig types using the same engine.

Examples

- Human
- Stylized Human
- Creature
- Dragon
- Quadruped
- Mechanical Rig

The engine itself should never require modification when adding new rig types.

Only the Definitions should change.

---

# Design Goals

## Simplicity

Small modules.

Single responsibility.

Easy to understand.

---

## Extensibility

Adding new rig types should require creating only new Definitions.

---

## Performance

Avoid unnecessary Blender API calls.

Use caching wherever possible.

Avoid repeated mode switching.

---

## Reliability

Every build should be validated before execution.

Rollback should be possible when build fails.

---

## Maintainability

No duplicated logic.

Every system has a dedicated responsibility.

---

# High Level Architecture

```
                User

                  │

                  ▼

             UI Panel

                  │

                  ▼

             Operators

                  │

                  ▼

            Rig Builder

                  │

        Build Pipeline

                  │

      ┌───────────┼────────────┐

      ▼           ▼            ▼

  Build Tasks  Validation   Logger

      │

      ▼

    Services

      │

      ▼

 Blender API
```

---

# Layer Overview

## UI Layer

Responsible only for user interaction.

Contains

- Panel
- Operators
- Properties
- Preferences

No rigging logic is allowed here.

---

## Builder Layer

Responsible for orchestration.

The Builder never creates bones.

The Builder never creates constraints.

The Builder only coordinates tasks.

---

## Pipeline Layer

Executes Tasks.

Determines execution order.

Handles task dependencies.

Provides build context.

---

## Task Layer

A Task performs one build stage.

Examples

- Create Root
- Create DEF
- Duplicate FK
- Duplicate IK
- Generate Controllers
- Generate Widgets
- Assign Collections

Tasks should remain independent.

---

## Service Layer

Contains all implementation.

Examples

BoneFactory

ConstraintService

DriverService

WidgetService

CollectionService

GuideService

MirrorService

ValidationService

Services are reusable.

---

## Model Layer

Contains pure data.

No Blender operations.

Examples

BoneName

Guide

ChainDefinition

BoneDefinition

BuildContext

---

# Build Pipeline

```
Load Guides

↓

Validate

↓

Create Root

↓

Create DEF

↓

Duplicate FK

↓

Duplicate IK

↓

Generate Controllers

↓

Constraints

↓

Drivers

↓

Widgets

↓

Collections

↓

Finalize
```

---

# Dependency Graph

```
Guide

↓

DEF

↓

FK

↓

IK

↓

Controller

↓

Constraint

↓

Driver

↓

Widget

↓

Collection
```

Every task declares its dependencies.

The Pipeline resolves execution order.

---

# Data Driven Architecture

The Builder never knows

- Arm
- Leg
- Spine
- Tail
- Finger

Everything comes from Definitions.

Example

```
Definition

↓

Builder

↓

Rig
```

To support another creature

Create a new Definition.

No Builder changes required.

---

# Definition System

Every rig component is represented as data.

Example

ChainDefinition

↓

BoneDefinition

↓

IKDefinition

↓

ControllerDefinition

↓

WidgetDefinition

The Builder reads Definitions.

It never hardcodes bone creation.

---

# Bone Naming

All bone names are represented by BoneName.

Instead of

```
DEF_UpperArm.L
```

The engine stores

```
prefix

DEF

base

UpperArm

side

L
```

Benefits

- safer
- easier to manipulate
- no replace()

---

# Guide System

Guide locations are loaded once.

GuideCache stores

- object
- location
- rotation
- matrix
- scale

No repeated guide search.

---

# Factory Pattern

All Blender API creation happens inside factories.

Factories

BoneFactory

ConstraintFactory

WidgetFactory

CollectionFactory

DriverFactory

Advantages

- centralized
- reusable
- testable

---

# Service Responsibilities

GuideService

Loads Guides

BoneFactory

Creates edit bones

DuplicateService

Duplicates chains

ConstraintService

Creates constraints

DriverService

Creates drivers

WidgetService

Creates controller shapes

CollectionService

Assigns Bone Collections

ValidationService

Checks build requirements

MirrorService

Handles symmetry

---

# Build Context

Instead of passing many variables

```
context

armature

guides

properties

settings
```

Everything is stored inside

BuildContext

Every Task receives

```
ctx
```

only.

---

# Validation

Before build

Check

✓ Guide Exists

✓ Duplicate Bones

✓ Invalid Parent

✓ Missing Collection

✓ Missing Widgets

If validation fails

Build stops.

---

# Error Handling

Custom exceptions

GuideNotFoundError

InvalidChainError

DuplicateBoneError

BuildCancelledError

Every error should explain

- what happened

- why

- how to fix it

---

# Logging

Levels

INFO

WARNING

ERROR

DEBUG

Performance log

Task timing

Total build time

Build statistics

---

# Future Features

Plugin System

Registry

Dependency Graph

Event System

Transaction Build

Undo Safe Build

Rig Templates

Creature Library

---

# Folder Structure

```
AutoRigV2/

README.md
ROADMAP.md
ARCHITECTURE.md

autorig/

    builder/

    services/

    models/

    tasks/

    ui/

docs/

tests/
```

---

# Coding Standards

Python

PEP8

Type Hint Required

Dataclass where appropriate

Slots enabled whenever possible

Avoid global state

Avoid duplicated logic

Prefer composition over inheritance

No Blender API outside Services

---

# Design Patterns

Builder Pattern

Factory Pattern

Pipeline Pattern

Dependency Injection

Service Layer

Registry Pattern

Strategy Pattern

Data Driven Design

---

# Long Term Goal

AutoRig V2 should evolve into a reusable rig generation framework.

The Builder should never need modification when adding

- Tail

- Wing

- Dragon

- Animal

- Robot

Only Definitions and optional Plugins should change.

The architecture should remain stable for future development.
