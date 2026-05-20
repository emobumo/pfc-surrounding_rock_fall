# AGENTS.md

## Project Purpose

This repository stores a PFC2D 6.0 and FLAC2D wall-zone coupled simulation project for underground stope caving and surrounding rock collapse.

The project aims to simulate the mechanical response, collapse, and stress redistribution after underground stope excavation.

## Modeling Framework

The model uses:

- PFC2D 6.0 for the discrete particle region;
- FLAC2D zones for the far-field continuum region;
- wall-zone coupling to connect the PFC particle region and the FLAC zone region.

The PFC region includes both the orebody and the near-field surrounding rock. The FLAC zone region wraps around the PFC region and represents far-field rock mass.

## Current Research Stage

The current task is to first establish a complete and runnable workflow. The model may initially be simplified as:

- one rock type;
- rectangular stope;
- particle deletion to represent excavation;
- unchanged FLAC constitutive model;
- contact model borrowed from a local reference case after converting from PFC5.0 to PFC2D 6.0.

After the workflow is verified, the model may be expanded to:

- inclined stope geometry imported from DXF;
- multiple DXF regions for different rock types;
- particle grouping and parameter assignment for different geological domains.

## Key Original Version

The original version has already been verified to run. Its most important parts are:

1. the PFC-zone coupling workflow;
2. the automatic state-saving logic after excavation.

However, the original version does not adequately restore the in-situ stress state of the PFC particle region. As a result, upper particles may separate from the coupling wall in later stages. The PFC modeling workflow therefore needs reconstruction.

## Reconstruction Goal

The reconstruction should preserve the validated coupling and state-saving logic, while rebuilding the PFC initialization process.

The reconstructed PFC workflow should include:

1. particle generation;
2. preliminary particle compaction;
3. particle grouping and parameter assignment;
4. contact model installation and bonding;
5. in-situ stress recovery using servo walls;
6. coupling boundary and FLAC zone region re-creation;
7. excavation by deleting stope particles;
8. later result output and automatic saving.

## Important Instructions for AI Assistants

When modifying or reviewing this repository:

- Do not overwrite the original coupled version unless explicitly requested.
- Treat the original version as a baseline reference.
- Keep PFC5.0 and PFC2D 6.0 syntax differences explicit.
- Convert PFC5.0 syntax carefully before applying reference code.
- Do not assume the local reference case has been successfully run.
- Preserve the validated wall-zone coupling idea unless there is a clear reason to change it.
- Preserve the automatic saving idea after excavation.
- Prefer small, verifiable changes over large refactoring.
- Explain the physical meaning of each modeling step, not only the code syntax.
- Be especially careful with PFC region size, coupling wall position, and FLAC zone geometry alignment.

## Preferred Change Workflow

1. Understand the current file and its role.
2. Identify whether it belongs to the original version, current version, or archive.
3. Make the smallest necessary modification.
4. Explain how the change affects the modeling workflow.
5. Provide a verification suggestion.
6. Update the corresponding Markdown documentation if the workflow or parameter meaning changes.
