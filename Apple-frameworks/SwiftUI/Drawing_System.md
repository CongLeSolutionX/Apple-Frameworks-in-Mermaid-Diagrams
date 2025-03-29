---
created: 2025-03-28 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Drawing System (Canvas & GraphicsContext) - A Diagrammatic Guide 
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---


Visualizing how drawing works using `Canvas` and `GraphicsContext`.

```mermaid
---
title: "SwiftUI Framework - Drawing System (Canvas & GraphicsContext)"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  layout: elk
  look: handDrawn
  theme: dark
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%%%%%%% Toggle theme value to `base` to activate the initilization below for the customized theme version.
%%%%%%%% Available curve styles include the following keywords:
%% basis, bumpX, bumpY, cardinal, catmullRom, linear, monotoneX, monotoneY, natural, step, stepAfter, stepBefore.
%%{
  init: {
    'graph': { 'htmlLabels': false, 'curve': 'linear' },
    'fontFamily': 'Fantasy',
    'themeVariables': {
      'primaryColor': '#ffff',
      'primaryTextColor': '#55ff',
      'primaryBorderColor': '#7c2',
      'lineColor': '#F8B229',
      'secondaryColor': '#006100',
      'tertiaryColor': '#fff'
    }
  }
}%%
graph TD
    D_Canvas(Canvas<Symbols>) -- "Provides" --> D_Renderer["Renderer Closure (inout GC, CGSize) -> Void"]
    D_Renderer -- "Receives" --> D_GC(GraphicsContext)
    D_Renderer -- "Receives" --> D_Size(CGSize)
    D_Canvas -- "Optionally Takes" --> D_Symbols(Symbols @ViewBuilder)

    subgraph GraphicsContextOps["GraphicsContext Operations"]
        D_GC -- "State" --> GC_State{Opacity, BlendMode, Transform, ClipRect}
        D_GC -- "Drawing" --> GC_DrawOps["fill(Path, Shading), stroke(Path, Shading), draw(Image), draw(Text), draw(ResolvedSymbol), drawLayer(...)"]
        D_GC -- "Resolving" --> GC_ResolveOps["resolve(Image), resolve(Text), resolveSymbol(id:)"]
        D_GC -- "Filters" --> GC_FilterOps["addFilter(Filter)"]
        D_GC -- "Clipping" --> GC_ClipOps["clip(to: Path), clipToLayer(...)"]
        D_GC -- "Transforms" --> GC_TransformOps["scaleBy(...), translateBy(...), rotate(by:), concatenate(...)"]
        D_GC -- "Interop" --> GC_Interop["withCGContext(...)"]
        D_GC -- "Environment" --> EnvironmentValues
    end

    subgraph GraphicsContextTypes["Associated GraphicsContext Types"]
        GCT_BlendMode(GraphicsContext.BlendMode Enum) -- ".normal, .multiply, .screen, ..." --> GCT_BlendMode
        GCT_Shading(GraphicsContext.Shading Struct) -- ".color, .style, .linearGradient, .radialGradient, .conicGradient, .tiledImage, .shader, .meshGradient, ..." --> GCT_Shading
        GCT_Filter(GraphicsContext.Filter Struct) -- ".shadow, .blur, .colorMatrix, .projectionTransform, ..." --> GCT_Filter
        GCT_ResolvedImage(GraphicsContext.ResolvedImage Struct) -- ".size, .baseline, .shading" --> GCT_ResolvedImage
        GCT_ResolvedText(GraphicsContext.ResolvedText Struct) -- ".shading, .measure(in:), .firstBaseline(in:), ..." --> GCT_ResolvedText
        GCT_ResolvedSymbol(GraphicsContext.ResolvedSymbol Struct) -- ".size" --> GCT_ResolvedSymbol
        GCT_ClipOptions(GraphicsContext.ClipOptions OptionSet) -- ".inverse" --> GCT_ClipOptions
        GCT_GradientOptions(GraphicsContext.GradientOptions OptionSet) -- ".repeat, .mirror, .linearColor" --> GCT_GradientOptions
        GCT_ShadowOptions(GraphicsContext.ShadowOptions OptionSet) -- ".shadowAbove, .shadowOnly, .invertsAlpha, .disablesGroup" --> GCT_ShadowOptions
        GCT_BlurOptions(GraphicsContext.BlurOptions OptionSet) -- ".opaque, .dithersResult" --> GCT_BlurOptions
        GCT_FilterOptions(GraphicsContext.FilterOptions OptionSet) -- ".linearColor" --> GCT_FilterOptions
        ColorMatrix  -- ".colorMatrix()" --> GCT_Filter
    end

    D_Symbols -- ".tag(ID)" --> TaggedView
    D_GC -- "resolveSymbol(id: ID)" --> GCT_ResolvedSymbol
    GC_DrawOps -- uses --> GCT_Shading
    GC_FilterOps -- uses --> GCT_Filter
    GC_FilterOps -- uses --> GCT_FilterOptions
    GC_ClipOps -- uses --> GCT_ClipOptions
    GCT_Filter -- ".shadow(...)" --> GCT_ShadowOptions
    GCT_Filter -- ".blur(...)" --> GCT_BlurOptions
    GCT_Shading -- Gradient methods --> GCT_GradientOptions
    
```

----


**Explanation:** This diagram focuses on the `Canvas` view and the `GraphicsContext` it provides. It shows the main operations available on the context (state changes, drawing, resolving, filters, clipping, transforms) and lists the key associated types like `BlendMode`, `Shading`, `Filter`, `ResolvedImage`, etc.



---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---