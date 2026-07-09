# AutoRigV2
Blender auto rig add-on

> A modular, data-driven auto rigging framework for Blender.

AutoRig V2 is a complete rewrite of the original Auto Rig addon.

Instead of adding more features on top of an increasingly complex codebase,
this project redesigns the entire architecture around a modular build pipeline,
making it easier to maintain, extend, and support future rig types.

The goal is to create an extensible rigging framework rather than a single
human auto rig.

---

# Features

Current Goals

- Human Auto Rig
- DEF / FK / IK generation
- Pole Target generation
- Controller generation
- Constraint automation
- Driver automation
- Widget generation
- Bone Collection management
- Mirror support
- Auto Weight
- Easy Parent

Future Goals

- Creature Rig
- Quadruped
- Dragon
- Mechanical Rig
- Facial Rig
- Tail Rig
- Wing Rig
- Cloth Bones

---

# Design Philosophy

The engine follows a **Data Driven Architecture**.

The Builder does not know what a "Human", "Arm", or "Leg" is.

Instead, everything is defined by data.

```
Definition

↓

Pipeline

↓

Builder

↓

Rig
```

Adding a new rig type should only require adding a new Definition.

The core engine should never need modification.

---

# Project Structure

```
AutoRigV2/

README.md
ROADMAP.md

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

# Core Architecture

```
Guide

↓

Guide Cache

↓

Definitions

↓

Build Pipeline

↓

Tasks

↓

Services

↓

Rig
```

---

# Main Components

## Builder

Controls the entire build process.

Responsible only for orchestration.

---

## Pipeline

Executes build tasks in dependency order.

---

## Services

Contains the implementation.

Examples

- BoneFactory
- ConstraintService
- WidgetService
- DriverService
- CollectionService

---

## Models

Pure data classes.

Examples

- BoneName
- BoneDefinition
- ChainDefinition
- Guide

---

## Tasks

Small independent build stages.

Examples

- Create DEF
- Duplicate FK
- Duplicate IK
- Generate Controllers
- Generate Constraints

---

# Design Principles

- Data Driven
- Single Responsibility
- Service Based
- Pipeline Architecture
- Builder Pattern
- Factory Pattern
- Type Hint Everywhere
- Minimal Hardcoded Logic

---

# Development Status

Current Version

AutoRig V2

Status

Architecture Design

---

# Requirements

Python 3.11+

Blender 4.x

---

# License

MIT License
