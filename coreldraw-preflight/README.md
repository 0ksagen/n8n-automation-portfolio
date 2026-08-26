# CorelDRAW Laser Preflight Automation

A production-oriented automation project created to improve the preparation and validation of CorelDRAW files before laser cutting.

Unlike my n8n portfolio projects, this automation was created around a real manufacturing workflow and is used to reduce repetitive manual checks before production.

## Problem

Before sending acrylic layouts to a laser-cutting machine, CorelDRAW files need to be checked for geometry problems.

Typical issues include:

- open contours;
- self-intersections;
- objects positioned too close to each other;
- difficult-to-find problem areas inside large layouts.

Manual inspection can be slow, especially when a production file contains many objects.

The goal of the project was to make these checks faster and easier for the machine operator.

## Solution

I worked on a custom CorelDRAW preflight utility that communicates with CorelDRAW and analyses selected production objects.

The utility helps the operator:

1. Select production objects.
2. Start a preflight check.
3. Detect potential geometry problems.
4. Place visual markers near detected issues.
5. Navigate between problems.
6. Correct the layout.
7. Clear service markers after checking.

## Main Features

### Open Contour Detection

The utility analyses curve subpaths and identifies paths that are not closed.

Conceptually:

```text
Selected Object
      ↓
Analyse Curve
      ↓
Inspect SubPaths
      ↓
Closed?
   ├── YES → OK
   └── NO  → Mark endpoints
```

Open contour endpoints are marked so the operator can quickly locate and repair them.

### Self-Intersection Detection

The tool also checks curves for self-intersections.

When a problem is found:

- the problematic object is recorded;
- a visual marker is created;
- the operator can navigate to the detected issue.

### Visual Problem Markers

Instead of only displaying an error count, the utility creates visual markers directly around detected problem locations.

This makes it much easier to find errors inside complex layouts.

### Problem Navigation

The interface supports navigation between detected issues.

Example workflow:

```text
Problem 1
   ↓
Next
   ↓
Problem 2
   ↓
Next
   ↓
Problem 3
```

The goal is to avoid manually searching through a large CorelDRAW page.

### Marker Management

Generated service markers can be removed after checking so they do not become part of the production file.

## External Utility Interface

The project also includes a separate HTA/JScript interface that communicates with CorelDRAW through Windows COM / ActiveX.

Conceptually:

```text
HTA Interface
      ↓
ActiveX / COM
      ↓
CorelDRAW
      ↓
VBA Macro
      ↓
Geometry Analysis
```

This allows production checks to be launched from a compact external interface.

## Technologies Used

- VBA
- CorelDRAW 2019
- CorelDRAW Object Model
- JScript
- HTA
- Windows COM
- ActiveX

## Production Optimization

The project was not limited to software.

I also improved the physical laser workflow by adding a repeatable mechanical reference point that helps align the laser with the zero position.

Previously, the laser position had to be manually adjusted relative to each acrylic sheet.

The physical reference reduced repetitive alignment work and made the process more consistent.

This reflects the same approach as the software project:

> identify a repetitive process → understand the cause → create a practical improvement.

## Development Approach

The utility was improved iteratively using real production files.

The process included:

```text
Real production problem
        ↓
Analyse operator workflow
        ↓
Implement improvement
        ↓
Test on CorelDRAW files
        ↓
Find edge cases
        ↓
Refine
```

Testing included heavier files and grouped objects to identify performance and usability problems.

## Skills Demonstrated

This project demonstrates experience with:

- analysing real production problems;
- workflow optimization;
- VBA automation;
- desktop software integration;
- geometry processing;
- debugging;
- Windows COM interaction;
- iterative testing;
- operator-focused UI design.

## Future Improvements

Possible future development includes:

- faster geometry scanning;
- checking only relevant outer contours when appropriate;
- reducing unnecessary geometry inspection;
- improved grouped-object handling;
- area calculation;
- perimeter calculation;
- material cost calculation;
- additional laser-production validation tools.

## Project Context

This automation was created as part of my work with CNC and laser-cutting production.

The main objective was not to build a programming demo, but to solve an actual production problem and reduce repetitive work.
