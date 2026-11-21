---
description: Analysis of a fibre-reinforced composite (CFRP, GFRP, short-fibre plastic) from an industrial CT scan with VoxelSieve - materials, fibre directions and fibre families, porosity in the matrix, with a report. Use when someone asks about fibre orientation, ply directions, fabric, fibre content or voids in a composite part.
---

# Fibre composites

VoxelSieve runs locally and only reads and writes inside `${user_config.scan_dir}`.

1. Open or create the project and import the scan as in the first-look skill. Noisy scans of fine
   fibres gain much from `run_denoise` before the next steps.
2. Look at the histogram with `histogram` and run `run_segment_materials` (`materials: 0` takes
   the number of classes the histogram suggests, typically matrix and fibre bundles). Check the
   classes with `view_slice` before going on.
3. Run `run_fibre_orientation`. Summarise the fibre families (warp and weft of a fabric, the
   plies of a laminate) with their direction and share, quoting the output, and show the slices
   coloured by direction.
4. For voids in the matrix, run `run_porosity`; with a segmentation it reports per material.
5. With an order that has `fibres` requirements (direction tolerance, share), run `run_report`
   with it as `order_path` and state for each requirement whether it is met.

Rules:
- Quote numbers from VoxelSieve's results, never estimate them.
- The structure tensor gives directions of bundles or fibres at the block size used; say which
  block size you used and do not claim single-fibre detail below the voxel size.
