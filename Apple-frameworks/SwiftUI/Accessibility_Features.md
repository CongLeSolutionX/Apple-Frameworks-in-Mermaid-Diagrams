---
created: 2025-03-28 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Accessibility Features - A Diagrammatic Guide 
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---


Overview of the accessibility-related protocols and types.

```mermaid
---
title: "SwiftUI Framework - Accessibility Features"
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
    subgraph MainFeatures["Accessibility Features"]
        Acc_View(View) -- ".accessibilityChartDescriptor()" --> AXChart(AXChartDescriptorRepresentable Protocol)
        AXChart -- "makeChartDescriptor()" --> AXDesc(AXChartDescriptor)
        AXChart -- "updateChartDescriptor()" --> AXDesc
        Acc_View -- ".accessibilityCustomContent()" --> AccCustomKey(AccessibilityCustomContentKey Struct)
        Acc_View -- ".accessibilityHeading()" --> AccHeading(AccessibilityHeadingLevel Enum)
        Acc_View -- ".accessibilityTextContentType()" --> AccTextType(AccessibilityTextContentType Struct)
        Acc_View -- ".accessibility(...)" --> AccTraits(AccessibilityTraits Struct/SetAlgebra)
    end

    subgraph Details["Details"]
        AccHeading -- ".unspecified, .h1 .. .h6" --> AccHeading
        AccTextType -- ".plain, .console, .sourceCode, ..." --> AccTextType
        AccTraits -- ".isButton, .isHeader, .isSelected, ..." --> AccTraits
        AccTraits -- Set Algebra Ops --> AccTraits
        AccCustomKey -- "init(_: Text, id: String)" --> AccCustomKey
        AccCustomKey -- "init(_: LocalizedStringKey, ...)" --> AccCustomKey
    end
    
```

-----


**Explanation:** This diagram highlights the primary accessibility features mentioned in the documentation attached to the `View` protocol, including chart descriptors, custom content, heading levels, text content types, and traits.


---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---