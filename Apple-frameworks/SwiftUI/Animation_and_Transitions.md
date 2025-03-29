---
created: 2025-03-28 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Animation & Transitions - A Diagrammatic Guide 
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---


Illustrating the animation and transition systems in SwiftUI.

```mermaid
---
title: "SwiftUI Framework - Animation & Transitions"
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
    subgraph AnimationSystem["Animation System"]
        A_Animatable(Animatable Protocol) -- "animatableData" --> A_VectorArithmetic(VectorArithmetic Protocol)
        AnimatablePair -- conforms --> A_VectorArithmetic
        EmptyAnimatableData -- conforms --> A_VectorArithmetic
        CGFloat -- conforms --> A_VectorArithmetic
        Double -- conforms --> A_VectorArithmetic
        CGPoint -- conforms --> A_Animatable
        CGSize -- conforms --> A_Animatable
        CGRect -- conforms --> A_Animatable
        Angle -- conforms --> A_Animatable
        Color.Resolved -- conforms --> A_Animatable
        AnimatablePair -- "<First: VA, Second: VA>" --> AnimatablePair

        A_Animation(Animation Struct)
        A_Animation -- "Types" --> ATypes{EaseIn, EaseOut, EaseInOut, Linear, Spring, TimingCurve, Custom}
        A_Animation -- "Modifiers" --> AMods["delay(), speed(), repeatCount(), repeatForever()"]
        A_Spring(Spring Struct)
        A_SpringKeyframe(SpringKeyframe<Value>) -- uses --> A_Spring
        A_CustomAnimation(CustomAnimation Protocol) -- "animate(...)" --> A_AnimationContext(AnimationContext)
        A_Animation -- "init(CustomAnimation)" --> A_CustomAnimation
        A_AnimationContext -- "state: AnimationState" --> A_AnimationState(AnimationState)
        A_AnimationState -- "[AnimationStateKey.Type]" --> AS_Value[Key.Value]
        A_AnimationStateKey(AnimationStateKey Protocol) -- "Defines" --> AS_Value
        A_View(View) -- ".animation(_:value:)" --> A_Animation
        Global_withAnimation["withAnimation { ... }"] -- "Applies" --> A_Animation
    end

    subgraph TransitionSystem["Transition System"]
       T_Transition(Transition Protocol) -- "body(content:phase:)" --> T_View(View)
       T_Transition -- "properties" --> T_Properties(TransitionProperties)
       T_Phase(TransitionPhase Enum) -- ".willAppear, .identity, .didDisappear" --> T_Phase
       T_AnyTransition(AnyTransition Struct) -- "Type-erases" --> T_Transition
       T_AnyTransition -- "Types" --> TTypes{identity, opacity, scale, move, offset, slide, push, modifier, asymmetric}
       T_AnyTransition -- "Modifiers" --> TMods["animation(), combined(with:)"]
       T_View(View) -- ".transition(_:)" --> T_AnyTransition
       T_View -- ".transition(_:)" --> T_Transition
       T_Asymmetric(AsymmetricTransition<I, R>) -- conforms --> T_Transition
       T_Concrete["Concrete Transitions (Examples)"] -- "IdentityTransition, OpacityTransition, ScaleTransition, MoveTransition, OffsetTransition, SlideTransition, PushTransition, BlurReplaceTransition" --> T_Concrete
       T_Concrete -- conforms --> T_Transition
    end

    subgraph KeyframeAnimation["Keyframe Animation"]
        KA_Animator(KeyframeAnimator<V, KP, C>) -- uses --> KA_Timeline(KeyframeTimeline<Value>)
        KA_Timeline -- "init(content: @KeyframesBuilder)" --> KA_Keyframes(Keyframes Protocol)
        KA_Keyframes -- "body: @KeyframesBuilder" --> KA_Keyframes
        KA_Track(KeyframeTrack<R, V, C>) -- conforms --> KA_Keyframes
        KA_Track -- "content: @KeyframeTrackContentBuilder" --> KA_TrackContent(KeyframeTrackContent Protocol)
        KA_TrackContent -- "body: @KeyframeTrackContentBuilder" --> KA_TrackContent
        KA_Cubic(CubicKeyframe<Value>) -- conforms --> KA_TrackContent
        KA_Linear(LinearKeyframe<Value>) -- conforms --> KA_TrackContent
        KA_Spring(SpringKeyframe<Value>) -- conforms --> KA_TrackContent
        KA_Move(MoveKeyframe<Value>) -- conforms --> KA_TrackContent
        A_Animatable -- "Used by" --> KA_TrackContent
    end

    subgraph ContentTransitionSystem["Content Transition"]
        CT_ContentTransition(ContentTransition Struct) -- ".identity, .opacity, .interpolate, .numericText" --> CT_ContentTransition
        CT_View(View) -- ".contentTransition(_:)" --> CT_ContentTransition
    end

    A_Animation --> T_AnyTransition -- ".animation(...)"
    A_Animation --> A_SpringKeyframe

```

----


**Explanation:** This diagram covers animation and transitions. It shows the `Animatable` protocol and related types (`VectorArithmetic`, `AnimatablePair`). It details the `Animation` struct, its types, and modifiers. The `Transition` system (`AnyTransition`, specific transitions, `TransitionPhase`) is outlined. Keyframe animations (`KeyframeAnimator`, `KeyframeTimeline`, `Keyframes`, `KeyframeTrack`) and Content Transitions are also included.


---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---