---
created: 2025-03-28 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Gestures - A Diagrammatic Guide 
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---


This diagram shows the gesture recognition system.

```mermaid
---
title: "SwiftUI Framework - Gesturess"
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
    subgraph GestureProtocol["Gesture Protocol"]
        GP_Gesture(Gesture Protocol) -- "<Value>" --> GP_ValueType[Value Type]
        GP_Gesture -- "body: Body" --> GP_Gesture
        GP_AnyGesture(AnyGesture<Value>) -- "Type-erases" --> GP_Gesture
    end

    subgraph ConcreteGestures["Concrete Gestures (Examples)"]
        CG_Tap(TapGesture) -- "Value: Void" --> GP_Gesture
        CG_LongPress(LongPressGesture) -- "Value: Bool" --> GP_Gesture
        CG_Drag(DragGesture) -- "Value: DragGesture.Value" --> GP_Gesture
        CG_Magnification(MagnificationGesture) -- "Value: CGFloat" --> GP_Gesture
        CG_Rotation(RotationGesture) -- "Value: Angle" --> GP_Gesture
    end

    subgraph GestureCombinators["Gesture Combinators"]
        GC_Simultaneous(SimultaneousGesture<G1, G2>) -- "Wraps G1, G2" --> GP_Gesture
        GC_Exclusive(ExclusiveGesture<G1, G2>) -- "Wraps G1, G2 (G1 priority)" --> GP_Gesture
        GC_Sequence(SequenceGesture<G1, G2>) -- "Wraps G1, G2 (G1 then G2)" --> GP_Gesture
        GP_Gesture -- ".simultaneously(with:)" --> GC_Simultaneous
        GP_Gesture -- ".exclusively(before:)" --> GC_Exclusive
        GP_Gesture -- ".sequenced(before:)" --> GC_Sequence
    end

    subgraph GestureModifiers["Gesture Modifiers"]
        GM_View(View) -- ".gesture(_:including:)" --> GP_Gesture
        GM_View -- ".highPriorityGesture(_:including:)" --> GP_Gesture
        GM_View -- ".simultaneousGesture(_:including:)" --> GP_Gesture
        GP_Gesture -- ".onChanged((Value)->Void)" --> GM_Changed(_ChangedGesture)
        GP_Gesture -- ".onEnded((Value)->Void)" --> GM_Ended(_EndedGesture)
        GP_Gesture -- ".map((Value)->T)" --> GM_Map(_MapGesture)
        GM_Changed -- conforms --> GP_Gesture
        GM_Ended -- conforms --> GP_Gesture
        GM_Map -- conforms --> GP_Gesture
    end

    subgraph AssociatedTypes["Associated Types/Enums"]
        AT_GestureMask(GestureMask OptionSet) -- ".none, .gesture, .subviews, .all" --> AT_GestureMask
        AT_DragValue(DragGesture.Value) -- ".time, .location, .startLocation, .translation, .predictedEndTranslation" --> AT_DragValue
        EventModifiers(EventModifiers OptionSet) -- ".shift, .control, .option, .command, ..." --> EventModifiers
    end

    GM_View -- uses --> AT_GestureMask
    
```

---


**Explanation:** This diagram outlines the Gesture system. It shows the base `Gesture` protocol, concrete gesture types, ways to combine gestures (`SimultaneousGesture`, `ExclusiveGesture`, `SequenceGesture`), and how gestures are attached to views using modifiers. Callback modifiers (`onChanged`, `onEnded`) are also included.


---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---