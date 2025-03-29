---
created: 2025-03-28 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Layout System - A Diagrammatic Guide 
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---


Visualizing the components involved in SwiftUI's layout process.

```mermaid
---
title: "SwiftUI Framework - Layout System"
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
    subgraph LayoutProcess["Layout Process"]
        ParentView -- "Proposes Size" --> LP_Container(Layout Container Call);
        LP_Container -- "Receives Subviews" --> SubviewsCollection(LayoutSubviews);
        SubviewsCollection -- "Contains" --> LayoutSubviewProxy(LayoutSubview);
    end

    subgraph LayoutProtocol["Layout Protocol"]
        P_Layout(Layout)
        P_Layout -- "sizeThatFits(...)" --> ReturnSize[CGSize]
        P_Layout -- "placeSubviews(...)" --> Placement[Places Subviews via Proxy]
        P_Layout -- "makeCache(...)" --> CacheData[(Cache)]
        P_Layout -- "updateCache(...)" --> CacheData
        P_Layout -- "spacing(...)" --> ViewSpacing(ViewSpacing)
        P_Layout -- "explicitAlignment(...)" --> AlignmentValue[CGFloat?]
        P_Layout -- "layoutProperties" --> LayoutProperties(LayoutProperties)

        Proto_HStackLayout(HStackLayout) -- conforms --> P_Layout
        Proto_VStackLayout(VStackLayout) -- conforms --> P_Layout
        Proto_ZStackLayout(ZStackLayout) -- conforms --> P_Layout
        Proto_AnyLayout(AnyLayout) -- conforms --> P_Layout
    end

    subgraph SubviewProxy["LayoutSubview Proxy"]
        LayoutSubviewProxy -- "sizeThatFits(_: ProposedViewSize)" --> ReturnSize
        LayoutSubviewProxy -- "dimensions(in: ProposedViewSize)" --> ViewDimensions(ViewDimensions)
        LayoutSubviewProxy -- "place(at:proposal:anchor:)" --> Placement
        LayoutSubviewProxy -- "spacing: ViewSpacing" --> ViewSpacing
        LayoutSubviewProxy -- "priority: Double" --> DoubleValue[Double]
        LayoutSubviewProxy -- "[LayoutValueKey.Type]" --> CustomValue[Key.Value]
    end

    subgraph AlignmentSystem["Alignment"]
        AS_Alignment(Alignment) --> AS_HAlign(HorizontalAlignment)
        AS_Alignment --> AS_VAlign(VerticalAlignment)
        AS_HAlign -- "init(_: AlignmentID.Type)" --> AS_AlignID(AlignmentID)
        AS_VAlign -- "init(_: AlignmentID.Type)" --> AS_AlignID
        AS_AlignID -- "defaultValue(in: ViewDimensions)" --> AlignmentValue
        ViewDimensions -- "[HorizontalAlignment]" --> AlignmentValue
        ViewDimensions -- "[VerticalAlignment]" --> AlignmentValue
    end


    LP_Container --> P_Layout
```

**Explanation:** This diagram breaks down the layout system. It shows the `Layout` protocol and its key methods/properties. It details the role of `LayoutSubviews` and `LayoutSubview` proxies for interaction. The alignment system (`Alignment`, `HorizontalAlignment`, `VerticalAlignment`, `AlignmentID`, `ViewDimensions`) is also visualized.


---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---