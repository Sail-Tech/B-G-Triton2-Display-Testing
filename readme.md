# Triton² HTML Canvas Visual Simulator

An experimental recreation of a marine-style multifunction display, built as a single HTML file with Canvas rendering and demonstration data. It includes wind, depth, navigation, tide, and simulated autopilot-status views.

> [!WARNING]
> **For visual demonstration and development only.** This is not a navigation instrument. Pls testing with NMEA 2000 network data, and it does not send commands to an autopilot. All displayed values are simulated. Do not use it to make navigation or safety decisions.

## Documented version

`v14.3.1` — entry file: [`triton2_views_integrated_v14_3_1.html`](./triton2_views_integrated_v14_3_1.html).

## Features

- Responsive HTML Canvas display with menus and navigation between views.
- View library including **Autopilot Status, SailSteer, Wind Mode, Highway, Laylines, Wind Plot, Tide, Weather, Depth History, Steering Reference, True Wind Speed, Depth, and SOG**, along with other reference views included in the HTML. Not all views are active at the same time.
- Eight active pages in the main navigation. Other views can be opened from the view library. The simulator's JavaScript API can change the active-page selection.
- Shared graphical elements across panels, including the autopilot semicircular wheel, port/starboard triangles, and the Canvas boat used in Highway and Steering Reference.
- An internal demonstration-data model organised around `pgn...` identifiers, with associated panels updating from the simulated values. **These identifiers do not implement an NMEA 2000 connection.**
- *Wind Mode* with `Auto`, `Apparent`, and `True` references. In `Auto`, the visual reference is AWA when the true wind angle is below 70° and TWA from 70° upwards.
- Visual warnings for simulated unavailability of wind, depth, tide, heading, waypoint, and H5000 data.
- Built-in consistency checks accessible from the browser console.

## Getting started

1. Place the HTML file listed above in the same directory as this `README.md`.
2. Open the `.html` file in a browser that supports Canvas and JavaScript. No dependencies or local server are required for local use.
3. Navigate between panels using the controls drawn on the display, the menu, or drag gestures on a compatible device.
4. Select **Dados DEMO ↗** to open the demonstration controls in a separate window. If the browser blocks the pop-up, the controls appear in an on-page dialog instead.
5. In the demonstration window, select **Vento** (wind), **Profundidade** (depth), **Maré** (tide), **Rumo** (heading), **Waypoint**, or **H5000** to show the corresponding unavailable-data state. Select **Normal** to restore valid simulated-data states.

**Note:** The current version starts in the **wind unavailable** scenario. Select **Normal** to view the available simulated data. Opening a separate window may depend on your browser's pop-up settings. The button labels above are reproduced as they appear in the current interface.

## Developer console

The following calls operate only on the simulator's local state:

```js
// Run built-in consistency checks.
tritonDisplay.runSelfTests();

// Inspect available views and active pages.
tritonDisplay.views.listLibrary();
tritonDisplay.menu.getState().pages;

// Show an unavailable-data scenario, then restore normal status.
tritonUnavailableDemo.show('depth');
tritonUnavailableDemo.show('normal');

// Inspect the simulated wind state.
tritonDisplay.windMode.getState();
```

To select the eight active pages, pass `setActivePages` a list of **eight distinct identifiers** returned by `listLibrary()`. This configuration is held in memory for the current session; it is not a persistent setting.

## Suggested repository structure

```text
.
├── README.md
└── triton2_views_integrated_v14_3_1_controlos_demo_janela_separada.html
```

If you publish newer files, update the implementation filename and version in this README. Before including screenshots or pages from third-party manuals, check that you have the necessary rights.

## References and attribution

This project is an **independent interface recreation** inspired by Triton² equipment. For information about the actual product, consult the [Triton² manuals provided by B&G](https://ww2.bandg.com/downloads-category/triton2-autopilots-manuals/). The manufacturer's official documentation should not be confused with this project's simulated values or implementation logic.

Triton² and B&G are names belonging to their respective owners. This reference does not imply affiliation, certification, or endorsement by the manufacturer.

## License and publication

**No license has been specified for this project yet.** Before making the repository public, confirm that you have the right to publish the code and any included assets, then add a `LICENSE` file with your chosen license. Do not automatically apply that license to third-party material.

## Contributions and version control

- Assign an identifiable version to each change and record what was modified.
- Preserve validated views and components, including Laylines, the Depth panel pointer, and the geometry of the shared wheel.
- Check navigation, unavailable-data states, control limits, and visual regressions before accepting changes.
- Clearly distinguish behaviour confirmed by the manual from design choices made for the simulator.
