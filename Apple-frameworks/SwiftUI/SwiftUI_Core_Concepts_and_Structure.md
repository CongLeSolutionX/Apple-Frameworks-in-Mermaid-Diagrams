---
created: 2025-03-19 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# SwiftUI Core Concepts & Structure - A Diagrammatic Guide
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---




This diagram illustrates the fundamental building blocks and protocols.

```mermaid
---
title: "SwiftUI Framework - SwiftUI Core Concepts & Structure"
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
    subgraph CoreProtocols["Core Protocols"]
        P_View(View) -- implements --> CustomView(Your Custom View)
        P_View -- "body: some View" --> P_View
        P_ViewModifier(ViewModifier) -- "body(content: Content)" --> P_View
        P_Shape(Shape) -- extends --> P_View
        P_Shape -- "path(in: CGRect)" --> Path(Path)
        P_InsettableShape(InsettableShape) -- extends --> P_Shape
        P_InsettableShape -- "inset(by: CGFloat)" --> P_InsettableShape
        P_ShapeStyle(ShapeStyle)
        P_Layout(Layout) -- extends --> P_Animatable(Animatable)
        P_Gesture(Gesture)
        P_Transition(Transition)
        P_Animatable(Animatable) -- "animatableData: AnimatableData" --> P_VectorArithmetic(VectorArithmetic)
        P_DynamicProperty(DynamicProperty) -- "update()" --> P_DynamicProperty
    end

    subgraph BasicViews["Common Views (Examples)"]
        V_Text(Text) -- extends --> P_View
        V_Image(Image) -- extends --> P_View
        V_Spacer(Spacer) -- extends --> P_View
        V_Group(Group) -- extends --> P_View
        V_Canvas(Canvas) -- extends --> P_View
        V_TupleView(TupleView) -- extends --> P_View
        V_AnyView(AnyView) -- extends --> P_View
        V_EmptyView(EmptyView) -- extends --> P_View
    end

    subgraph LayoutContainers["Layout Containers (Examples)"]
        LC_HStack(HStack) -- extends --> P_View
        LC_VStack(VStack) -- extends --> P_View
        LC_ZStack(ZStack) -- extends --> P_View
        LC_ForEach(ForEach) -- extends --> P_View
        LC_GeometryReader(GeometryReader) -- "provides" --> GeometryProxy(GeometryProxy)
    end

    CustomView --> V_Text
    CustomView --> LC_HStack
    LC_HStack --> V_Image
    LC_HStack --> V_Spacer

    style P_View fill:#f9f3,stroke:#333,stroke-width:2px
    style P_ViewModifier fill:#ccf3,stroke:#333,stroke-width:1px
    style P_Shape fill:#cfc3,stroke:#333,stroke-width:1px
    style P_ShapeStyle fill:#ffc3,stroke:#333,stroke-width:1px
    style P_Layout fill:#fcc3,stroke:#333,stroke-width:1px
    style P_Gesture fill:#cff3,stroke:#333,stroke-width:1px
    style P_Transition fill:#fcf3,stroke:#333,stroke-width:1px
    style P_Animatable fill:#fec3,stroke:#333,stroke-width:1px
    style P_DynamicProperty fill:#eee3,stroke:#333,stroke-width:1px
```

**Explanation:** This diagram shows the central `View` protocol and how custom views implement it. It also highlights other key protocols like `ViewModifier`, `Shape`, `ShapeStyle`, `Layout`, `Gesture`, `Transition`, `Animatable`, and `DynamicProperty`. Examples of common views and layout containers derived from `View` are included.



---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---