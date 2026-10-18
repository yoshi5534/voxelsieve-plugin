---
description: Nominal-actual comparison of an industrial CT scan with its CAD model (STL) in VoxelSieve - surface extraction, alignment and deviation map. Use when someone wants to know where a scanned part deviates from its design, by how much, or whether it is within a form tolerance.
---

# Comparison with the CAD model

VoxelSieve runs locally and only reads and writes inside `${user_config.scan_dir}`; the STL must
be there too.

1. Open or create the project and import the scan as in the first-look skill.
2. Extract the surface with `run_surface`.
3. Run `run_compare_cad` with `cad_path` set to the STL (in mm) and `tolerance_mm` set to the
   tolerance the user gave. It aligns the scan to the model by best fit.
4. Check the alignment with `view_objects` before reporting deviations; a poor alignment makes
   every deviation wrong.
5. Report the share of the surface within the tolerance the user gave, the largest positive and
   negative deviations and where they are, quoting the numbers of the comparison step.

For flexible parts (thin walls, rubber, sheet metal), `non_rigid: true` lets the comparison allow
for deformation; say when you used it, since it hides part of the deviation.
