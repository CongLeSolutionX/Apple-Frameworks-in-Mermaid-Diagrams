---
created: 2025-03-28 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Data Flow & State Management - A Diagrammatic Guide 
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---


Illustrating how data flows through the view hierarchy using property wrappers.

```mermaid
---
title: "SwiftUI Framework - Data Flow & State Management"
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
    subgraph SourceOfTruth["Sources of Truth"]
        State[@State] -- "Owns Value (Value Type)" --> DataValue[(Value)]
        StateObject[@StateObject] -- "Owns Object (Reference Type)" --> ObservableObject(ObservableObject)
    end

    subgraph Propagation["Propagation & Observation"]
        State -- "$property" --> Binding1[Binding<Value>]
        StateObject -- "$property" --> Binding2[ObservedObject.Wrapper] -- "Provides" --> Binding3[Binding<Property>]
        ObservedObject[@ObservedObject] -- "Observes External Object" --> ObservableObject
        ObservedObject -- "$property" --> Binding4[ObservedObject.Wrapper] -- "Provides" --> Binding3
        EnvironmentObject[@EnvironmentObject] -- "Reads from Environment" --> ObservableObject
        EnvironmentObject -- "$property" --> Binding5[ObservedObject.Wrapper] -- "Provides" --> Binding3
        Bindable[@Bindable] -- "Wraps Observable" ----> ObservableMacro(@Observable Object)
        Bindable -- "$property" --> Binding6[Binding<Property>]
        Binding[@Binding] -- "Two-way connection" --> DataValue
        Binding -- "Two-way connection" --> Property(Object Property)
    end

    subgraph EnvironmentSystem["Environment"]
        Environment[@Environment] -- "Reads keyPath" --> EnvironmentValues(EnvironmentValues)
        Environment -- "Reads Observable type" --> ObservableMacro
        EnvironmentValues -- "Contains" --> EnvValue["Key: Value"]
        EnvironmentKey(EnvironmentKey) -- "Defines" --> EnvValue
        View -- ".environment(_:_:)" --> EnvironmentValues
        View -- ".environmentObject(_:)" --> EnvironmentObject
        View -- ".environment(_:)" --> Environment
        EntryMacro["@Entry Macro"] -- "Creates" ---> EnvValue
        EntryMacro -- "Creates" ---> TransactionValue["Transaction Value"]
        EntryMacro -- "Creates" ---> ContainerValue["Container Value"]
        EntryMacro -- "Creates" ---> FocusedValue["Focused Value"]
    end

    ObservableObject -- "@Published" --> Property
    Property -- "Causes Update" --> View(View)

    style State fill:#lightblue,stroke:#333,stroke-width:2px
    style StateObject fill:#lightgreen,stroke:#333,stroke-width:2px
    style ObservedObject fill:#lightyellow,stroke:#333,stroke-width:1px
    style EnvironmentObject fill:#lightcoral,stroke:#333,stroke-width:1px
    style Environment fill:#lightgrey,stroke:#333,stroke-width:1px
    style Binding fill:#cyan,stroke:#333,stroke-width:1px
    style Bindable fill:#magenta,stroke:#333,stroke-width:1px
```

---


**Explanation:** This diagram focuses on data flow. It distinguishes between sources of truth (`@State`, `@StateObject`) and ways to propagate or observe data (`@ObservedObject`, `@EnvironmentObject`, `@Environment`, `@Binding`, `@Bindable`). The environment system (`EnvironmentValues`, `EnvironmentKey`, `@Entry`) is also shown.


---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---