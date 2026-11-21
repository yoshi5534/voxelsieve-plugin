---
description: Porosity inspection of a cast or printed part from an industrial CT scan with VoxelSieve, against the acceptance limits of an inspection order (BDG P 202 zones or BDG P 203 porosity keys in freely defined regions), with an inspection report. Use when someone asks for pores, voids, shrinkage, gas porosity or loosened microstructure in a CT scan, or whether a part passes.
---

# Porosity check

VoxelSieve runs locally and only reads and writes inside `${user_config.scan_dir}`.

1. Open or create the project (next to the scan if the user names none) and import the scan as
   in the first-look skill. Use `background: true` and `wait` for large scans.
2. If the slices show beam hardening (material darker towards the middle, dark streaks between
   thick regions), run `run_beam_hardening` first and say so; the later steps use the corrected
   dataset. Strong noise can be reduced with `run_denoise`.
3. Run `run_porosity`. Summarise the result from its output: number of pores, largest pore with
   its volume and position, porosity in percent, and zones of loosened microstructure.
4. Show the worst region with `view_slice` through the largest pore; pores are drawn in red,
   loosened zones in yellow.
5. If the user has an inspection order (JSON with the acceptance limits per zone), check its
   regions first with `run_inspection_regions` and a `view_slice` or `view_objects`: a zone in
   the wrong place makes the whole evaluation wrong. A zone is rated either in the scheme of
   BDG P 202 (largest pore, pore count, porosity) or of BDG P 203 (`porosity_key` as written on
   the drawing, such as `PROI2/Øaq3/da3/UØaq1`). Then run `run_report` with the order as
   `order_path`. For each acceptance limit, state whether it is met and quote the values from
   the report.
6. Give the path of `report.html` in the project directory.

Rules:
- Quote numbers from VoxelSieve's results, never estimate them.
- The report from VoxelSieve is the result; your summary only points to it.
- Without an inspection order there are no limits: report the findings and do not call the part
  good or bad.
- Never invent a porosity key or region. If the drawing gives one only in words, write the order
  with the user and show them the regions before the report.
- `run_inspection_regions`, `run_beam_hardening` and P 203 keys need a current VoxelSieve
  release; if a tool is missing, ask the user to update VoxelSieve.
