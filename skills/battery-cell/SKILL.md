---
description: Inspection of a lithium-ion battery cell from an industrial CT scan or section images with VoxelSieve - housing, electrode layers, anode overhang, foreign particles and gas voids, with a report against the cell specification. Use when someone has a CT scan of a cylindrical (18650, 21700, 4680), pouch or prismatic cell and asks about overhang, layers, particles, voids or whether the cell meets its specification.
---

# Battery cell inspection

VoxelSieve runs locally and only reads and writes inside `${user_config.scan_dir}`.

1. Open or create the project. A volume is imported as in the first-look skill. Section images
   (a folder or ZIP with `axial_images/` and `radial_images/` per cell) need no import: use
   `run_battery_images` instead of step 2.
2. Run `run_battery_inspection`. `cell_type` is `auto`, `cylindrical` or `stacked`; the cell axis or
   stack normal must lie along a volume axis (`axis`, default `auto`).
3. Summarise from its output: outer size and roundness, wall thickness of the can, number of
   cathode and anode layers, the smallest anode overhang per edge, gaps between layers, foreign
   particles and gas voids with their sizes and positions. Show the section with the smallest
   overhang with `view_slice`.
4. With a cell specification, write it as the `battery` section of an order (limits such as
   `min_overhang_mm`, `cathode_layers`, `max_particle_size_mm`, `max_voids`) and run
   `run_battery_report` with it as `order_path`. For each requirement, state whether it is met and
   quote the report.
5. Give the path of `report.html` in the project directory.

Rules:
- Quote numbers from VoxelSieve's results, never estimate them.
- Never invent limits. Typical values from the literature (an overhang of at least 0.1 mm) are
  only a hint; the cell's own specification decides.
- Voids at the ends of the electrode strips can be part of the design; mention them, but leave
  the judgement to the user.
