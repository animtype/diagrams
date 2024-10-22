# Updating Process for Tweakly.eu 3D Models

This document outlines the updating process for the Tweakly Angular application once the initial loading process is complete, detailing how the scene is initially drawn and how subsequent updates are applied.

---

## Part 1: Initial Draw

The initial drawing process begins once the Angular application is launched and the loading process has updated the parameters, as detailed in the "LOADING-PROCESS" document.

### Completion of Loading Process

Upon completion of the loading process, the `furnitures.furniture` JSON is fully prepared, allowing the drawing on the 3D scene to commence. The utilized JSON files include:

- **`furnitures.furniture`**: The 3D model to be rendered.
- **`parameters`**: Updated through the loading process, with all internal parameters evaluated and finalized.
- **`materials`**: Sourced from the `material_url`, prepared based on names for use in the 3D model.

These files also contain essential settings for rendering the scene, such as dimensions, lighting, and camera configurations, including aperture settings.

### Initial Draw Tasks

The initial draw sets up the following components:

- **Scene**: Establishes the three-dimensional space for model rendering.
- **Lighting**: Positions and configures lights within the scene to correctly illuminate the 3D model.
- **Camera**: Arranges the camera's position, angle, and parameters for optimal scene capture.
- **3D Model Rendering**: Draws the 3D model within the scene, utilizing updated parameters and materials to accurately reflect the model's intended appearance.

After the initial draw, the 3D model is presented in the scene with proper configurations, ready for user interaction or further updates.

---

## Part 2: Update Scene vs. Refresh Decision

The update process, triggered via `postMsg`, involves determining whether to execute an `UPDATE SCENE` or a `SCENE REFRESH`. This distinction is crucial, as it affects whether the 3D component is deleted and redrawn with new dimensions or simply refreshed with updated parameters.

### Update Scene

An `UPDATE SCENE` is required when significant parameters affecting the model's dimensions, such as `width`, `height`, `depth`, `shelf_thickness`, `side_thickness`, etc., are altered. This necessitates a re-evaluation of parameters and an update to the 3D JSON (furniture) with new dimensions.

### Refresh Material

A `REFRESH MATERIAL` occurs when parameters related to materials change, typically prefixed with `mat_selector_` and including other material-related keys. This refresh updates the materials applied to the model without altering its dimensions or necessitating a full scene redraw.

### Scene Refresh

A `SCENE REFRESH` is executed when parameters that do not affect the model's dimensions but may impact its visibility or presentation are altered, such as animation toggles, visibility settings, and aesthetic adjustments.

---

## Part 3: Criteria for Update Types

The decision for `UPDATE MODEL`, `REFRESH MATERIAL`, or `SCENE REFRESH` is based on the following criteria:

### Full Scene Update

Required for changes in dimensions or other fundamental properties, including:

- Alterations to `width`, `height`, `depth`, `shelf_thickness`, `side_thickness`, etc.
- Changes necessitating a complete re-evaluation and redraw of the 3D model.

### Refresh Material

Occurs when material-related parameters are updated, ensuring selected materials are refreshed in the scene without changing the model dimensions.

### Scene Refresh

Needed for updates to non-dimensional parameters like animation controls, visibility options, and camera settings, along with other aesthetic adjustments that do not require redrawing the 3D model.

---

## Part 4: Full Scene Update Process

### Step 1: "Before" Update Scene

Prior to the update, it is essential to preserve the current scene state:

- **Save Current Values**: All existing scene parameters and camera settings are saved to ensure they can be accurately restored post-update.
- **Remove 3D Model**: The current 3D model is removed from the scene to prepare for the updated model.

### Step 2: "Init" Update Scene

Setting up the new parameters and preparing the scene involves:

- **Overwrite Parameters**: Parameters from `postMsg` overwrite existing scene parameters.
- **Update Evaluations**: Parameters within the 3D furniture JSON are re-evaluated to reflect new dimensions and settings.
- **Update Materials**: Material settings are updated based on new parameters to ensure the model's appearance aligns with updated specifications.
- **Redraw 3D Model**: The 3D model is redrawn in the scene, incorporating all updates.

### Step 3: "After" Update Scene

After updating and redrawing the model, the final step is to restore the scene's original state:

- **Restore Parameters**: All parameters saved during the "before" step are reinstated, ensuring the scene returns to its prior state and maintaining the user's perspective and custom settings.

This process guarantees that significant changes to the 3D model are reflected in the scene without disrupting the user's interaction or visual context, ensuring a seamless and continuous user experience.

---

For more detailed information about the processes mentioned above, please refer to the respective process documentation:
- [ANGULAR-STRUCTURE.md](/docs/ANGULAR-STRUCTURE.md)
- [IFRAME-LOADING.md](/docs/IFRAME-LOADING.md)
- [LOADING-PROCESS.md](/docs/LOADING-PROCESS.md)
- [UPDATING-PROCESS.md](/docs/UPDATING-PROCESS.md)
- [MATERIALS.md](/docs/MATERIALS.md)
- [PARAMETERS.md](/docs/PARAMETERS.md)