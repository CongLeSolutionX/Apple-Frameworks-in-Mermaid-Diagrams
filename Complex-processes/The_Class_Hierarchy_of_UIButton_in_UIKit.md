---
created: 2024-12-07 04:58:55
url:
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# The Class Hierarchy of UIButton in UIKit

> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---

Below diagrams are designed to be clear, informative, and serve as useful reference documentation for developers.

### Diagram 1: UIButton Class Hierarchy

This diagram provides a clear overview of the inheritance chain for `UIButton`.

```mermaid
classDiagram
    NSObject <|-- UIResponder
    UIResponder <|-- UIView
    UIView <|-- UIControl
    UIControl <|-- UIButton
    class NSObject{
        +alloc()
        +init()
        +dealloc()
        +isKindOfClass:
        +respondsToSelector:
        +performSelector:
    }
    class UIResponder{
        +touchesBegan:withEvent:
        +touchesMoved:withEvent:
        +touchesEnded:withEvent:
        +touchesCancelled:withEvent:
        +becomeFirstResponder
        +resignFirstResponder
        +isFirstResponder
    }
    class UIView{
        +initWithFrame:
        +addSubview:
        +removeFromSuperview
        +backgroundColor
        +frame
        +bounds
        +center
        +transform
        +alpha
        +isHidden
        +setNeedsLayout
        +layoutIfNeeded
        +layoutSubviews
        +drawRect:
    }
    class UIControl{
        +addTarget:action:forControlEvents:
        +removeTarget:action:forControlEvents:
        +sendAction:to:forEvent:
        +enabled
        +selected
        +highlighted
    }
    class UIButton{
        +buttonWithType:
        +setTitle:forState:
        +setImage:forState:
        +setBackgroundImage:forState:
        +setTitleColor:forState:
        +titleLabel
        +imageView
    }
```

**Explanation:**

*   The diagram visually represents the inheritance chain, starting from the base class `NSObject` and extending to `UIButton`.
*   Each class is linked to its superclass, showing the flow of inheritance.
*   Methods are included as a representation of the functionality provided at each level of the hierarchy. (Methods listed are representative and not an exhaustive list).

### Diagram 2: UIButton Interaction and State Management

This diagram focuses on how `UIButton` inherits and utilizes features from `UIControl` to manage interactions and states.

```mermaid
graph LR
    A[User Interaction] --> B{Touch Event};
    B -- Tap --> C[UIButton];
    C --> D{UIControl Manages State};
    D -- Normal/Highlighted/Selected/Disabled --> E[Updates Appearance];
    D -- Target-Action --> F[Action Method Invoked];
    F --> G[App Logic Executes];
```

**Explanation:**

*   The diagram starts with a user interaction (a tap).
*   The `UIButton` receives the touch event.
*   `UIControl` (superclass of `UIButton`) manages the button's state (normal, highlighted, selected, disabled).
*   Based on the state, the button's appearance updates.
*   `UIControl` also handles the target-action mechanism, invoking the specified action method.
*   Finally, the app logic associated with the button's action is executed.

### Diagram 3: UIView and Responder Chain

This diagram shows how `UIButton` participates in the responder chain and utilizes `UIView` properties.

```mermaid
graph LR
    A[User Touch] --> B{"UIView (UIButton as a View)"};
    B --> C{Is Hit Testing Successful?};
    C -- Yes --> D[UIResponder Chain];
    D --> E{"Finds Appropriate Responder (UIButton or Superview)"};
    E -- Touch Event Handled --> F[Action/Animation/Layout Change];
    C -- No --> G[Event Passed to Next Responder];
```

**Explanation:**

*   The diagram starts with a user touch on the screen.
*   Since `UIButton` inherits from `UIView`, the touch event first interacts with the button as a view.
*   A hit test determines if the touch is within the bounds of the button.
*   If yes, the event is passed to the responder chain.
*   The responder chain finds the appropriate responder (e.g., the `UIButton` itself or one of its superviews).
*   The responder handles the touch event, potentially triggering an action, animation, or layout change.
*   If the hit test fails, the event is passed to the next responder in the chain.

### Diagram 4:  NSObject's Role

This simple diagram highlights the fundamental contribution of `NSObject`.

```mermaid
    graph LR
      A[UIButton] --> B{Objective-C Runtime};
      B -- Memory Management \n Introspection \n etc. --> C[NSObject];
```

**Explanation:**

*   Illustrates that `UIButton`, through its inheritance chain, relies on `NSObject` for fundamental Objective-C runtime features like memory management and introspection.

---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---