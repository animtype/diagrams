# Parameters Overview for Tweakly.eu 3D Models

This document provides a comprehensive overview of the parameters used in the Tweakly.eu application, synthesizing information from other documents and adding additional useful parameters. These parameters help define the 3D scene, camera behavior, model dimensions, and various interactive settings.

---

## Summary of Parameters

Parameters are essential for configuring the 3D scene and models in the Tweakly.eu application. They control everything from model dimensions to camera settings and visual effects. Below, we provide an overview of the most commonly used parameters, including their explanations and default values where applicable.

### Useful Parameters

- **`scene_height`**: Defines the height of the 3D scene (e.g., `600` pixels).

- **`scene_width`**: Defines the width of the 3D scene (e.g., `600` pixels).

- **`width`**: The width of the furniture model (e.g., `1400` mm).

- **`depth`**: The depth of the furniture model (e.g., `900` mm).

- **`height`**: The height of the furniture model (e.g., `750` mm).

- **`base_height`**: The base height of the furniture (e.g., `750` mm).

- **`allow_camera_zoom`**: Enables or disables zooming capability for the camera (`true` or `false`).

- **`allow_camera_rotate`**: Enables or disables the ability to rotate the camera (`true` or `false`).

- **`allow_camera_pan`**: Enables or disables the ability to pan the camera (`true` or `false`).

- **`scene_viewport`**: Determines the type of view for the scene. Options include `'perspective'` or `'top'` (e.g., `'perspective'`).

- **`show_wireframe`**: Toggles whether the model should be displayed in wireframe mode (`true` or `false`).

- **`show_measurement`**: Displays measurements for various model dimensions (`true` or `false`).

- **`button_measurement`**: Displays a button that allows users to toggle measurement visibility (`true` or `false`).

- **`button_toggle_animation`**: Shows a button that allows users to start or stop animations (`true` or `false`).

- **`button_reset`**: Provides a button that resets the scene or model to its original state (`true` or `false`).

- **`show_test_params`**: Indicates whether test parameters are visible for debugging or testing purposes (`true` or `false`).

- **`button_test_params`**: Shows a button to allow toggling of test parameters visibility (`true` or `false`).

- **`camera_start`**: Defines the starting position of the camera in the format `[x, y, z]` (e.g., `[8, 3, 10]`).

- **`storelocal_toggled`**: Defines whether certain settings or parameters should be saved locally (e.g., in session storage) (`true` or `false`).

- **`base_color`**: Sets the base color for the model, usually defined as a hexadecimal color code (e.g., `0xffffff` for white).

- **`model_soft_shadow`**: Toggles soft shadows for the model, enhancing realism (`true` or `false`).

- **`model_scene_shadow`**: Toggles whether shadows are cast on the scene (`true` or `false`).

---

## Explanation and Use of Parameters

### Scene Configuration Parameters

- **`scene_height`** and **`scene_width`** define the dimensions of the scene in which the 3D model is rendered. These parameters are crucial for establishing the aspect ratio and ensuring the model fits well within the user's viewport.

- **`scene_viewport`** allows you to select between different types of viewing angles (`perspective` or `top`), influencing how depth and scale are perceived.

### Camera Control Parameters

- **`allow_camera_zoom`**, **`allow_camera_rotate`**, and **`allow_camera_pan`** provide granular control over the camera's capabilities, determining whether users can zoom, rotate, or pan to explore the model.

- **`camera_start`** sets the initial position of the camera, providing control over the perspective from which users first view the model.

### Model and Scene Visuals

- **`width`**, **`depth`**, **`height`**, and **`base_height`** are the primary measurements that determine the physical attributes of the 3D furniture model.

- **`show_wireframe`** helps visualize the underlying structure of the 3D model by displaying only the edges, which can be useful for debugging or for stylistic purposes.

- **`base_color`** sets the default color of the model, impacting its appearance and helping differentiate components.

### Interaction and Animation Parameters

- **`button_toggle_animation`** controls animations related to model components, such as doors and drawers.

- **`button_measurement`**, **`show_measurement`**, and **`button_reset`** allow users to interact with the model through on-screen controls, adding features like toggling measurement display or resetting the model to its initial state.

### Debugging and Testing

- **`show_test_params`** and **`button_test_params`** are particularly useful during development. They make it easier for developers to test various configurations and ensure that the model behaves as expected.

- **`storelocal_toggled`** allows certain user settings to be stored locally, so they persist across sessions.

### Shadows and Lighting

- **`model_soft_shadow`** and **`model_scene_shadow`** determine whether shadows are used in the scene, adding a layer of visual realism. Soft shadows help soften the transition between light and dark areas, making the rendering look more natural.

---

For more detailed information about the processes and components that involve these parameters, please refer to the respective documentation:
- [ANGULAR-STRUCTURE.md](/docs/ANGULAR-STRUCTURE.md)
- [IFRAME-LOADING.md](/docs/IFRAME-LOADING.md)
- [LOADING-PROCESS.md](/docs/LOADING-PROCESS.md)
- [UPDATING-PROCESS.md](/docs/UPDATING-PROCESS.md)
- [MATERIALS.md](/docs/MATERIALS.md)
- [PARAMETERS.md](/docs/PARAMETERS.md)