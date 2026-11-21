---
description: Wall thickness analysis of a part from an industrial CT scan with VoxelSieve - thickness at every point of the surface, thin and thick regions, the local thickness map of the volume and the deviation from the nominal thickness of the CAD model. Use when someone asks for wall thickness, minimum wall, thin walls, material accumulations or whether walls meet a drawing limit.
---

# Wall thickness

VoxelSieve runs locally and only reads and writes inside `${user_config.scan_dir}`.

1. Open or create the project and import the scan as in the first-look skill.
2. Run `run_wall_thickness` with the limits the user gave as `min_wall_mm` and `max_wall_mm`.
   Choose the method:
   - `ray` (default): sub-voxel accurate for walls with roughly parallel faces, such as housings
     and sheet-like parts.
   - `sphere`: the largest inscribed sphere, also in corners, at ribs and in solid sections.
   Pores make a wall thinner; say so when the porosity result shows pores in a thin region.
3. Add `volume_map: true` when the user wants material accumulations (hot spots of a casting)
   or walls inside the part; the slice view then colours the material by thickness.
4. With a CAD model: compare it first as in the cad-comparison skill, then run
   `run_wall_thickness` with `nominal_thickness: true` and `nominal_tolerance_mm` to get the
   deviation of the actual from the nominal thickness.
5. Report the smallest and largest thickness, the area below `min_wall_mm` and where the thin
   regions are, quoting the step's output, and show them with `view_objects`.
6. An inspection order with a `wall_thickness` section (`min_mm`, `max_area_below_min_mm2`) is
   evaluated by `run_report` with the order as `order_path`, together with the porosity.

Rules:
- Quote numbers from VoxelSieve's results, never estimate them.
- Without limits from the user or an order, report the values and do not call the part good or
  bad.
