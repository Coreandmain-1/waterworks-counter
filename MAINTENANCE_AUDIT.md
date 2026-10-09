# Waterworks Counter — maintenance audit (ASSEMBLY-51)

## Preserved
- Existing iPhone Shortcut URL contract: `?q=<encoded speech>`.
- Single-file app entry point `index.html` and GitHub Pages deployment.
- Ford, Fernco, HARCO, Inserta Tee, EBAA, Star Pipe, and MJ lookups.
- Existing manufacturer model candidates and assembly quantities.

## Corrected
1. Dictation: `M8 inch` is normalized to `8 inch` before nominal-size extraction.
2. Dictation: `MJT` is normalized to `MJ tee`.
3. Pipe aliases: C 9 0 0 and MEGA LUG forms are normalized.
4. Standalone EBAA/STARGRIP with `MJ` no longer automatically enters the generic MJ assembly path unless an actual fitting is present.
5. Repaired double-escaped regex in IPS/SDR identification and accessory-package detection.
6. Preserved priority for a dimension followed by `inch` over DR18 material dimension ratio.
7. Added `tests/smoke.html` with repeatable browser checks.

## Known limitations — DO NOT treat as a ready-to-order bill of material
- MJ fitting part numbers are not yet verified.
- MJ bolt counts and dimensions are reference values; verify against manufacturer schedules.
- Whether EBAA/Star restraint packages include gaskets or bolts is not fully documented in app.
- The app assumes each indicated MJ fitting end is a distinct connection. Direct fitting-to-fitting connections may change required components.
- Mixed IPS/CIOD end allocations remain sensitive to natural-language phrasing.
- Fernco catalog part numbers require outside-diameter, material, and application confirmation. Some catalog combinations have not been independently checked.
- Regression checks validate app behavior only, **not** manufacturer data accuracy.
- Browser test suite is new and needs to be run on a live deployment. Do not claim automated test success without seeing the test report.

## Release procedure
1. Save code to GitHub; confirm commit SHA.
2. Open `/tests/smoke.html` and inspect all scenarios.
3. Resolve every FAIL and rerun the entire suite.
4. Test a real iPhone Shortcut request, including `M8 inch MJT` and `MJ tee + elbow`.
5. Verify source manufacturer catalogs before marking any component order-ready.
6. Keep the Shortcut unchanged unless the URL contract itself is proven broken.

## Future engineering work
- Separate parsing, catalog data, assembly calculation, and rendering into independently tested modules.
- Use structured objects for fittings, joint counts, restraints, and gasket/bolt requirements instead of parsing formatted prose.
- Add per-end pipe-material allocation and a confidence/verification status to every line item.
- Implement CI checks so a regression fails before deployment.
