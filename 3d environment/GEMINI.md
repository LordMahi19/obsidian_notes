# Gemini Project Context: Lightweight, Primitive-based 3D Scene Reconstruction for Robotics

## Directory Overview

This directory serves as the planning and documentation hub for a bachelor thesis focused on **lightweight, primitive-based 3D scene reconstruction for robotics**. The project's goal is to build a prototype system that uses a single camera to create a simplified, live 3D model of its environment, represented by geometric primitives (planes, cuboids). This model is intended for real-time navigation by robots, particularly those trained in 3D simulated environments.

## Key Files

*   `thesis.md`: The formal thesis proposal, detailing the plan to build and evaluate the primitive-based 3D reconstruction system.
*   `research_ideas.md`: A document that captures the evolution of the project idea, from initial concepts to the current goal of primitive-based 3D reconstruction.
*   `new plan.md`: The current step-by-step action plan for the software implementation of the primitive-based 3D reconstruction system.
*   `plan.md`: (Outdated) The previous action plan for the 2.5D mapping system.

## Implementation Progress

The project has pivoted from a 2.5D mapping approach to a lightweight, primitive-based 3D scene reconstruction. Implementation will now follow the plan outlined in `new plan.md`. Previous work on Visual Odometry and Object Detection will be adapted and integrated into the new pipeline, alongside new components such as monocular depth estimation, plane detection, and 3D cuboid fitting.

## Usage

This directory is for managing the research and documentation aspects of the thesis.

*   Refer to `thesis.md` for the formal structure and research questions.
*   Use `new plan.md` as the primary coding and implementation guide.