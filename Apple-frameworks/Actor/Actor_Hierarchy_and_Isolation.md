---
created: 2025-04-13 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Actor Hierarchy and Isolation - A Diagrammatic Guide 
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---


## Actor Hierarchy and Isolation

This diagram shows the relationship TWEEN `Actor`, `GlobalActor`, and the specific `MainActor`. It also highlights the core isolation mechanisms.

```mermaid
---
title: Actor Hierarchy and Isolation
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
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#BEF',
      'primaryTextColor': '#55ff',
      'primaryBorderColor': '#7c2',
      'lineColor': '#F8B229',
      'secondaryColor': '#EE2',
      'tertiaryColor': '#fff',
      'stroke':'#3323',
      'stroke-width': '0.5px'
    }
  }
}%%
graph TD
    subgraph Actors
        A[Actor Protocol] --> GA(GlobalActor Protocol)
        A --> P1{Properties}
        P1 --> PE[nonisolated var unownedExecutor: UnownedSerialExecutor]
        A --> M1{Methods}
        M1 --> MI1["preconditionIsolated(...)"]
        M1 --> MI2["assertIsolated(...)"]
        M1 --> MI3["assumeIsolated(...)"]

        GA --> GA_Props{Properties}
        GA_Props --> GA_Shared[static var shared: ActorType]
        GA_Props --> GA_Executor["static var sharedUnownedExecutor: UnownedSerialExecutor"]
        GA --> GA_Methods{Methods}
        GA_Methods --> GA_Pre["static preconditionIsolated(...)"]
        GA_Methods --> GA_Assert["static assertIsolated(...)"]

        MA[MainActor] --> GA
        MA --> MA_Shared["static let shared: MainActor"]
        MA --> MA_Executor["nonisolated var unownedExecutor: UnownedSerialExecutor"]
        MA --> MA_Run["static run(...)"]
        MA --> MA_Assume["static assumeIsolated(...)"]
    end

    subgraph Executors
        style Executors fill:#f9f3,stroke:#333,stroke-width:2px
        UX["UnownedSerialExecutor"]
        PE --> UX
        GA_Executor --> UX
        MA_Executor --> UX
    end

    subgraph Core Concepts
        Is[Isolation]
        A --> Is
        GA --> Is
        MI1 --> Is
        MI2 --> Is
        MI3 --> Is
        GA_Pre --> Is
        GA_Assert --> Is
    end

    style A fill:#bbf3,stroke:#333,stroke-width:2px
    style GA fill:#ccf3,stroke:#333,stroke-width:2px
    style MA fill:#ddf3,stroke:#333,stroke-width:2px
    
    
```


**Explanation:**

*   `Actor` is the base protocol.
*   `GlobalActor` builds on `Actor`, defining a shared instance (`shared`) and its associated executor (`sharedUnownedExecutor`).
*   `MainActor` is a specific, concrete `GlobalActor` provided by the system.
*   Actors ensure safety through isolation, checked via `preconditionIsolated`, `assertIsolated`, and `assumeIsolated`.
*   The `unownedExecutor` property links an actor instance to its underlying `SerialExecutor`.




---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---