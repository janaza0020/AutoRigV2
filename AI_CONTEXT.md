# AI_CONTEXT.md

# AutoRig V2 AI Context

> This document provides project context specifically for AI assistants.

Version: 2.0

---

# Purpose

This file exists to help AI assistants understand the project before writing
any code.

Read this document together with

- README.md
- ROADMAP.md
- ARCHITECTURE.md
- CODING_STANDARD.md
- DEVELOPMENT_GUIDE.md
- CONTRIBUTING.md

before implementing new features.

---

# Project Summary

AutoRig V2 is a complete rewrite of an existing Blender Auto Rig addon.

The original implementation worked but became increasingly difficult to
maintain because rig generation, Blender API calls, UI logic, and helper
functions were tightly coupled.

AutoRig V2 separates those responsibilities into independent modules.

The objective is not only to generate a Human Rig, but to become a reusable
rig generation framework.

---

# Long-Term Vision

The engine should eventually support

- Human
- Stylized Human
- Creature
- Quadruped
- Dragon
- Mechanical Rig
- Facial Rig
- Tail
- Wing
- Tentacle

without changing the core Builder.

The Builder should remain stable across future versions.

---

# Primary Design Philosophy

Everything should be Data Driven.

Avoid hardcoded logic.

The Builder should never know

- Arm
- Leg
- Spine
- Finger
- Tail

Instead, the Builder receives Definitions.

Definitions describe the rig.

The Builder builds the rig.

---

# Architecture Overview

UI

↓

Operators

↓

Rig Builder

↓

Pipeline

↓

Tasks

↓

Services

↓

Blender API

No layer should bypass another.

---

# Builder Responsibilities

The Builder only coordinates execution.

The Builder should NEVER

- create bones
- create constraints
- create widgets
- create drivers

Those responsibilities belong to Services.

---

# Definitions

Definitions describe

- Chains
- Bones
- IK
- Controllers
- Widgets

Definitions must contain data only.

No bpy imports.

No Blender logic.

---

# Services

Services are the only layer allowed to communicate directly with Blender.

Examples

GuideService

BoneFactory

ConstraintService

WidgetService

DriverService

MirrorService

ValidationService

CollectionService

Services should remain reusable.

---

# Tasks

Tasks perform one build stage.

Examples

CreateDEF

DuplicateFK

DuplicateIK

GenerateControllers

GenerateConstraints

GenerateDrivers

GenerateWidgets

AssignCollections

Finalize

Tasks should be independent whenever possible.

---

# Context Object

Avoid passing many parameters.

Everything required for building should exist inside

BuildContext

Every Task should receive only

ctx

---

# Guide System

Guide locations are cached before building.

Avoid repeated Blender lookups.

GuideCache should provide

- Object
- Location
- Rotation
- Matrix
- Scale

Future systems may require orientation information.

---

# Naming System

Never manipulate bone names using string replacement.

Use BoneName instead.

BoneName separates

Prefix

Base

Side

This avoids fragile string operations.

---

# Performance Rules

Prefer

- Cache
- Data reuse
- One Blender lookup

Avoid

- Repeated bpy.data access
- Repeated mode switching
- Repeated object lookup

Performance is a design requirement.

---

# Error Handling

Do not use generic Exception.

Use descriptive exceptions.

Examples

GuideNotFoundError

InvalidChainError

DuplicateBoneError

BuildCancelledError

Every exception should explain

- what happened
- why
- possible solution

---

# Validation

Always validate before build.

Check

- Missing Guides
- Invalid Chains
- Duplicate Bones
- Missing Collections
- Invalid Parents

Fail early.

---

# Coding Style

Follow

PEP8

Use

Type Hint

Dataclass

Slots

Docstrings

Small functions

Avoid duplicated code.

---

# Blender API

Keep Blender API isolated.

Models

Definitions

Pipeline

Builder

must not directly manipulate Blender objects.

Only Services should do so.

---

# Current Development Stage

Architecture Phase

Completed

- constants.py
- bone_name.py
- guide_cache.py
- definitions.py

Currently Planned

- Models
- Services
- Builder
- Tasks
- UI

Follow ROADMAP.md.

---

# AI Development Rules

When generating code

Prefer

- Composition
- Small modules
- Reusable Services
- Factory Pattern
- Builder Pattern
- Pipeline Pattern
- Registry Pattern

Avoid

- Giant functions
- Giant classes
- Hardcoded strings
- Duplicate logic

Whenever possible

Reduce code duplication before adding features.

---

# Preferred Response Style

When proposing architecture improvements

Explain

- Why
- Benefits
- Trade-offs

When writing code

Produce production-quality code.

Avoid pseudo-code.

Include

- Type hints
- Docstrings
- Error handling

Follow the project architecture.

---

# If Architecture Conflicts

When new requirements conflict with existing architecture

Do not immediately modify the Builder.

First consider whether the feature can be implemented by extending

- Definitions
- Tasks
- Services
- Registry
- Plugins

Only redesign the Builder when absolutely necessary.

---

# Project Goal

The final result should resemble a reusable rigging engine rather than a
single Blender addon.

The architecture should remain understandable after several years of
development.

Every new feature should improve the engine without increasing unnecessary
complexity.

Keep the core stable.

Keep the code clean.

Keep everything modular.
