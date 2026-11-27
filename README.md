[README.md](https://github.com/user-attachments/files/35511138/README.md)
# Zentravo by Glazentri

**Browser-based 3D container and truck load planning for construction and glazing.** Zentravo is Glazentri’s modified build of İstif, the open-source load planner created by Cuma Ali Dirik. [Original İstif project](https://github.com/ceceys/istif)

Plan how windows, doors, crates, stillages and other building materials will fit from container to truck to site. Choose a vehicle or enter its dimensions, add your cargo, then auto-pack it or arrange it by hand. Review the load in 3D, play through the loading sequence, and prepare a manifest and labels for dispatch.

## What Glazentri changed

| Area | Glazentri adaptation |
| --- | --- |
| Browser app | Runs in a browser without a Windows installer. The standalone planner saves drafts in browser storage and runs its packing calculations locally. |
| Glazing and construction cargo | Model upright windows and doors, timber crates and A-frame stillages. Group items inside crates, track each package by supplier and consignment, and calculate gross mass from the contents and packaging. |
| Door fit and packing | Check package width and height against the actual door opening as well as the internal space. Auto-pack adds unplaced cargo to the plan. Optimisation preserves locked packages and the packages supporting them. |
| Australian vehicle options | Use editable container and truck dimensions, with Australian vehicle references and options for tautliners, tray trucks, mezzanines and B-double combinations. |
| Truck delivery and handling | Reuse cargo from the container plan for multi-stop site deliveries. Estimate trips, travel time, fuel and unloading costs for manual handling, forklift unloading or a combination. |
| Dispatch documents | Print cargo labels with supplier branding and generate load sheets. Export the manifest as CSV or save the plan as a JSON backup. |

The original İstif project provides the packing engine, interactive 3D view, step-by-step loading and manual placement tools that Zentravo builds on. [Glazentri change log](GLAZENTRI_CHANGES.md)

## Run the standalone planner

From the repository root, start a local web server with Python 3.

```sh
python3 -m http.server 8080 --directory public
```

Open [http://localhost:8080/container-studio/](http://localhost:8080/container-studio/). The bundled build runs without a backend or API credentials. If WebGL is unavailable, the planner provides a 2D top view.

To rebuild from source, run `npm install` and `npm run build`. Run `npm test` for the engine and integration checks.

## WinMatch integration

Inside WinMatch, Zentravo can pull windows and doors from a project schedule, flag source dimensions that have changed, and retain confirmed shipping dimensions and manual placements. Schedule import, project saving and IFC export require the WinMatch host. [WinMatch](https://winquotes.com.au/)

## Credits and licence

Adapted for Zentravo by **Glazentri**. The original İstif components are copyright © 2026 **Cuma Ali Dirik** and retain their MIT licence. [Original İstif source](https://github.com/ceceys/istif) · [İstif licence notice](LICENSE-ISTIF.txt)
