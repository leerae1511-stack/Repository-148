# Tool Pocket Generator V148

## Provenance
- Built directly from `Tool_Pocket_Generator_V147_FINAL.zip`.
- V147 was the tested-in-Safari build supplied by the user for this geometry-check investigation.
- V139 remains the known-working historical baseline; this release does not replace that record.

## Problem addressed
On JSON import, the imported Length × Width values can represent the orange workspace rectangle until the user deliberately establishes final dimensions from the confirmed physical photo grid. V147's `finish()` could prefer stored `projectFinalDims` values over the actual sampled outline envelope, allowing stale imported rectangle dimensions to be treated as final profile dimensions.

## Change in V148
- `finish()` now requires `dimensionsSetFromGrid` to be true before closing.
- When closing, it derives the final Length × Width from `physicalOutlineMm()` and its sampled profile envelope, rather than preferring imported `projectFinalDims`.
- The orange workspace rectangle remains a separate workspace value.
- No changes were made to Curve/Straight point modes, curve sampling, drawing, point dragging, point positions, or the profile geometry algorithms.

## Process / order
1. Import JSON or create a tool.
2. Confirm the physical grid in the photograph.
3. Detect/edit the outline as required.
4. Confirm profile editing.
5. Set dimensions from the confirmed physical photo grid.
6. Close profile.
7. Run Geometry Check and export if it passes.

## What was not changed
- Curve and Straight dot behaviour and their existing V147 rendering/sampling implementation.
- Point drag handling or point coordinates.
- Geometry Check's self-intersection and clearance algorithms.
- STL triangulation/export behavior, tray settings, and unrelated UI.

## Verification
- ZIP archive integrity checked.
- HTML JavaScript syntax checked with Node.js.
- Source-diff scope checked: V147 curve sampling and draw/drag code are unchanged.
- Static workflow check: closing is blocked until dimensions are set from the confirmed physical grid; final dimensions are then measured from the sampled physical outline.

## Important test limitation
This release has not been run through Safari's full interactive workflow or against the user's actual imported JSON/photo in this build environment. Therefore V148 is a targeted candidate fix, not yet user-validated. Please verify the imported rectangle remains unchanged until the physical-grid dimension step, then confirm the final envelope matches the physical-grid measurement and that V147's dot-on-profile behavior remains intact.
