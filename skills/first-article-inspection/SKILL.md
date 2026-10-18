---
description: First article inspection of a part from an industrial CT scan against its drawing in VoxelSieve - characteristics measured on the scan with datums and tolerances, and the first article inspection report. Use when someone needs a first article inspection (FAI, initial sample report), dimensional measurement of drawing characteristics, or a ballooned report from a CT scan.
---

# First article inspection

VoxelSieve runs locally and only reads and writes inside `${user_config.scan_dir}`.

Inputs: the scan, the CAD model as STL in the coordinates of the drawing, and the characteristics
of the drawing (an inspection plan as JSON, or the characteristics in words). Order data
(supplier, customer, part, drawing revision, reason) is optional.

1. Open or create the project, import the scan as in the first-look skill and extract the surface
   with `run_surface`.
2. Align the CAD model to the scan with `run_compare_cad` and check it with `view_objects`.
3. If there is no inspection plan, or only characteristics in words, call `cad_features` on the
   STL and build the plan as described in `run_measure_dimensions`: one element per feature with
   its `at` point, the datums of the drawing in order (`alignment.datums`), and each
   characteristic with its balloon number, nominal value and tolerance.
4. Run `run_measure_dimensions` with the plan. For elements that could not be measured, fix their
   `at` point or `search_mm` and measure again.
5. Run `run_first_article_report` with the order data; list the fields the report says are
   missing so the user can fill them in.
6. Summarise the decision and every characteristic out of tolerance with nominal, actual value
   and deviation, quoting the measurement.

Rules:
- Never invent a tolerance. Leave characteristics without one unrated and say so.
- The report from VoxelSieve is the result; the final approval belongs to the customer.
