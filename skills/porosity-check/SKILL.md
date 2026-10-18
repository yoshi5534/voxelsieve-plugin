---
description: Porosity inspection of a cast or printed part from an industrial CT scan with VoxelSieve, against the acceptance limits of an inspection order (BDG P 202 zones), with an inspection report. Use when someone asks for pores, voids, shrinkage, gas porosity or loosened microstructure in a CT scan, or whether a part passes.
---

# Porosity check

VoxelSieve runs locally and only reads and writes inside `${user_config.scan_dir}`.

1. Open or create the project (next to the scan if the user names none) and import the scan as
   in the first-look skill. Use `background: true` and `wait` for large scans.
2. Run `run_porosity`. Summarise the result from its output: number of pores, largest pore with
   its volume and position, porosity in percent, and zones of loosened microstructure.
3. Show the worst region with `view_slice` through the largest pore; pores are drawn in red,
   loosened zones in yellow.
4. If the user has an inspection order (JSON with the acceptance limits per zone), run
   `run_report` with it as `order_path`. For each acceptance limit, state whether it is met and
   quote the values from the report.
5. Give the path of `report.html` in the project directory.

Rules:
- Quote numbers from VoxelSieve's results, never estimate them.
- The report from VoxelSieve is the result; your summary only points to it.
- Without an inspection order there are no limits: report the findings and do not call the part
  good or bad.
