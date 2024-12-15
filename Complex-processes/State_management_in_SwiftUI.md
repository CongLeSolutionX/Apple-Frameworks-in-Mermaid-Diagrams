---
created: 2024-12-07 04:58:55
url:
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
---


# State Management in SwiftUI

Below is the set of Mermaid diagrams discussing state management in SwiftUI in various perspectives.

## Overview of State Management in SwiftUI

```mermaid
graph TD
    A[State Management in SwiftUI]
    
    A --> B[Property Wrappers]
    A --> C[Combine Framework]
    A --> D[Unidirectional Data Flow]
    A --> E[MVVM Architecture]
    A --> F[Reactive Programming]
    A --> G[Swift Concurrency]
    A --> H[Data Persistence]
    A --> I[Performance Optimization]
    A --> J[Best Practices]
    
    %% Property Wrappers Subgraph
    subgraph Property_Wrappers
        B1[@State<br/>- Local State]
        B2[@Binding<br/>- Two-Way Binding]
        B3[@ObservedObject<br/>- Shared State]
        B4[@StateObject<br/>- Shared State - Single Instance]
        B5[@EnvironmentObject<br/>- Global State]
    end
    B --> Property_Wrappers
    
    %% Combine Framework Subgraph
    subgraph Combine_Framework
        C1[ObservableObject Protocol]
        C2[Publishers & Subscribers]
    end
    C --> Combine_Framework
    
    %% MVVM Architecture Subgraph
    subgraph MVVM_Architecture
        E1[Model]
        E2[View]
        E3[ViewModel]
    end
    E --> MVVM_Architecture
    
    %% Reactive Programming Subgraph
    subgraph Reactive_Programming
        F1[Automatic View Updates]
        F2[Reactive Data Flow]
    end
    F --> Reactive_Programming
    
    %% Best Practices Subgraph
    J1[Unidirectional Data Flow]
    J2[Utilize MVVM]
    J3[Leverage Combine]
    J4[Implement Swift Concurrency]
    J5[Optimize Performance]
    J --> J1
    J --> J2
    J --> J3
    J --> J4
    J --> J5
    
    %% Styling
    classDef main fill:#FF8C00,stroke:#333,stroke-width:2px, color:#000000;
    classDef sub fill:#FFA500,stroke:#333,stroke-width:1.5px, color:#000000;
    classDef subNode fill:#FFD580,stroke:#333,stroke-width:1px, color:#000000;
    class A main;
    class B,C,D,E,F,G,H,I,J sub;
    class B1,B2,B3,B4,B5,C1,C2,E1,E2,E3,F1,F2,J1,J2,J3,J4,J5 subNode;
```

---

Another style



```mermaid
graph TD
    A[State Management in SwiftUI] --> B{Core Concepts};
    
    B --> C[Declarative Approach]:::Core_Concepts_Detail;
    C --> CA["UI as a function of its state"]:::Core_Concepts_Detail_More;
    C --> CB["Dynamic and responsive"]:::Core_Concepts_Detail_More;
    
    B --> D[Unidirectional Data Flow]:::Core_Concepts_Detail;
    D --> DA["Data flows from parent to child"]:::Core_Concepts_Detail_More;
    D --> DB["Simplifies state management"]:::Core_Concepts_Detail_More;
    D --> DC["Predictable data flow"]:::Core_Concepts_Detail_More;
    
    B --> E[Reactive Updates]:::Core_Concepts_Detail;
    E --> EA["Views update automatically on state changes"]:::Core_Concepts_Detail_More;
    E --> EB["No imperative updates"]:::Core_Concepts_Detail_More;
 
    A --> F{Property Wrappers}:::Property_Wrappers;
    F--> G[@State]:::Property_Wrappers_Detail;
    G--> GA["Local, simple state in a single view"]:::Property_Wrappers_Detail_More;
    G--> GB["Transient"]:::Property_Wrappers_Detail_More;
    		
    F--> H[@Binding]:::Property_Wrappers_Detail;
    H--> HA["Two-way connection between parent and child views"]:::Property_Wrappers_Detail_More;
    H--> HB["Child can read and write parent’s state"]:::Property_Wrappers_Detail_More;

    F--> I[@ObservedObject]:::Property_Wrappers_Detail;
    I--> IA["External object conforming to ObservableObject"]:::Property_Wrappers_Detail_More;
    I--> IB["Views update when published properties change"]:::Property_Wrappers_Detail_More;
            
    F--> J[@StateObject]:::Property_Wrappers_Detail;
    J--> JA["Similar to ObservedObject"]:::Property_Wrappers_Detail_More;
    J--> JB["Object instantiated only once in the view’s lifecycle"]:::Property_Wrappers_Detail_More;
	J--> JC["Ensures single source of truth"]:::Property_Wrappers_Detail_More;
            
    	
    F--> K[@EnvironmentObject]:::Property_Wrappers_Detail;
    K--> KA["State shared across multiple views"]:::Property_Wrappers_Detail_More;
    K--> KB["No need to explicitly pass the data"]:::Property_Wrappers_Detail_More;
    K--> KC["Accessible throughout the app’s environment"]:::Property_Wrappers_Detail_More;
    
    A --> L{Combine Framework}:::Combine_framework;
    L --> LA["Handles asynchronous events using publishers and subscribers"]:::Combine_framework_Detail;
    L --> LB["Used with ObservableObject to manage state changes"]:::Combine_framework_Detail;

    A --> M{Architecture Patterns}:::Architecture_Patterns;
    M --> N["MVVM (Model-View-ViewModel)"]:::Architecture_Patterns_Detail;
    N --> NA["Separates View, ViewModel, and Model"]:::Architecture_Patterns_Detail_More;
    N --> NB["Enhances testability"]:::Architecture_Patterns_Detail_More;
    N --> NC["Promotes maintainability"]:::Architecture_Patterns_Detail_More;
            
    A --> O{Swift Concurrency}:::Swift_Concurrency;
    O --> OA["Handles asynchronous operations more seamlessly"]:::Swift_Concurrency_More;
    O --> OB["Improves code readability"]:::Swift_Concurrency_More;
    O --> OC["Enhances performance"]:::Swift_Concurrency_More;

    A --> P{Data Persistence}:::Data_Persistence;
    P --> PA["Persists state using CoreData, UserDefaults, etc"]:::Data_Persistence_More;
	P --> PB["Maintains state across launches"]:::Data_Persistence_More;
    
    A --> Q{Performance Optimization}:::Performance_Optimization;
    Q --> QA["Reduces view re-renders"]:::Performance_Optimization_More;
    Q --> QB["Minimizes memory usage"]:::Performance_Optimization_More;
	Q --> QC["Profile with Instruments"]:::Performance_Optimization_More;

%% Style for Core Concepts
classDef Core_Concepts fill:#20ff,stroke:#333,stroke-width:2px
class B Core_Concepts

classDef Core_Concepts_Detail fill:#25ff,stroke:#333,stroke-width:2px
classDef Core_Concepts_Detail_More fill:#29ff,stroke:#333,stroke-width:2px

%% Style for Property Wrappers
classDef Property_Wrappers fill:#132,stroke:#333,stroke-width:2px
classDef Property_Wrappers_Detail fill:#152,stroke:#333,stroke-width:2px
classDef Property_Wrappers_Detail_More fill:#192,stroke:#333,stroke-width:2px

%% Style for Property Wrappers
classDef Combine_framework fill:#912,stroke:#333,stroke-width:2px
classDef Combine_framework_Detail fill:#912,stroke:#333,stroke-width:2px

%% Style for Architecture Patterns
classDef Architecture_Patterns fill:#942,stroke:#333,stroke-width:2px
classDef Architecture_Patterns_Detail fill:#952,stroke:#333,stroke-width:2px
classDef Architecture_Patterns_Detail_More fill:#972,stroke:#333,stroke-width:2px

%% Style for Swift Concurrency
classDef Swift_Concurrency fill:#382,stroke:#333,stroke-width:2px
classDef Swift_Concurrency_More fill:#362,stroke:#333,stroke-width:2px

%% Style for Data Persistence
classDef Data_Persistence fill:#6266,stroke:#333,stroke-width:2px
classDef Data_Persistence_More fill:#6466,stroke:#333,stroke-width:2px

%% Style for Performance Optimization
classDef Performance_Optimization fill:#256,stroke:#333,stroke-width:2px
classDef Performance_Optimization_More fill:#266,stroke:#333,stroke-width:2px

```

---




## State management using native property wrappers

```mermaid
graph TD
    A[State Management <br> using built-in property wrappers] --> B[@State]
    A --> C[@Binding]
    A --> D[@ObservedObject]
    A --> E[@StateObject]
    A --> F[@EnvironmentObject]
	
	B --> G[Transient state within a single view.]
	C --> H[Two-way data binding between views.]
	D --> I[External observable data objects.]
	E --> J[Ensures single lifecycle for observable objects.]
	F --> K[Globally accessible data through the app's environment.]

```
