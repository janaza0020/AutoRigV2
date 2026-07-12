# AutoRig V2 Roadmap

---

# Phase 1

Core Architecture

Status

In Progress

## Core

- [x] constants.py
- [x] bone_name.py
- [x] guide_cache.py
- [x] definitions.py

---

## Models

- [ ] guide.py
- [ ] build_context.py
- [ ] chain.py

---

## Builder

- [ ] builder.py
- [ ] pipeline.py
- [ ] task.py

---

## Services

- [ ] guide_service.py
- [ ] bone_factory.py
- [ ] duplicate_service.py
- [ ] constraint_service.py
- [ ] controller_service.py
- [ ] widget_service.py
- [ ] collection_service.py
- [ ] driver_service.py
- [ ] mirror_service.py
- [ ] validation_service.py
- [ ] logger.py

---

## Tasks

- [ ] CreateRoot
- [ ] CreateDEF
- [ ] DuplicateFK
- [ ] DuplicateIK
- [ ] CreateControllers
- [ ] CreateConstraints
- [ ] CreateDrivers
- [ ] GenerateWidgets
- [ ] AssignCollections
- [ ] Finalize

---

## UI

- [ ] Operators
- [ ] Properties
- [ ] Preferences
- [ ] Panel

---

# Phase 2

Performance

- [ ] Guide Cache
- [ ] Bone Cache
- [ ] Constraint Cache
- [ ] Widget Cache
- [ ] Collection Cache

---

# Phase 3

Validation

- [ ] Missing Guide Detection
- [ ] Duplicate Bone Detection
- [ ] Invalid Parent Detection
- [ ] Invalid Chain Detection
- [ ] Build Report

---

# Phase 4

Debug

- [ ] Logger
- [ ] Profiler
- [ ] Performance Report
- [ ] Debug Mode

---

# Phase 5

Creature Support

- [ ] Tail
- [ ] Wing
- [ ] Ear
- [ ] Facial Rig
- [ ] Cloth Bone

---

# Phase 6

Framework

- [ ] Plugin System
- [ ] Registry
- [ ] Dependency Graph
- [ ] Event System
- [ ] Transaction System
- [ ] Undo Safe Build

---

# Phase 7

Testing

- [ ] Unit Test
- [ ] Integration Test
- [ ] Benchmark
- [ ] Documentation

---

# Long Term Goal

Create a completely modular rigging framework.

The engine should be capable of generating

- Human
- Stylized Human
- Creature
- Dragon
- Quadruped
- Mechanical Rig

using the same build pipeline.

Only the Definitions should change.

The Builder must remain unchanged.
