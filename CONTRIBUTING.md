# Contributing to AutoRig V2

> Thank you for contributing to AutoRig V2!

This document describes the workflow, coding practices, and development rules
for contributing to this project.

The primary goal is to keep the project clean, maintainable, and extensible
without introducing unnecessary complexity.

---

# Project Philosophy

AutoRig V2 is designed around one core principle:

> **The Builder should remain stable.**

When adding new features, contributors should extend the system through
Definitions, Tasks, Services, or Plugins instead of modifying the Builder
whenever possible.

---

# Architecture First

Before writing code, read these documents:

1. README.md
2. ROADMAP.md
3. ARCHITECTURE.md
4. CODING_STANDARD.md
5. DEVELOPMENT_GUIDE.md

Do not start implementing new features without understanding the project
architecture.

---

# Development Workflow

Recommended workflow

```

Fork Repository

↓

Create Branch

↓

Implement Feature

↓

Test

↓

Update Documentation

↓

Commit

↓

Pull Request

```

---

# Branch Naming

Use descriptive branch names.

Examples

```

feature/bone-factory

feature/guide-cache

feature/widget-system

feature/plugin-system

bugfix/pole-angle

bugfix/mirror

refactor/builder

docs/readme

performance/cache

```

---

# Commit Convention

Follow Conventional Commits.

Examples

```

feat: add BoneFactory

feat: implement GuideCache

fix: correct pole angle calculation

fix: prevent duplicate bone creation

refactor: simplify ConstraintService

docs: update architecture

perf: cache guide lookup

test: add validation tests

```

---

# Pull Request Checklist

Before opening a Pull Request, verify the following:

- [ ] Project builds successfully
- [ ] Validation passes
- [ ] No duplicate code introduced
- [ ] Blender API is only used inside Services
- [ ] Type hints are included
- [ ] Public APIs include docstrings
- [ ] Documentation updated if required
- [ ] ROADMAP updated (if feature completed)
- [ ] CHANGELOG updated (if applicable)

---

# Coding Rules

Every contribution must follow

- CODING_STANDARD.md
- DEVELOPMENT_GUIDE.md

Do not introduce a different coding style.

---

# Architecture Rules

Never bypass the architecture.

Correct flow

```

UI

↓

Operator

↓

Builder

↓

Pipeline

↓

Task

↓

Service

↓

Blender API

```

Avoid

```

Operator

↓

Blender API

```

or

```

Builder

↓

bpy.ops

```

---

# Builder Rules

The Builder coordinates work.

The Builder should NOT

- create bones
- create constraints
- create drivers
- create widgets

Those responsibilities belong to Services.

---

# Service Rules

Each Service has one responsibility.

Examples

GuideService

BoneFactory

ConstraintService

WidgetService

CollectionService

DriverService

MirrorService

ValidationService

Services should be reusable.

---

# Definition Rules

Definitions are data only.

Definitions must never

- import bpy
- create bones
- modify Blender objects

Definitions describe the rig.

They never build the rig.

---

# Performance Guidelines

Always consider performance.

Preferred

- Cache Blender lookups
- Cache guide locations
- Cache edit bones
- Cache pose bones

Avoid

- Repeated bpy.data lookups
- Frequent mode switching
- Duplicate calculations

---

# Error Handling

Do not raise generic exceptions.

Create descriptive custom exceptions.

Examples

GuideNotFoundError

DuplicateBoneError

InvalidChainError

BuildCancelledError

Every error should clearly explain

- what happened
- why it happened
- how to fix it

---

# Documentation

Documentation is part of the codebase.

Whenever architecture changes

Update

- README.md
- ROADMAP.md
- ARCHITECTURE.md

When implementation changes

Update

- DEVELOPMENT_GUIDE.md
- API documentation (if applicable)

---

# Testing

Before merging

Verify

- Guide generation
- DEF creation
- FK generation
- IK generation
- Pole Targets
- Controllers
- Constraints
- Drivers
- Widgets
- Bone Collections

Every major feature should be manually tested in Blender.

---

# Design Principles

When making implementation decisions, prefer

- Readability over cleverness
- Simplicity over complexity
- Composition over inheritance
- Data over hardcoded logic
- Reusable services
- Small focused modules

---

# What Should NOT Be Added

Avoid

- Giant classes
- Giant functions
- Hardcoded bone names
- Hardcoded collections
- Hardcoded widget logic
- Business logic inside Operators
- Business logic inside UI

---

# Long-Term Vision

AutoRig V2 is intended to become a reusable rig generation framework.

Future rig types should include

- Human
- Stylized Human
- Creature
- Quadruped
- Dragon
- Mechanical
- Facial
- Tail
- Wing
- Tentacle

The Builder should remain unchanged while new Definitions, Tasks, or Plugins
extend the engine.

---

# Need Help?

If you're unsure where a feature belongs, ask yourself:

> Can this be solved by extending Definitions, Services, Tasks, or Plugins?

If the answer is "yes", avoid modifying the Builder.

When in doubt, preserve the architecture and keep the engine modular.

Thank you for helping improve AutoRig V2!
