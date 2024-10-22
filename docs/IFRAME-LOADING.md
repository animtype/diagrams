# IFRAME URL Parameters Guide for Tweakly.eu

This document provides a comprehensive overview of how URL parameters are utilized when an IFRAME is called within the Tweakly.eu application. It simplifies the configuration process and outlines the effects of essential URL parameters on the application's behavior.

## Overview

When the application initializes within an IFRAME, it can receive configuration settings through URL parameters. These parameters dictate how the application loads and renders the initial 3D model, aligning the model with specific requirements or user preferences.

## URL Parameter Usage

- **Example**: `?url=tweakly%2Ftweakly_hallway_h1.json&model=%7B"width":1600,"depth":900,"height":770,"base_height":810%7D`

### `url`
- **Parameter Name**: `url`
- **Description**: Specifies the location of the furniture model file.
- **Example Usage**: `?url=furniture/furnitures%2Felo1.json`
- **Behavior**: This parameter fetches the model data from a specified URL, overriding the default or previously set model URL in the application. It is important to include the project name as part of the path to correctly locate the model file.

### `model`
- **Parameter Name**: `model`
- **Description**: Contains JSON-encoded parameters that define various dimensions and settings of the furniture model.
- **Example Usage**: `?model=%7B"width":1600,"depth":900,"height":770,"base_height":810%7D`
- **Behavior**: This parameter dynamically configures the model's properties, influencing dimensions and other necessary attributes for rendering and interaction within the scene.

#### Key Variables in `model` Parameter
- **`width`**, **`height`**, **`depth`**: Define the dimensions of the model.
- **`scene_width`**, **`scene_height`**: Set the dimensions of the scene in which the model is rendered.
- **`mat_selector_NAME`**, **`mat_selector_front`**: Set the material for the selection based on the selector name, such as "front" (e.g., `mat_selector_front`).

These parameters are critical for establishing the initial dimensions of the model and its environment, ensuring that the 3D model fits well within the user's view and the application's UI constraints.

### `test_view`
- **Parameter Name**: `test_view`
- **Description**: Indicates whether to load a test view from a local URL. This is useful for development or testing purposes.
- **Example Usage**: `?test_view=true`
- **Behavior**: Overrides certain application settings to load a local test view for rapid testing and development iterations.

### `logger`
- **Parameter Name**: `logger`
- **Description**: Enables console logging in a production environment. Useful for debugging and monitoring.
- **Example Usage**: `?logger=true`
- **Behavior**: Allows console logs to be displayed even when running the application in a production environment, providing insights and debugging information that would normally be disabled.

## Decoding and Applying Parameters

During the initialization of the application within an IFRAME, the `URLSearchParams` interface is used to parse query parameters from `window.location.search`. Parameters like `url` and `model` are decoded and applied as follows:

1. **Loading the Furniture Model URL**: If present, the `url` parameter specifies the path to the furniture model file, overriding the default source.
2. **Applying Model Dimensions and Settings**: The `model` parameter, if provided, contains a JSON-encoded string that details settings such as dimensions. These parameters are parsed and applied to the model, allowing for immediate customization based on URL data.
3. **Test View and Logger Settings**: Additional parameters like `test_view` and `logger` help control the application's behavior, making it easier to test in various environments.

### Error Handling

- If there is an error in parsing the `model` parameter, it is logged to prevent the application from crashing and to provide a debug point.

This process ensures the application can be customized dynamically via URL parameters without the need for recompilation or manual adjustments, facilitating easier integration and testing in different environments.

---

For more detailed information about the processes mentioned above, please refer to the respective documentation:
- [ANGULAR-STRUCTURE.md](/docs/ANGULAR-STRUCTURE.md)
- [IFRAME-LOADING.md](/docs/IFRAME-LOADING.md)
- [LOADING-PROCESS.md](/docs/LOADING-PROCESS.md)
- [UPDATING-PROCESS.md](/docs/UPDATING-PROCESS.md)
- [MATERIALS.md](/docs/MATERIALS.md)
- [PARAMETERS.md](/docs/PARAMETERS.md)