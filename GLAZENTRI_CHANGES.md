# Glazentri / Zentravo adaptation of İstif

## Upstream and attribution

- Upstream project: [İstif](https://github.com/ceceys/istif), an open-source Windows truck and container load planner by Cuma Ali Dirik.
- Upstream revision used: [`347dc7ba656b41e851a3e35ba52252fbeb1b1c5d`](https://github.com/ceceys/istif/commit/347dc7ba656b41e851a3e35ba52252fbeb1b1c5d).
- Upstream licence: MIT, Copyright © 2026 Cuma Ali Dirik. Preserve the original `LICENSE` and copyright notice. Three.js is also MIT-licensed; retain its separate notice wherever bundled.
- Adaptation: **Zentravo by Glazentri**, integrated with [WinMatch](https://winquotes.com.au/), for construction, glazing and whole-of-home logistics.

This is a record of the changes made in the Glazentri implementation, not a claim that the original project lacked 3D loading, stacking constraints, mixed fleets, manual editing, load sequencing, PDF output, or undo/redo. Those capabilities originate in İstif. The browser integration is maintained separately from the upstream Windows application; the upstream desktop shell, updater, analytics and native file bridge have not been ported into WinMatch.

## Changes to upstream-derived JavaScript components

| Area | Glazentri change |
| --- | --- |
| Packing engine (`js/motor/motor.js`) | Check actual door width and height for each package orientation, independently of internal container dimensions. Validate fractional millimetre dimensions and placements without integer rounding while preserving the planner's default dimension handling. |
| Vehicle rendering (`js/gorunum3d/arac-modeli.js`) | Added trailer-only rendering, tray bodies, van bodies, tautliners and mezzanine vehicle visuals, axle metadata, and variable rear-axle rendering. |
| Scene adaptation | Expose cargo identifiers, category, packaging and locked state for the browser cargo workspace. Use standard npm Three.js addon imports instead of desktop-specific paths. |
| Texture typography (`js/gorunum3d/dokular.js`) | Adapted canvas label typography to the Glazentri interface with DM Sans and Space Mono. |

## New integration and optimisation features

- Browser-based cargo workspace with a bundled local packing worker and Three.js renderer. The worker runs in the browser; cargo is not sent to an external packing service. A top-view SVG fallback is available when WebGL is unavailable.
- Construction-specific cargo library, including upright windows and doors, crates, stillages, and other whole-of-home items. Every top-level physical package has a stable ID, outer dimensions, gross mass, supplier, consignment and handling constraints.
- Nested crate contents and source-opening references; contents-plus-tare mass calculation and explicit unknown weight handling. Unknown weights are not presented as zero.
- WinMatch project schedule integration: import missing openings without duplication, flag changed source dimensions for review, retain confirmed shipping dimensions and preserve manual placements. Added same-origin project-save bridge, JSON backup/restore and project IFC export.
- Door, wall, roof and rear-clearance validation; collision, orientation, payload, full support, rated top load and delivery-order checks. Upright glazing protection and conservative side-support checks for eligible light window stacking and restrained window packages.
- Auto-pack only unplaced items. Optimise preserves locked cargo and its supporting packages; compare candidate plans and keep the existing layout if the candidate is not better. Added bounded tiled-floor search for tightly packed floor-only layouts around locked packages, retaining exact physical measurements.
- Editable nominal shipping and truck envelopes, Australian vehicle references including LR/MR/HR descriptions and B-double combinations. Preserve fitting placements when equipment dimensions change and return non-fitting cargo to the unplaced list rather than losing it.
- Integrated truck delivery and multi-stop route planning. Reuse top-level shipment package IDs, assign consignments to sites, and avoid duplicate imports. Manual/forklift/combined unloading allowances; fuel, drive time and trip estimates separated from quoted carrier costs.
- Address-first route previews with optional user-entered road distance/time and advanced coordinate estimates; no mapping API key required. External previews share only the selected route addresses with the map provider.
- Cargo manifest, supplier-specific label branding, print-ready labels and load sheets, JSON/CSV and PNG exports; connected site-planning unloading order and handover workflow.
- Responsive browser interface, multiple views, shipment notes, loading checklist, undo/redo and project persistence. Original İstif functionality is credited rather than represented as newly invented.

## Validation performed

- 15 WinMatch cargo integration checks passed: mixed cargo round-trip, collisions, dimensional and door constraints, missing weights, rated stacking, crate contents, schedule synchronisation, manual placements, equipment resizing, fractional dimensions and import validation.
- Optimiser regression checks passed for imported glazing, braced windows, shared payload and locked/tiled floor layouts.
- Light window stacking and two-sided support checks passed.
- Upstream İstif engine test suite: **212 checks passed, zero failed** against the adapted implementation.
- Browser QA recorded in the integration README includes local save, grouping, placement, rotation, undo, IFC and mobile layout. GPU-specific 3D and loading-animation smoke testing still requires a WebGL-capable browser.

## Limits

This is a dimensional planning aid, not engineering or cargo-restraint certification. Vehicle dimensions and payloads are editable examples, not guarantees of booked equipment. The packing optimiser is heuristic with bounded search, not a proof of global optimum. Confirm crate ratings, restraints, lifting, actual openings, carrier rules and vehicle mass/axle compliance with the responsible professionals. A package fitting the door cross section does not certify a continuous insertion path.

## Suggested fork description

**İstif fork and browser cargo-planning adaptation for Zentravo by Glazentri — construction and glazing logistics, container/truck optimisation, packaging, route estimates and WinMatch integration.**

Keep the upstream README and licence intact. Add this file at the repository root as `GLAZENTRI_CHANGES.md`. It describes the actual implementation in WinMatch; the full WinMatch platform and its private services are not part of the upstream fork. Any code or assets subsequently published in the fork should be scoped and reviewed separately so the fork's contents accurately match its claims.
