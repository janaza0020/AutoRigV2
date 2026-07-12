# PROJECT_STATE.md

> Current development state of AutoRig V2

**Project:** AutoRig V2  
**Version:** v2.0.0-alpha.1  
**Status:** 🚧 Architecture Phase  
**Last Updated:** 2026-07-09

---

# Overview

AutoRig V2 is a complete rewrite of the original Blender Auto Rig addon.

This project focuses on creating a modular, data-driven rig generation engine
instead of extending the legacy implementation.

The architecture is designed for long-term maintainability, scalability, and
future support for multiple rig types.

---

# Current Milestone

## Milestone 1

**Architecture & Foundation**

Status

🟡 In Progress

Goal

Design and implement the project architecture before writing production
features.

---

# Current Progress

## Documentation

| File | Status |
|------|--------|
| README.md | ✅ Complete |
| ROADMAP.md | ✅ Complete |
| ARCHITECTURE.md | ✅ Complete |
| CODING_STANDARD.md | ✅ Complete |
| DEVELOPMENT_GUIDE.md | ✅ Complete |
| CONTRIBUTING.md | ✅ Complete |
| AI_CONTEXT.md | ✅ Complete |
| PROJECT_STATE.md | ✅ Current |

---

## Core

| Module | Status |
|----------|--------|
| constants.py | ✅ Designed |
| bone_name.py | ✅ Designed |
| guide_cache.py | ✅ Designed |
| definitions.py | ✅ Designed |

---

## Models

| Module | Status |
|----------|--------|
| guide.py | ⏳ Planned |
| build_context.py | ⏳ Planned |
| chain.py | ⏳ Planned |

---

## Services

| Module | Status |
|----------|--------|
| guide_service.py | ⏳ Planned |
| bone_factory.py | ⏳ Planned |
| duplicate_service.py | ⏳ Planned |
| constraint_service.py | ⏳ Planned |
| controller_service.py | ⏳ Planned |
| widget_service.py | ⏳ Planned |
| collection_service.py | ⏳ Planned |
| driver_service.py | ⏳ Planned |
| mirror_service.py | ⏳ Planned |
| validation_service.py | ⏳ Planned |
| logger.py | ⏳ Planned |

---

## Builder

| Module | Status |
|----------|--------|
| builder.py | ⏳ Planned |
| pipeline.py | ⏳ Planned |
| task.py | ⏳ Planned |

---

## Tasks

Status

⏳ Planned

Expected Tasks

- CreateRoot
- CreateDEF
- DuplicateFK
- DuplicateIK
- CreateControllers
- CreateConstraints
- CreateDrivers
- CreateWidgets
- AssignCollections
- Finalize

---

## UI

Status

⏳ Planned

Modules

- operators.py
- panel.py
- properties.py
- preferences.py

---

# Architecture Decisions

The following decisions are considered stable.

## Builder

The Builder is responsible only for orchestration.

It should never directly manipulate Blender objects.

---

## Pipeline

The Pipeline executes build tasks.

Tasks remain independent whenever possible.

---

## Services

Only Services are allowed to interact directly with the Blender API.

---

## Definitions

Definitions contain data only.

No Blender API.

No business logic.

---

## Build Context

Every build stage receives a single BuildContext instance.

Avoid passing multiple parameters.

---

## Naming

Bone names are represented by the BoneName class.

Avoid string replacement.

---

## Performance

Guide lookup must be cached.

Bone lookup should be cached.

Avoid repeated Blender API calls.

---

# Design Patterns

Approved patterns

- Builder Pattern
- Factory Pattern
- Pipeline Pattern
- Registry Pattern
- Dependency Injection
- Service Layer
- Data Driven Design

Avoid introducing unnecessary new patterns unless they provide clear value.

---

# Known Design Decisions

These decisions should remain unchanged unless there is a compelling reason.

- Builder is orchestration only.
- Services own Blender API interaction.
- Definitions are pure data.
- Build is task-based.
- Guide locations are cached.
- Bone creation goes through BoneFactory.
- Constraint creation goes through ConstraintService.
- Widget generation goes through WidgetService.

---

# Outstanding Questions

The following topics require further implementation and validation.

- IK Pole angle customization
- Twist Bone support
- Stretch IK
- Custom Controller Shapes
- Face Rig architecture
- Plugin loading system
- Registry implementation
- Event system
- Transaction / Rollback support

---

# Next Priority

Highest Priority

1. Implement guide.py
2. Implement build_context.py
3. Implement chain.py
4. Implement guide_service.py
5. Implement bone_factory.py

After those modules are complete

Continue with

- Pipeline
- Builder
- Tasks

---

# Future Milestones

## Milestone 2

Core Services

---

## Milestone 3

Rig Builder

---

## Milestone 4

Human Rig Generation

---

## Milestone 5

UI

---

## Milestone 6

Testing

---

## Milestone 7

Optimization

---

## Milestone 8

Plugin System

---

## Milestone 9

Creature Support

---

## Milestone 10

Release Candidate

---

# Known Risks

Potential risks

- Blender API changes
- IK solver edge cases
- Pole vector calculation
- Mirror naming edge cases
- Large rig performance
- Constraint dependency order

---

# Notes For Future Development

Whenever a new feature is proposed, evaluate whether it can be implemented by

- extending Definitions
- adding a new Task
- adding a new Service
- registering a new component

Avoid modifying the Builder unless absolutely necessary.

---

# Session Notes

This project originated as a refactor of an existing Auto Rig addon.

During the design phase, the architecture evolved into a reusable rig
generation engine.

The long-term objective is to build a stable framework capable of supporting
multiple rig types without redesigning the core engine.

---

# Current Repository Status

Documentation

██████████████░░░░ 70%

Architecture

██████████████████ 100%

Core Design

███████████████░░░ 85%

Implementation

██░░░░░░░░░░░░░░░░ 10%

Testing

░░░░░░░░░░░░░░░░░░ 0%

Release Readiness

░░░░░░░░░░░░░░░░░░ 0%

---

# Development Resume Prompt

When continuing development in a new ChatGPT conversation, use the following prompt:

> Read the following documents before writing any code:
>
> - README.md
> - ROADMAP.md
> - ARCHITECTURE.md
> - CODING_STANDARD.md
> - DEVELOPMENT_GUIDE.md
> - CONTRIBUTING.md
> - AI_CONTEXT.md
> - PROJECT_STATE.md
>
> Follow the architecture exactly.
> Continue implementation from the current project state.
> Do not redesign completed systems unless necessary.
> Produce production-ready code only.

---

# End of File
