# Course Allocation Engine

A high-performance C++ implementation of a capacity-constrained course allocation system based on the Gale-Shapley (Hospital-Residents) matching algorithm.

The engine allocates students to courses while considering:

- Course seat capacities
- Student priority (CGPA)
- Course prerequisites
- Time-slot conflicts
- Student course preferences

The project was built with a focus on both algorithmic efficiency and memory-conscious systems design. Instead of relying heavily on object-oriented abstractions, the implementation uses a data-oriented approach with compact data structures and cache-friendly memory layouts.

---

## Features

### Efficient Matching Algorithm

The allocation process is based on the Hospital-Residents variant of the Gale-Shapley stable matching algorithm.

Key behaviors include:

- Students apply to courses according to their preference lists.
- Courses maintain enrollments up to their seat capacity.
- Higher-priority students can replace lower-priority students when a course is full.
- Evicted students automatically continue applying to their remaining preferences.
- The process continues until no further allocations are possible.

### Constraint Handling

The engine supports:

- Capacity constraints
- Prerequisite validation
- Time-slot conflict detection
- Priority-based admissions

### Systems-Level Optimizations

Several implementation choices were made to improve performance:

- String identifiers are converted to compact integer IDs during preprocessing.
- Core data structures use contiguous memory (`std::vector`) where possible.
- Time slots and prerequisite states are represented using bitmasks for fast validation.
- Course enrollments are maintained using heap-based structures for efficient lowest-priority eviction.

---

## Design Overview

### Student Representation

Each student stores:

- CGPA
- Course preferences
- Completed prerequisites
- Allocated courses

### Course Representation

Each course stores:

- Capacity
- Time-slot information
- Required prerequisites
- Currently enrolled students

### Matching Workflow

1. Students are placed into an active processing queue.
2. Each student applies to their next preferred course.
3. The course evaluates eligibility and capacity.
4. If necessary, the lowest-priority enrolled student is removed.
5. Evicted students continue applying to other preferences.
6. The process terminates when all students are either allocated or have exhausted their options.

---

## Build Instructions

### Requirements

- C++17 or later
- GCC / Clang

### Compile

```bash
g++ -std=c++17 -O3 -march=native high_performance_allocation_engine.cpp -o engine
