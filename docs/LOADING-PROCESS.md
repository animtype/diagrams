# Loading Process for Tweakly.eu 3D Models

This document outlines the structure and loading process of the 3D JSON model files used in the Tweakly.eu Angular application for displaying 3D furniture models.

---

## URL Parameters Overview

The application supports specific URL parameters that can be used to customize the loading of the 3D furniture model. Below are the key parameters and their roles:

- **`url`**: Specifies the URL for the furniture model JSON file. This allows for loading different furniture models dynamically based on the provided URL.
  - Example: `?url=models/tweakly/tweakly_regal_one.json`

- **`model`**: Contains model-specific parameters in JSON format, which are applied to adjust the dimensions or properties of the furniture. This allows for instance-specific customization without modifying the core model.
  - Example: `?model={"width":1600,"depth":900,"height":770}`

- **`test_view`**: Indicates whether to load a test view from a local URL. This is useful for testing or development purposes to override default settings.
  - Example: `?test_view=true`

- **`logger`**: Enables console logging in a production environment. This is useful for debugging or monitoring purposes.
  - Example: `?logger=true`

These URL parameters are parsed during the loading process, allowing for flexible control over the rendering and customization of 3D models directly via the URL.

---

## Part 1: 3D JSON Model File Structure

The 3D JSON model file organizes the data needed to render a piece of furniture within a 3D scene. It is structured hierarchically, with `furniture` as the primary node, which may contain multiple child nodes representing different pieces of furniture. Currently, only a single piece of furniture is used.

### Hierarchical Structure Overview

- **`furnitures`**: The parent node that encapsulates all furniture elements in the scene.

```
- furnitures
  - furniture (Array of furniture objects, typically one)
    - settings (Units of measurement, other settings, etc.)
    - global_url (Reference to global parameters for rendering, such as thickness, dimensions, etc.)
    - material_url (Reference to materials used in the model)
```

- **`furniture`**:
  - **`global_url`**: Specifies parameters for rendering, including dimensions and thickness.
  - **`material_url`**: Contains data on the materials used in rendering the furniture.
  - **`groups`**: The `furniture` node can contain `groups`, which can further contain `models` or additional `groups` up to three levels deep.

### Dynamic Measurement Calculation

The JSON model primarily uses relative units (e.g., `parameters.width`) defined in a parameters JSON file, referenced by `global_url`. Most dimensions in the 3D model JSON are relative, allowing the model to adapt to various sizes using different parameters without modifying the core model structure.

### Sample JSON Snippet

```json
{
  "name": "EL01",
  "units": "mm",
  "shopid": "244839Jwue",
  "global_url": "global/tweakly_hallway.json",
  "material_url": "materials/tweakly.json",
  "mat_selector": "model",
  "dimensions": {
    "width": { "calc": "parameters.width" },
    "depth": { "calc": "parameters.depth" },
    "height": { "calc": "parameters.height" }
  },
  "groups": [{}]
}
```

---

## Part 2: Parameters JSON Structure

The `parameters` JSON is crucial for defining the dimensions and settings for rendering. It is initially sourced from the `global_url` and can be updated dynamically.

### Example Parameters JSON

```json
{
  "id": "tweakly_table",
  "base_height": 600,
  "shelf_thickness": 25,
  "side_thickness": 40,
  "back_thickness": 4,
  "width": 1600,
  "height": 760,
  "depth": 800,
  "materials_url": "materials/tweakly.json"
}
```

### Key Concepts

- **Parameter References**: Any reference like `parameters.base_height` in the furniture JSON is replaced with values from the `parameters` JSON.
- **Calculation Object**: Objects like `"calc": "parameters..."` allow arithmetic operations within the model file, making it possible to update variables dynamically. For example, `parameters.width` can be modified as `parameters.width = parameters.width * 2` to adjust the size based on specific requirements.
- **Finalized Model**: After processing, all relative measures in the 3D JSON are replaced with absolute values from the `parameters` JSON.

---

## Part 3: Parameters JSON Loading Process

The parameters JSON is updated in stages, with a fallback mechanism and a prioritized loading sequence.

### Step-by-Step Loading Process

1. **Initial Load from Angular Environment**

   - Parameters are read from `environment.parameters` within the Angular application. These parameters are essential for initial scene setup.

1.1 **Preliminary Preparation: `checkCalculations`**

   - Before proceeding to the next stages, the parameters undergo an additional preparation step using the `checkCalculations` function. This function evaluates and updates parameters to ensure all derived calculations are correctly applied before moving forward.

2. **Override with `global_url`**

   - Parameters from the `global_url` JSON file are read, overwriting any default values from the Angular environment. This step ensures that any global settings or shared dimensions are applied consistently across the model.

3. **Override with IFRAME URL Arguments**

   - Parameters provided via IFRAME URL arguments (such as width, height, and depth) take precedence over previous settings. These arguments are crucial for defining instance-specific dimensions for the furniture, allowing unique adjustments without altering the original model file.

4. **Post-load Updates via `PostMsg`**

   - After the initial rendering, parameters can be updated dynamically via `PostMsg`. This allows for real-time updates of the model without redrawing the entire 3D scene, making it efficient for user interactions or other dynamic changes.

### Rendering Sequence

- **Initial Render**: The initial render takes place during step 3, where IFRAME URL arguments are used to define the dimensions for the first time.
- **Update Render**: During step 4, updates are applied specifically to modify the 3D model. These updates affect only the model properties without redrawing the entire scene, enhancing performance.
- **Absolute Measurements**: By the end of the process, all dimensions in the 3D JSON are converted into absolute values derived from the latest version of the `parameters` JSON, ensuring a fully parameterized and consistent model.

### ReturnFurnitures Function as the Loading Process

The `returnFurnitures` function is responsible for managing the entire loading process of the furniture data. Here's a summary of how it works:

- **Clear Existing Data**: The function starts by clearing any previously loaded furniture data to prevent conflicts.
- **Load Initial Data**: It then loads the initial 3D model data, including parameters and assets, which form the basis for the furniture rendering.
- **Initialize Furniture Array**: Once the initial data is loaded, it sets up the furniture array and adds the loaded furniture model to it.
- **Apply Calculations**: If calculations are needed, it evaluates and updates the parameters to ensure derived values are accurate and up to date.
- **Evaluate Model Properties**: The function then ensures all expressions within the model are evaluated properly, resulting in updated and consistent model properties.
- **Collect Material Selectors**: It collects material selectors, which may be useful for testing or validation purposes.
- **Return the Furniture Data**: Finally, it returns the complete furniture data, ready for rendering in the 3D scene.

This structured approach ensures that all parameters are layered correctly, with each stage offering the opportunity to adjust and refine the furniture model as needed, while maintaining consistency.

---

## How `updateModelProperties` and `evaluateExpression` Work

To further understand the dynamic evaluation of model properties, it's essential to know how the functions `updateModelProperties` and `evaluateExpression` operate during the loading process.

### `updateModelProperties` Function

- **Purpose**: This function recursively updates object properties within the 3D model JSON by evaluating specific expressions defined in the model file. It ensures that all parameter references and calculations are applied consistently throughout the furniture model.
- **Process**:
  - **Traversal**: It traverses the model object, identifying keys that need updating, such as those with `calc` properties or conditions.
  - **Handling `calc` Properties**: When a property has a `"calc"` key, it passes the expression to the `evaluateExpression` function to determine the final value.
  - **Recursion**: The function is recursive, meaning it will continue to process all nested objects, ensuring that every relevant parameter and calculation is correctly applied.
  - **Condition Checks**: It also evaluates conditions like `show_if` or `hide_if`, ensuring that visibility and settings are properly adjusted based on parameters.

### `evaluateExpression` Function

- **Purpose**: The `evaluateExpression` function is responsible for evaluating arithmetic expressions defined in the `calc` properties of the JSON model.
- **Process**:
  - **Replacing Parameters**: It replaces references like `parameters.width` within the expression with their actual values from the parameters JSON.
  - **Expression Evaluation**: It uses JavaScript's `Function` constructor to evaluate the resulting arithmetic expression, which allows for dynamic calculations such as addition, subtraction, multiplication, and division.
  - **Error Handling**: The function includes error handling to log warnings if an expression cannot be evaluated, ensuring that issues can be easily identified and resolved.

These functions work together to dynamically adapt the model properties based on updated parameters, ensuring the 3D representation always reflects the latest settings without requiring manual edits to the core JSON model.

---

For more detailed information about the processes mentioned above, please refer to the respective documentation:
- [ANGULAR-STRUCTURE.md](/docs/ANGULAR-STRUCTURE.md)
- [IFRAME-LOADING.md](/docs/IFRAME-LOADING.md)
- [LOADING-PROCESS.md](/docs/LOADING-PROCESS.md)
- [UPDATING-PROCESS.md](/docs/UPDATING-PROCESS.md)
- [MATERIALS.md](/docs/MATERIALS.md)
- [PARAMETERS.md](/docs/PARAMETERS.md)