---
created: 2024-12-07 04:58:55
url:
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
---


# Game Engines using Unreal Engine - Graphics and Game Engine Pipelines

Here are the Mermaid diagrams representing Unreal Engine, categorized for clarity.

## 1. High-Level Overview of Unreal Engine Architecture

```mermaid
graph TD
    A[Game] --> B(Engine)
    B --> C{Core Subsystems}
    C --> D[Rendering Engine]
    C --> E["Physics Engine (e.g., Chaos, PhysX)"]
    C --> F[Animation Engine]
    C --> G[Networking & Replication]
    C --> H[Audio Engine]
    C --> I[AI Engine]
    C --> J["Scripting (e.g., Blueprints, C++)"]
    B --> K{Platform Abstraction Layer}
    K --> L[Windows, macOS, Linux, iOS, Android, Consoles, etc.]
   D --> M[Scene Management]
   M --> N[Visibility & Occlusion Culling]
   M --> O["Level of Detail (LOD)"]
   D --> P[Rendering Pipeline]
    
    classDef highLevel fill:#e10f,stroke:#333,stroke-width:2px;
    class A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P highLevel

```

**Explanation:**

*   **Game:** The top-level object representing a specific game.
*   **Engine:** The core Unreal Engine, providing essential services.
*   **Core Subsystems:** Key modules within the engine:
    *   **Rendering Engine:**  Responsible for drawing visuals.
    *   **Physics Engine:** Handles physical simulations.
    *   **Animation Engine:** Controls character and object animations.
    *   **Networking & Replication:** Manages multiplayer functionality.
    *   **Audio Engine:** Processes sounds and music.
    *   **AI Engine:** Provides tools for non-player character behavior.
    *   **Scripting:** Allows game logic to be written in Blueprints or C++.
*   **Platform Abstraction Layer:** Enables cross-platform support.
*   **Scene Management:** Handles objects, levels, culling, and LODs.
*   **Rendering Pipeline:** (Detailed in the next diagram).

## 2. Unreal Engine's Rendering Pipeline (Simplified)

```mermaid
graph TD
    A[Scene Data] --> B{Visibility Culling}
        B -- Visible Objects --> C[Render Queue]
    C --> D{Base Pass}
    D --> E{Depth Prepass}
    D --> F[Material Shading]
     F --> G[Lighting]
    G --> H{Post Processing}
     H --> I[Output Framebuffer]

    classDef stage fill:#f196,stroke:#333,stroke-width:2px;
    class A,C stage
    classDef process fill:#61cf,stroke:#333,stroke-width:2px;
    class B,D,E,F,G,H process
    classDef output fill:#9f16,stroke:#333,stroke-width:2px;
    class I output

```

**Explanation:**

1. **Scene Data:** Information about objects in the scene, including meshes, materials, and lights.
2. **Visibility Culling:** Determines which objects are visible to the camera, optimizing performance.
3. **Render Queue:** A list of visible objects to be rendered.
4. **Base Pass:** Main rendering pass:

    *   **Depth Prepass:** Renders depth information for optimization.
    *   **Material Shading:** Calculates the color of objects based on their materials and lighting.
5. **Lighting:** Computes light contributions.
6. **Post Processing:** Applies effects like bloom, motion blur, and color grading.
7. **Output Framebuffer:** The final rendered image.

## 3. Unreal Engine's Deferred Rendering Pipeline (Detailed)

```mermaid
graph TD
    A[Scene Data] --> B{Visibility Culling}
    B -- Visible Objects --> C[Render Queue]
    C --> D{"Geometry Pass (G-Buffer)"}
    D --> E[Base Color]
    D --> F[Metallic]
    D --> G[Roughness]
    D --> H[Normal]
    D --> I[Specular]
    D --> J{Other G-Buffer Channels}
     D --> K["Depth (Pre-pass)"]
    J --> L{G-Buffer}
    L --> M{Lighting Pass}
    M --> N[Direct Lighting]
    M --> O["Indirect Lighting (e.g., Global Illumination)"]
    M --> P[Reflections]
    M --> Q[Shadows]
    N --> R{Combine Lighting}
    O --> R
    P --> R
    Q --> R
    R --> S{Post Processing}
    S --> T[Output Framebuffer]

    classDef stage fill:#f196,stroke:#333,stroke-width:2px;
    class A,C stage
    classDef process fill:#61cf,stroke:#333,stroke-width:2px;
    class B,D,M,R,S process
    classDef gbuffer fill:#f1c9,stroke:#333,stroke-width:2px;
    class E,F,G,H,I,J,K,L gbuffer
    classDef lighting fill:#11fc,stroke:#333,stroke-width:2px;
    class N,O,P,Q lighting
    classDef output fill:#1f16,stroke:#333,stroke-width:2px;
    class T output

```

**Explanation:**

1. **Scene Data:** Information about the scene.
2. **Visibility Culling:** Determines visible objects.
3. **Render Queue:** A list of visible objects.
4. **Geometry Pass (G-Buffer):** Objects are rendered to multiple render targets (G-buffer), storing properties like:

    *   **Base Color:** The albedo or diffuse color.
    *   **Metallic:** How metallic the surface is.
    *   **Roughness:** How rough or smooth the surface is.
    *   **Normal:** Surface orientation.
    *   **Specular:** Specular highlight intensity.
    *   **Other G-Buffer Channels:**  Ambient occlusion, emissive, etc.
    *   **Depth (Pre-pass)**: Depth information can be rendered in a separate pre-pass or as part of the G-buffer pass.
5. **G-Buffer:** A collection of textures storing deferred shading data.
6. **Lighting Pass:** Lighting calculations are performed using the G-buffer:

    *   **Direct Lighting:** Light from light sources.
    *   **Indirect Lighting:** Bounced light (global illumination).
    *   **Reflections:** Reflection of the environment.
    *   **Shadows:** Shadow calculations.
7. **Combine Lighting:** Different lighting components are combined.
8. **Post Processing:** Effects are applied to the combined image.
9. **Output Framebuffer:** The final rendered frame.

## 4. Unreal Engine Material System

```mermaid
graph TD
    A[Material] --> B{Material Graph}
    B -- Nodes --> C[Material Inputs/Outputs]
    B --> F[Material Expression Nodes]
     F --> FA[Texture Sample]
     F --> FB[Constant]
     F --> FC[Arithmetic Operations]
      F --> FD[Vector Operations]
    F --> FE[Custom HLSL Code]
    C --> D[Base Color]
    C --> E[Metallic]
    C --> G[Roughness]
    C --> H[Normal]
    C --> I[Emissive Color]
    C --> J["Other Outputs (e.g., Opacity, World Position Offset)"]
    

    classDef material fill:#91fa,stroke:#333,stroke-width:2px;
    class A,B,C,F,FA,FB,FC,FD material
    classDef outputs fill:#12af,stroke:#333,stroke-width:2px;
    class D,E,G,H,I,J outputs
    
```

**Explanation:**

1. **Material:** Defines the visual properties of a surface.
2. **Material Graph:** A visual scripting graph where materials are created.
3. **Material Inputs/Outputs:** Pins that connect nodes in the graph.
4. **Material Expression Nodes:** Building blocks of materials:

    *   **Texture Sample:** Samples a texture.
    *   **Constant:** Provides a constant value.
    *   **Arithmetic Operations:** Add, subtract, multiply, etc.
    *   **Vector Operations:** Dot product, cross product, normalize, etc.
    *   **Custom HLSL Code:** Allows writing custom shaders.

5. Material Outputs determine how the material interacts with light and the rendering pipeline, common outputs include but aren't limited to:

    *   **Base Color:** The base color of the surface.
    *   **Metallic:** How metallic the surface is.
    *   **Roughness:** How rough or smooth the surface is.
    *   **Normal:** Specifies the surface normal for detailed shading.
    *   **Emissive Color:** Light emitted by the surface.
    *   **Other Outputs:** Opacity, world position offset, etc.

## 5. Blueprints Visual Scripting

```mermaid
graph TD
    A[Blueprint] --> B{Event Graph}
    B -- Nodes --> C[Events]
    B --> D[Functions]
    B --> E[Variables]
    B --> F[Macros]
     B --> G[Exec Pins]
    B --> H[Data Pins]
    C --> I[Event BeginPlay]
    C --> J[Event Tick]
    C --> K[Custom Events]
    D --> L[Add, Subtract, etc.]
    D --> M["Branch (if/else)"]
    D --> N[For Loop]
    D --> O[Spawn Actor]
    D --> P[Get/Set Actor Location]
    E --> Q[Boolean]
    E --> R[Integer]
    E --> S[Float]
    E --> T[Vector]
    E --> U[Actor Reference]

    classDef blueprint fill:#c19f,stroke:#333,stroke-width:2px;
    class A,B,C,D,E,F,G,H blueprint
    classDef events fill:#129c,stroke:#333,stroke-width:2px;
    class I,J,K events
    classDef functions fill:#91cf,stroke:#333,stroke-width:2px;
    class L,M,N,O,P functions
    classDef variables fill:#2c19,stroke:#333,stroke-width:2px;
    class Q,R,S,T,U variables

```

**Explanation:**

1. **Blueprint:** A visual script asset in Unreal Engine.
2. **Event Graph:** A graph containing nodes that define the Blueprint's behavior.
3. **Nodes:** Building blocks of Blueprints:

    *   **Events:** Trigger execution based on game events (e.g., `BeginPlay`, `Tick`, custom events).
    *   **Functions:** Perform actions or calculations (e.g., arithmetic operations, control flow, spawning actors).
    *   **Variables:** Store data (e.g., Boolean, Integer, Float, Vector, Actor references).
    *   **Macros:** Reusable groups of nodes.
    *   **Exec Pins:** Control the flow of execution between nodes.
    *   **Data Pins:** Pass data between nodes.

These diagrams provide a comprehensive, yet concise, overview of key aspects of Unreal Engine, its architecture, rendering pipeline, and visual scripting system.

---