# AutoRig V2 Coding Standard

> Official Coding Standard for AutoRig V2

Version: 2.0

---

# Purpose

This document defines the coding standards used throughout AutoRig V2.

Every module should follow these rules to ensure consistency,
maintainability, and readability.

---

# General Principles

Follow these principles in every file.

- Readability over cleverness
- Explicit over implicit
- Composition over inheritance
- Data Driven over hardcoded logic
- Small reusable components
- Single Responsibility Principle
- Avoid duplicated code
- Keep Blender API isolated

---

# Python Version

Python 3.11+

Blender 4.x

---

# Style Guide

Follow

PEP8

Maximum line length

88 characters

Use Black formatting whenever possible.

---

# Naming Convention

## Modules

snake_case.py

Example

guide_service.py

bone_factory.py

build_context.py

---

## Classes

PascalCase

Example

RigBuilder

GuideCache

ConstraintService

BoneFactory

---

## Functions

snake_case

Example

create_chain()

build()

duplicate_chain()

load_guides()

---

## Variables

snake_case

Example

guide_location

bone_name

edit_bone

constraint_list

---

## Constants

UPPER_CASE

Example

DEFAULT_BONE_LENGTH

MAX_CHAIN_DEPTH

ROOT_NAME

---

## Enum

PascalCase

Members

UPPER_CASE

Example

RigType.DEF

RigType.FK

RigType.IK

---

# Type Hint

Type hints are required.

Bad

def create(name):

Good

def create(name: str) -> EditBone:

---

# Dataclass

Prefer dataclass for data containers.

Always use

@dataclass(slots=True)

unless mutability requires otherwise.

---

# Class Responsibilities

Each class should have one responsibility.

Good

GuideCache

only caches guides.

Bad

GuideCache

creates bones

creates widgets

creates constraints

---

# Function Size

Recommended

20–40 lines

Maximum

80 lines

Split large functions.

---

# Comments

Only explain WHY.

Do not explain WHAT.

Bad

# Create bone

Good

# Bone roll must match Blender's X-axis to avoid IK flipping.

---

# Docstrings

Public classes

Required

Public functions

Required

Private methods

Optional

Use Google Style.

Example

def build():

    """
    Build the complete rig.

    Returns:
        None
    """

---

# Imports

Standard Library

↓

Third Party

↓

Blender API

↓

Local Modules

Example

import math

from dataclasses import dataclass

import bpy

from .definitions import ChainDefinition

---

# Blender API Rules

Never call Blender API outside Services.

Allowed

BoneFactory

ConstraintService

GuideService

Not allowed

Definitions

Models

Builder

---

# Build Context

Never pass multiple objects.

Bad

build(context, armature, guides, settings)

Good

build(ctx)

---

# Error Handling

Never raise generic Exception.

Create custom exceptions.

Example

GuideNotFoundError

DuplicateBoneError

InvalidChainError

BuildCancelledError

---

# Logging

Use Logger.

Never use print().

Levels

INFO

WARNING

ERROR

DEBUG

---

# Caching

Expensive Blender lookups must be cached.

Examples

Guides

Edit Bones

Pose Bones

Collections

Widgets

---

# Builder Rules

Builder must not

Create Bones

Create Constraints

Create Drivers

Builder only

Coordinates Tasks

---

# Task Rules

One task

One responsibility.

Good

CreateDEFTask

Bad

CreateEverythingTask

---

# Service Rules

Services may use Blender API.

Services should not call Operators.

Services should be reusable.

---

# Factory Rules

Factories create objects.

Factories never manage workflow.

Examples

BoneFactory

ConstraintFactory

WidgetFactory

---

# Definitions

Definitions are data only.

No Blender logic.

No bpy imports.

---

# Testing

Every Service should be independently testable.

Avoid hidden global state.

---

# Performance

Avoid

Repeated mode switching

Repeated guide lookup

Repeated bone lookup

Repeated constraint lookup

Cache whenever possible.

---

# Architecture Rule

UI

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

Never bypass layers.

---

# Commit Rules

Every commit should

Compile

Build

Pass Validation

Follow Coding Standard

---

# Golden Rule

If a function becomes difficult to explain,

split it.

Small code is easier to maintain than clever code.
