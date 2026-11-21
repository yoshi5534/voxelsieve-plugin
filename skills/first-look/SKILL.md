---
description: A first look at an industrial CT scan with VoxelSieve - size, voxel size, grey values and slices through the part. Use when someone opens a new CT volume (raw, TIFF stack, DICOM, .vsieve) and wants to know what is in it before choosing an analysis.
---

# First look at a CT scan

VoxelSieve runs on the user's computer and only sees files inside the scan directory set for
this plugin (`${user_config.scan_dir}`). Paths outside it are refused; ask for a path inside it.

1. Open the project the user names with `project_open`, or create one next to the scan with
   `project_create`. Keep projects inside the scan directory.
2. Import the scan with the operation that fits the input:
   - raw volume with a JSON sidecar: `run_import_raw`
   - TIFF stack, also inside a ZIP: `run_import_tiff`
   - DICOM slices: `run_import_dicom`
   - gzipped XML project of a CT system: `run_import_gzipped_xml`
   - an existing VoxelSieve dataset (`.vsieve`): `run_open_dataset`
   The import shows a preview first. Scans of tens or hundreds of GB take minutes: start the
   import with `background: true`, follow it with `wait`, and tell the user the progress. If the
   user wants to stop, call `cancel`.
3. Report dimensions, voxel size (it can differ per axis) and memory use from `dataset_info`, and
   the grey value distribution from `histogram`, including the suggested number of materials.
4. Show the middle slices along z, y and x with `view_slice`. Describe the part, visible voids,
   and artefacts such as rings, streaks or beam hardening. Say what you see, do not guess sizes.
5. Suggest which analysis fits next: porosity check, wall thickness, comparison with the CAD
   model, material segmentation, fibre orientation of a composite, battery cell inspection or
   first article inspection. If you saw beam hardening or strong noise, suggest correcting it
   first with `run_beam_hardening` or `run_denoise`; both write a new dataset and keep the scan.
