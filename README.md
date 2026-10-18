# VoxelSieve plugin

Analyse industrial computed tomography (CT) scans with Claude on your own computer. The plugin
connects Claude to [VoxelSieve](https://github.com/yoshi5534/VoxelSieve), an open-source CT
analysis program built on OpenVDB, and adds skills for the common inspection tasks:

- **first-look**: size, voxel size, grey values and slices through a new scan
- **porosity-check**: pores and loosened microstructure, checked against the acceptance limits of
  an inspection order (BDG P 202 zones), with an inspection report
- **cad-comparison**: nominal-actual comparison of the scanned surface with the CAD model
- **first-article-inspection**: drawing characteristics measured on the scan with datums and
  tolerances, and the first article inspection report

VoxelSieve handles raw volumes, TIFF stacks, DICOM and gzipped XML projects, also scans of
hundreds of GB that do not fit in memory.

## What the plugin runs and where your data goes

The plugin starts one local MCP server, VoxelSieve's own program `vs-gui --mcp <scan directory>`,
over stdin/stdout. It contains no code of its own besides the skills in `skills/` and the server
entry in `.mcp.json`.

- Your scans never leave your computer. VoxelSieve reads them and writes projects, images and
  reports next to them. Claude receives only results: pore lists, measurements, slice images and
  report paths.
- VoxelSieve reads and writes only inside the scan directory you choose when you enable the
  plugin, and refuses every other path.
- VoxelSieve makes no network connections, needs no account and no API key, and sends no
  telemetry. Its time and memory statistics stay in the project directory.

## Install

1. Install VoxelSieve from the
   [latest release](https://github.com/yoshi5534/VoxelSieve/releases/latest): unpack
   `voxelsieve-<version>-<platform>.tar.gz` (Linux, macOS) or `.zip` (Windows), for example to
   `/opt/voxelsieve` or `C:\Tools\voxelsieve`. The
   [quickstart](https://github.com/yoshi5534/VoxelSieve/blob/main/docs/quickstart.md) has the
   details and sample data.
2. Install the plugin:
   - Claude Code: `/plugin marketplace add yoshi5534/voxelsieve-plugin`, then
     `/plugin install voxelsieve@voxelsieve`
   - Claude app: Customize > Plugins
3. When asked, choose the **scan directory**, and set **VoxelSieve program** to the full path of
   `bin/vs-gui` (`bin\vs-gui.exe` on Windows) unless it is on your PATH.

The plugin's server runs in Claude Code. Cowork and the Claude chat do not ask for the scan
directory yet, so there install VoxelSieve's `.mcpb` bundle from the release in Claude Desktop
instead (double-click it, then choose the scan directory).

## Try it

With the sample data from the release in your scan directory:

> Analyse the porosity of voxelsieve-samples/housing.raw with the inspection order next to it and
> tell me whether the part passes.

> Compare the scan with housing.stl and show me where it deviates by more than 0.1 mm.

> Take a first look at this TIFF stack: size, voxel size and three slices.

## License

Apache-2.0, like VoxelSieve. Issues and questions:
[github.com/yoshi5534/VoxelSieve/issues](https://github.com/yoshi5534/VoxelSieve/issues).
