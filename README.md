# COMP3015 Initial Prototype 30% Overview

## Development Environment

- **Visual Studio Version**: 2022
- **Operating System**: Windows 11 Home

The code for this prototype was developed and tested using **Visual Studio 2022** on **Windows 11 Home**.

## Link to Unlisted YouTube Video

Video demonstration on YouTube: [Watch Video]()

## How Does It Work?

This prototype is designed to render a 3D object using OpenGL, with a focus on lighting and shading effects such as **Phong lighting**, **toon shading**, **normal mapping**, and **fog**. The application loads a 3D model (a skull) and applies textures and lighting, creating a stylised 3D rendering that simulates cartoonish shading with fog effects.

### Key Components

1. **SceneBasic_Uniform Class**:
    - The main class that handles the setup, update, and rendering of the scene.
    - **initScene()**: Initializes shaders, loads textures, and sets up light sources.
    - **compile()**: Compiles and links the shaders for use.
    - **update()**: Updates the scene, rotating the object.
    - **render()**: Renders the scene, applying all shaders, textures, and lighting effects.
    - **resize()**: Handles window resizing and updates the projection matrix.
    - **setMatrices()**: Updates and sets matrix uniforms (model, view, projection) for shader programs.

2. **Shaders**:
    - **basic_uniform.vert (Vertex Shader)**:
      - Transforms vertices from object space to camera space.
      - Passes lighting and normal data to the fragment shader.
      - Computes the tangent for normal mapping.
      - Calculates fog depth for each fragment.
    - **basic_uniform.frag (Fragment Shader)**:
      - Uses textures (base color and normal map) to compute the final color.
      - Performs lighting calculations using Phong lighting (diffuse and ambient), with toon shading applied to create a stylised look.
      - Calculates fog blending based on fragment depth.

3. **Lighting & Material**:
    - Two light sources are used in the scene.
    - Material properties (diffuse, ambient, specular, shininess) are passed to the shader to control how the object reacts to light.
    - The diffuse component is calculated using the **toon shading** technique, where lighting is quantized into discrete steps for a cartoon-like effect.

4. **Textures**:
    - **Base Texture**: A standard texture that defines the color of the object.
    - **Normal Map**: Used for bump mapping to add surface detail without increasing geometry complexity.

5. **Fog Effect**:
    - Linear fog is applied based on the camera's distance from the object, blending the object's color with a specified fog color.

## Code Structure and Navigation

### High-Level Structure

- The **SceneBasic_Uniform** class is the central point where the program initializes, updates, and renders the scene.
- The **shaders** (vertex and fragment) define how the graphics are computed on the GPU. They handle transformations, lighting calculations, and texturing.
- The `render()` function is responsible for the actual rendering pipeline, where textures, shaders, and lighting information are passed to OpenGL.
- **Textures** and **models** are loaded using helper functions (`Texture::loadTexture` and `ObjMesh::load`).

### Programmer Navigation

1. **Initialization**:
   - Begin by calling `initScene()` to set up shaders, lighting, textures, and the 3D model. This function also prepares the view and projection matrices.
2. **Updating the Scene**:
   - The `update()` function rotates the object and updates the model transformation matrix.
3. **Rendering the Scene**:
   - The `render()` function is called to clear the screen, apply lighting and material properties, and render the object. The shaders handle all lighting and fog calculations.
4. **Shader Files**:
   - Ensure the shaders `basic_uniform.vert` and `basic_uniform.frag` are present in the correct paths (`shader/` directory). These files contain the logic for vertex transformations, normal mapping, and the toon shading effect.

## Additional Information

- **Toon Shading**: This technique was applied in the fragment shader to simulate a cartoon-like, stepped lighting effect.
- **Normal Mapping**: Used to simulate surface detail like bumps or wrinkles without adding extra geometry to the model.
- **Fog Effect**: A linear fog effect is used to simulate atmospheric scattering, fading distant objects into the background.
