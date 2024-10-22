# Angular Structure for Tweakly.eu 3D Models

This document explains the functionality of the Tweakly Angular application used for displaying 3D furniture models.

---

## Development Environment

The Tweakly.eu application is built on a robust and modern tech stack that ensures high performance and scalability:

1. **Angular (Latest Version)**: The application is developed using the latest version of Angular. Regular updates are performed to ensure the application stays up-to-date with the latest releases, enhancing performance, security, and features.

2. **Three.js (Stable Version)**: For 3D modeling and rendering, we use Three.js. It is crucial that we load the latest stable version of Three.js to benefit from the most recent improvements and fixes in 3D rendering technology.

3. **Additional Libraries**: Other libraries used in the application are part of the core Angular environment, such as Angular CLI and Angular Core libraries. These are updated alongside Angular to maintain compatibility and performance.

---

## Application Structure

The Angular project is organized as follows:

### `/app/scene/`

- **clients/**
  - Contains client-specific customizations. The `main` branch does not contain client-specific committed versions.

- **models/**
  - Includes all 3D models for rendering and the logic required for drawing them.

- **config.service.ts**
  - Manages all configurations for displaying the scene using the THREE.js library. This includes setting up scene lights, camera positions, and other necessary configurations for the 3D environment.

- **engine.service.ts**
  - Computes all positions and settings from the 3D JSON and converts them into relative units for more straightforward rendering of the models.

- **load.service.ts**
  - Loads the 3D JSON containing data for rendering, utilizes the loading logic (see `LOADING-PROCESS.md`), and updates the 3D JSON with parameters such as dimensions and materials.

- **materials.service.ts**
  - Contains all default materials and loads materials from the 3D JSON that will be used for the specific 3D model (refer to `MATERIALS.md`).

- **msg.service.ts**
  - Handles update triggers via `postMsg`, determining whether to execute an `UPDATE SCENE` or a `REFRESH SCENE`.

- **logger.service.ts**
  - Manages logging, such as `console.log`. Console logs are disabled in production environments but can be enabled using the `?logger=true` URL parameter. This feature is particularly useful for debugging and monitoring in production.

- **scene-interfaces.ts**
  - Stores all interfaces in one place, allowing each service or component to easily access shared data structures. This helps maintain consistency and reusability throughout the application.

- **scene.component.[ts|html|scss]**
  - The main component responsible for rendering the 3D model in the scene. It initiates when `engine.service` has calculated and prepared the 3D JSON for rendering. It also manages model controls, camera positions, and animations on demand.

---

## Responsibilities of Each Service

Each service within the Angular project is responsible for a specific aspect of the application, working together to render the 3D scenes effectively:

- **`config.service.ts`**: Manages scene configuration, including lighting and camera setup.
- **`engine.service.ts`**: Calculates positions and converts settings for the 3D models.
- **`load.service.ts`**: Loads and processes the 3D JSON, adding dimensions and materials.
- **`materials.service.ts`**: Loads and manages materials for the models.
- **`msg.service.ts`**: Handles update triggers via `postMsg` to refresh or update the scene.
- **`logger.service.ts`**: Manages logging behavior depending on the environment.
- **`scene-interfaces.ts`**: Centralizes all interfaces for easy access and consistency.
- **`scene.component`**: Renders the 3D scene, manages controls, and handles animations.

Please note that all `*.spec.ts` files are Angular testing files, used to define tests for their corresponding services and components.

---

## Documentation Reference

This documentation is based on:
[NG-Doc Documentation - Getting Started](https://ng-doc.com/docs/getting-started/installation)

---

For more detailed information about the processes mentioned above, please refer to the respective documentation:
- [ANGULAR-STRUCTURE.md](/docs/ANGULAR-STRUCTURE.md)
- [IFRAME-LOADING.md](/docs/IFRAME-LOADING.md)
- [LOADING-PROCESS.md](/docs/LOADING-PROCESS.md)
- [UPDATING-PROCESS.md](/docs/UPDATING-PROCESS.md)
- [MATERIALS.md](/docs/MATERIALS.md)
- [PARAMETERS.md](/docs/PARAMETERS.md)