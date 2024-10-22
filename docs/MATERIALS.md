# Material Management for Tweakly.eu 3D Models

This document outlines the management and configuration of materials used in the Tweakly.eu Angular application for displaying 3D furniture models. It details how materials are defined, selected, and dynamically applied to enhance the visual representation of 3D models using the THREE.js library.

---

## Summary

Materials are crucial in defining the visual aspects of 3D models in the Tweakly.eu application. This guide provides a comprehensive overview of how materials are configured, managed, and dynamically applied based on JSON configurations.

## Material Configuration

Materials in the Tweakly.eu application are defined using the `MaterialConfig` interface, which includes properties such as color, texture maps, transparency, shininess, etc. These materials are managed within the `materials.service.ts` and are crucial for rendering realistic 3D furniture models.

### Properties of `MaterialConfig`

The `MaterialConfig` interface defines the following properties for materials:

#### Globally Accessible Materials
- **globals_inox**: Stainless steel material for metallic finishes.
- **globals_chrome**: Chrome material for reflective surfaces.
- **globals_material_drawer**: Material used for drawer components.
- **globals_material_foot**: Material used for foot components.
- **globals_material_mirror**: Mirror material for reflective surfaces.
- **globals_material_glass**: Glass material for transparent or translucent elements.

### Material Properties
- **color**: The color of the material.
- **map**: The texture map applied to the material.
- **bumpMap**: The bump map for adding surface details.
- **shininess**: The shininess factor for specular highlights.
- **transparent**: Boolean indicating if the material is transparent.
- **opacity**: The opacity level of the material.
- **depthWrite** *(optional)*: Set to `false` to avoid writing to the depth buffer, preventing visual artifacts like flickering when multiple transparent objects overlap.
- **depthTest** *(optional)*: Set to `true` to ensure that the depth of each fragment is tested before rendering, which helps in avoiding overlap issues.

Materials are instantiated and managed within the `materials.service.ts`, ensuring that materials like `MeshBasicMaterial`, `MeshPhongMaterial`, and `ShadowMaterial` are appropriately configured and stored.

## Material Selection Process

The application facilitates dynamic material selection through the `mat_selector` mechanism. This functionality allows materials to be assigned to specific parts of a model based on configuration settings defined in the model's parameters.

### Using `mat_selector`

Material selection operates similarly to applying styles and classes in the DOM. Note that only the following reserved names can be used for `mat_selector`:

- **model**
- **front**
- **handle**
- **drawer**
- **door**
- **foot**
- **inner**
- **back**
- **zone**
- **zone1** to **zone9**

Any other name is not allowed and will result in an error.

#### Material Selection Concepts

- **Material as STYLE**: In the context of 3D models, `material` can be considered akin to a style attribute in the DOM. It directly applies specific visual properties to the model parts.
- **`mat_selector` as CLASS**: Similarly, `mat_selector` functions like a class in HTML, where it represents a reference to a set of predefined styles that can be dynamically applied to various parts of the model.

### Material Selector Methods

This approach allows for:
- **`createMaterialSelectorMaterials`**: This method creates materials for various selectors such as `model`, `front`, `handle`, `drawer`, etc.
- **`initMatSelector`**: Initializes the material selectors based on model parameters, extracting material names and updating properties as needed.

### Fallback Mechanism

A sophisticated fallback mechanism ensures that every model part has a valid material applied:
1. **Direct Material Application**: The application first attempts to apply a specified material directly to the model.
2. **Mat Selector Usage**: If no direct material exists, the application searches for a `mat_selector` to apply a general material name.
3. **Parent `mat_selector`**: If neither is found, it searches for a parent `mat_selector`, ensuring that the main parent always provides a fallback material.

### Dynamic Material Updates

- **`changeMaterial`** and **`updateMaterialProperties`**: These functions allow for the dynamic updating of materials in the model based on `mat_selector`. Changes to material properties can be applied immediately without the need for redrawing the model, enabling seamless visual updates.

All customizable materials are typically created as `MeshPhongMaterial` to maintain consistency and visual quality across different model configurations.

---

For more detailed information about the processes mentioned above, please refer to the respective process documentation:
- [ANGULAR-STRUCTURE.md](/docs/ANGULAR-STRUCTURE.md)
- [IFRAME-LOADING.md](/docs/IFRAME-LOADING.md)
- [LOADING-PROCESS.md](/docs/LOADING-PROCESS.md)
- [UPDATING-PROCESS.md](/docs/UPDATING-PROCESS.md)
- [MATERIALS.md](/docs/MATERIALS.md)
- [PARAMETERS.md](/docs/PARAMETERS.md)