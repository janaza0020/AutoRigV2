# AutoRig V2 Development Guide

> Developer Handbook

Version: 2.0

---

# Introduction

This document describes how AutoRig V2 should be developed.

The goal is to keep the architecture stable while allowing new rig types
and new features to be added without modifying the core engine.

---

# Development Philosophy

Never modify the Builder to support a new rig.

Instead

Create Definitions

↓

Register them

↓

Run the Builder

---

# Project Layers

UI

↓

Operators

↓

Builder

↓

Pipeline

↓

Tasks

↓

Services

↓

Blender API

Each layer has one responsibility.

---

# Development Order

Always follow this order.

## Phase 1

Core

- constants.py
- config.py
- definitions.py

---

## Phase 2

Models

- bone_name.py
- guide.py
- chain.py
- build_context.py

---

## Phase 3

Services

- guide_service.py
- bone_factory.py
- duplicate_service.py
- constraint_service.py
- controller_service.py
- widget_service.py
- collection_service.py
- driver_service.py
- mirror_service.py
- validation_service.py

---

## Phase 4

Builder

- pipeline.py
- builder.py
- task.py

---

## Phase 5

Tasks

Create every build stage.

---

## Phase 6

UI

Operators

Properties

Panel

Preferences

---

# Before Creating New Features

Ask

Can this be solved with Definitions?

If yes

Do not modify Builder.

---

# Adding a New Chain

Create

ChainDefinition

↓

Register

↓

Done

Builder remains unchanged.

---

# Adding a New Rig Type

Example

Dragon

Create

DragonDefinition

↓

Register

↓

Finished

No Builder modification.

---

# Adding a New Service

Check

Does another Service already solve this?

If yes

Reuse it.

Avoid duplicate functionality.

---

# Dependency Rules

Definitions

↓

Models

↓

Services

↓

Tasks

↓

Pipeline

↓

Builder

↓

Operators

Never reverse dependencies.

---

# Build Flow

Load Guides

↓

Validate

↓

Create Root

↓

Generate DEF

↓

Generate FK

↓

Generate IK

↓

Controllers

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

---

# Validation Checklist

Before Build

Guide Exists

Bone Names Valid

Mirror Valid

Collections Ready

Widgets Ready

No Duplicate Bones

---

# Performance Checklist

Cache Guides

Cache Bones

Cache Pose Bones

Avoid bpy.ops

Avoid mode switching

Avoid repeated lookups

---

# Debug Checklist

Logger Enabled

Performance Timer

Validation Report

Build Report

---

# Code Review Checklist

Functions under 80 lines

Type Hint present

Docstrings written

No duplicated code

No Blender API outside Services

Naming follows Coding Standard

---

# Pull Request Checklist

Build passes

Validation passes

No regression

Documentation updated

Roadmap updated

---

# Future Modules

Registry

Plugin System

Dependency Graph

Transaction Build

Undo Safe Build

Rig Templates

Creature Library

---

# Versioning

Major

Architecture changes

Minor

New features

Patch

Bug fixes

---

# Documentation

Whenever a feature is added

Update

README

ROADMAP

ARCHITECTURE

Development Guide

if necessary.

Documentation is considered part of the codebase.

---

# Long Term Vision

AutoRig V2 should evolve into a reusable rig generation engine.

Supported rigs should include

- Human
- Stylized Human
- Creature
- Dragon
- Quadruped
- Mechanical
- Tentacle
- Facial Rig

without modifying the core Builder.

Only Definitions, Tasks, and optional Plugins should be extended.

The architecture should remain stable across future versions.
