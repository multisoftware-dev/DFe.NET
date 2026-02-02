# NuGet-MultiCTe

This folder is an **overlay** for publishing DFe.NET packages to an internal feed
with a **PackageId prefix** (default: `MultiCTe.`), without modifying the upstream
`NuGet/` nuspec files.

## How it works

- Source nuspecs live in `NuGet/**.nuspec` (from upstream).
- This overlay is generated into `NuGet-MultiCTe/**.nuspec`.
- The generator:
  - prefixes each `<id>` with `MultiCTe.` (or whatever prefix you choose)
  - rewrites nuspec `<dependency id="...">` entries for any package that is also
    part of the same set (so internal dependency graphs stay consistent)

## Generate / refresh

From the repo root (PowerShell):

```powershell
pwsh -File .\tools\generate-multicte-nuspecs.ps1 -Prefix "MultiCTe."
```

Commit the generated `NuGet-MultiCTe/**.nuspec` files.

## Notes

- This does **not** change upstream sources; it only creates additional files.
- If upstream adds/removes packages (nuspecs), rerun the generator and commit the new output.
