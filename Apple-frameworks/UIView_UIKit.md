---
created: 2024-12-07 04:58:55
url: https://developer.apple.com/documentation/UIKit
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---

# UIView - UIKit framework
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---

Below is a comprehensive and organized set of Mermaid diagrams of `UIView` class in the `UIKit` framework.  These diagram will cover in depth to understand the `UIView`'s structure, functionalities, and relationships within the `UIKit` framework.

---

## **1. Class Structure and Hierarchy**

### **a. Core Class Diagram**
- **Purpose**: Illustrate the primary structure of `UIView`, including its properties, methods, and related enumerations.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Properties**: Key attributes like `frame`, `bounds`, `backgroundColor`, etc.
  - **Methods**: Essential functions like initializers, `addSubview()`, `removeFromSuperview()`, etc.
  - **Enumerations**: Nested enums such as `AutoresizingMask`, `ContentMode`, `AnimationOptions`.

```mermaid
classDiagram
    class UIView {
        +frame: CGRect
        +bounds: CGRect
        +center: CGPoint
        +transform: CGAffineTransform
        +backgroundColor: UIColor?
        +alpha: CGFloat
        +isHidden: Bool
        +isUserInteractionEnabled: Bool
        +clipsToBounds: Bool
        +addSubview(_ view: UIView)
        +removeFromSuperview()
        +layoutSubviews()
        +draw(_ rect: CGRect)
        +init(frame: CGRect)
        // Additional properties and methods...
    }

    class AutoresizingMask {
        <<enum>>
        +flexibleWidth
        +flexibleHeight
        +flexibleTopMargin
        +flexibleBottomMargin
        +flexibleLeftMargin
        +flexibleRightMargin
    }

    class ContentMode {
        <<enum>>
        +scaleToFill
        +scaleAspectFit
        +scaleAspectFill
        +redraw
        +center
        +top
        +bottom
        +left
        +right
        +topLeft
        +topRight
        +bottomLeft
        +bottomRight
    }

    class AnimationOptions {
        <<enum>>
        +curveEaseInOut
        +curveEaseIn
        +curveEaseOut
        +curveLinear
        +transitionNone
        +transitionFlipFromLeft
        +transitionFlipFromRight
        +transitionCurlUp
        +transitionCurlDown
        +transitionCrossDissolve
        +transitionFlipFromTop
        +transitionFlipFromBottom
        // Additional animation options...
    }

    UIView --> AutoresizingMask
    UIView --> ContentMode
    UIView --> AnimationOptions
```

---

## **2. Initializers Overview**

### **a. Initialization Methods Diagram**
- **Purpose**: Break down the various ways to instantiate `UIView`.
- **Diagram Type**: `flowchart` (`graph LR`)
- **Contents**:
  - **Frame-Based Initializers**: `init(frame:)`
  - **Coder-Based Initializers**: `init?(coder:)`
  - **Custom Initializers**: Extensions and convenience initializers.

```mermaid
graph LR
    A[UIView Initializers] --> B[Frame-Based]
    A --> C[Coder-Based]
    A --> D[Custom Initializers]

    B --> B1["init(frame: CGRect)"]
    
    C --> C1["init?(coder: NSCoder)"]
    
    D --> D1["convenience init()"]
    D --> D2["convenience init(backgroundColor: UIColor)"]
    D --> D3["convenience init(alpha: CGFloat)"]
```

---

## **3. Properties Breakdown**

### **a. Key Properties Diagram**
- **Purpose**: Detail the main properties of `UIView`.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Geometry**: `frame`, `bounds`, `center`, `transform`
  - **Appearance**: `backgroundColor`, `alpha`, `isHidden`, `clipsToBounds`
  - **Layout**: `autoresizingMask`, `contentMode`, `semanticContentAttribute`
  - **Interaction**: `isUserInteractionEnabled`, `gestureRecognizers`
  - **Layer Management**: `layer`, `mask`

```mermaid
graph LR
    A[UIView Properties] --> B[Geometry]
    A --> C[Appearance]
    A --> D[Layout]
    A --> E[Interaction]
    A --> F[Layer Management]

    B --> B1[frame: CGRect]
    B --> B2[bounds: CGRect]
    B --> B3[center: CGPoint]
    B --> B4[transform: CGAffineTransform]

    C --> C1[backgroundColor: UIColor?]
    C --> C2[alpha: CGFloat]
    C --> C3[isHidden: Bool]
    C --> C4[clipsToBounds: Bool]

    D --> D1[autoresizingMask: AutoresizingMask]
    D --> D2[contentMode: ContentMode]
    D --> D3[semanticContentAttribute: UISemanticContentAttribute]

    E --> E1[isUserInteractionEnabled: Bool]
    E --> E2["gestureRecognizers: [UIGestureRecognizer]?"]

    F --> F1[layer: CALayer]
    F --> F2[mask: UIView?]
    
```

---

## **4. Methods Grouped by Functionality**

### **a. View Hierarchy Management Methods**
- **Purpose**: Categorize methods based on managing the view hierarchy.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Subview Management**: `addSubview()`, `insertSubview(_:at:)`, `bringSubviewToFront()`, `sendSubviewToBack()`
  - **Layout Management**: `setNeedsLayout()`, `layoutIfNeeded()`, `layoutSubviews()`
  - **Rendering**: `setNeedsDisplay()`, `draw(_:)`
  - **Clipping and Masks**: `clipsToBounds`, `mask`

```mermaid
flowchart TD
    A[UIView Methods] --> B[View Hierarchy Management]
    A --> C[Layout Management]
    A --> D[Rendering]
    A --> E[Clipping and Masks]

    B --> B1["addSubview(_ view: UIView)"]
    B --> B2["insertSubview(_ view: UIView, at index: Int)"]
    B --> B3["bringSubviewToFront(_ view: UIView)"]
    B --> B4["sendSubviewToBack(_ view: UIView)"]

    C --> C1["setNeedsLayout()"]
    C --> C2["layoutIfNeeded()"]
    C --> C3["layoutSubviews()"]

    D --> D1["setNeedsDisplay()"]
    D --> D2["draw(_ rect: CGRect)"]

    E --> E1["clipsToBounds: Bool"]
    E --> E2["mask: UIView?"]
```

### **b. Gesture Handling Methods**
- **Purpose**: Outline methods related to gesture recognition and handling.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Adding Gestures**: `addGestureRecognizer()`
  - **Removing Gestures**: `removeGestureRecognizer()`
  - **Gesture Recognizer Events**: Handling callbacks and actions.

```mermaid
flowchart TD
    A[Gesture Handling Methods] --> B[Adding Gestures]
    A --> C[Removing Gestures]
    A --> D[Gesture Recognizer Events]

    B --> B1["addGestureRecognizer(_ gesture: UIGestureRecognizer)"]
    
    C --> C1["removeGestureRecognizer(_ gesture: UIGestureRecognizer)"]

    D --> D1["Handling gesture callbacks and actions"]
```

### **c. Animation Methods**
- **Purpose**: Categorize methods that facilitate view animations.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Basic Animations**: `animate(withDuration:animations:)`
  - **Spring Animations**: `animate(withDuration:delay:usingSpringWithDamping:initialSpringVelocity:options:animations:completion:)`
  - **Transition Animations**: `transition(with:duration:options:animations:completion:)`

```mermaid
flowchart TD
    A[Animation Methods] --> B[Basic Animations]
    A --> C[Spring Animations]
    A --> D[Transition Animations]

    B --> B1["animate(withDuration: TimeInterval, animations: () -> Void)"]

    C --> C1["animate(withDuration: TimeInterval, delay: TimeInterval, usingSpringWithDamping: CGFloat, initialSpringVelocity: CGFloat, options: UIView.AnimationOptions, animations: () -> Void, completion: ((Bool) -> Void)?)"]

    D --> D1["transition(with view: UIView, duration: TimeInterval, options: UIView.AnimationOptions, animations: (() -> Void)?, completion: ((Bool) -> Void)?)"]
```

---

## **5. Enumerations and Configurations**

### **a. Enumerations Diagram**
- **Purpose**: Highlight the enums used within `UIView` and their possible values.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **AutoresizingMask**
  - **ContentMode**
  - **SemanticContentAttribute**
  - **AnimationOptions**

```mermaid
classDiagram
    class UIView {
        <<enumeration>> AutoresizingMask
        <<enumeration>> ContentMode
        <<enumeration>> SemanticContentAttribute
        <<enumeration>> AnimationOptions
    }

    class AutoresizingMask {
        +flexibleWidth
        +flexibleHeight
        +flexibleTopMargin
        +flexibleBottomMargin
        +flexibleLeftMargin
        +flexibleRightMargin
    }

    class ContentMode {
        +scaleToFill
        +scaleAspectFit
        +scaleAspectFill
        +redraw
        +center
        +top
        +bottom
        +left
        +right
        +topLeft
        +topRight
        +bottomLeft
        +bottomRight
    }

    class SemanticContentAttribute {
        +forceLeftToRight
        +forceRightToLeft
        +unspecified
        +playback
        +spatial
    }

    class AnimationOptions {
        +curveEaseInOut
        +curveEaseIn
        +curveEaseOut
        +curveLinear
        +transitionNone
        +transitionFlipFromLeft
        +transitionFlipFromRight
        +transitionCurlUp
        +transitionCurlDown
        +transitionCrossDissolve
        +transitionFlipFromTop
        +transitionFlipFromBottom
        // Additional animation options...
    }

    UIView --> AutoresizingMask
    UIView --> ContentMode
    UIView --> SemanticContentAttribute
    UIView --> AnimationOptions
```

### **b. Configuration Classes Diagram**
- **Purpose**: Show the relationship between `UIView` and its configuration classes.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **UIView.Configuration**
  - **UIVisualEffect**
  - **UIGestureRecognizer**

```mermaid
classDiagram
    class UIView {
        +configuration: UIView.Configuration
    }

    class Configuration {
        // Placeholder for configuration properties
    }

    class UIVisualEffect {
        // Visual effect properties
    }

    class UIGestureRecognizer {
        // Gesture recognizer properties
    }

    UIView --> Configuration
    UIView --> UIVisualEffect
    UIView --> UIGestureRecognizer
```

---

## **6. Protocol Conformances**

### **a. Protocols Diagram**
- **Purpose**: Display the protocols that `UIView` conforms to and their impact.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **NSCoding**
  - **UIAppearance**
  - **UITraitEnvironment**
  - **UIKeyInput**

```mermaid
classDiagram
    class UIView {
        <<open class>>
    }

    class NSCoding {
        <<protocol>>
    }

    class UIAppearance {
        <<protocol>>
    }

    class UITraitEnvironment {
        <<protocol>>
    }

    class UIKeyInput {
        <<protocol>>
    }

    UIView ..|> NSCoding
    UIView ..|> UIAppearance
    UIView ..|> UITraitEnvironment
    UIView ..|> UIKeyInput
```

---

## **7. Relationships with Other Classes**

### **a. Related Classes Diagram**
- **Purpose**: Illustrate how `UIView` interacts with other UIKit classes and frameworks.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **UIViewController**: Manages views.
  - **CALayer**: Handles lower-level rendering.
  - **UIGraphicsContext**: Drawing contexts.
  - **UILayoutGuide**: Layout management.
  - **UIStackView**: Arranged subviews.
  - **UIGestureRecognizer**: Gesture handling.
  - **UIScreen**: Device screen information.
  - **UIColor**: Color management.

```mermaid
flowchart TD
    A[UIView] --> B[UIViewController]
    A --> C[CALayer]
    A --> D[UIGraphicsContext]
    A --> E[UILayoutGuide]
    A --> F[UIStackView]
    A --> G[UIGestureRecognizer]
    A --> H[UIScreen]
    A --> I[UIColor]

    B --> |manages| A
    C --> |renders| A
    D --> |drawing context| A
    E --> |layout management| A
    F --> |arranged subviews| A
    G --> |handles gestures| A
    H --> |provides screen info| A
    I --> |applies colors| A
```

---

## **8. Extensions and Additional Functionalities**

### **a. UIView Extensions Diagram**
- **Purpose**: Showcase the additional functionalities provided through extensions.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Frame Manipulation**
  - **Animations**
  - **Shadow and Border Customizations**
  - **Gesture Recognizers Integration**

```mermaid
classDiagram
    class UIView {
        <<open class>>
    }

    class UIViewExtensions {
        <<extension>>
        +func setCornerRadius(_ radius: CGFloat)
        +func setShadow(color: UIColor, opacity: Float, offset: CGSize, radius: CGFloat)
        +func addTapGestureRecognizer(target: Any, action: Selector)
        +func animateFadeIn(duration: TimeInterval)
        +func animateFadeOut(duration: TimeInterval)
        // Additional extended methods
    }

    UIView <-- UIViewExtensions
```

### **b. Extensions Functionalities Flowchart**
- **Purpose**: Detail specific extended methods and their purposes.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Frame Manipulations**
  - **Shadow and Border Customizations**
  - **Gesture Recognizers**
  - **Animations Enhancements**

```mermaid
flowchart LR
    A[UIView Extensions] --> B[Frame Manipulations]
    A --> C[Shadow and Border Customizations]
    A --> D[Gesture Recognizers]
    A --> E[Animations Enhancements]

    B --> B1["setCornerRadius(_ radius: CGFloat)"]
    
    C --> C1["setShadow(color: UIColor, opacity: Float, offset: CGSize, radius: CGFloat)"]
    
    D --> D1["addTapGestureRecognizer(target: Any, action: Selector)"]
    
    E --> E1["animateFadeIn(duration: TimeInterval)"]
    E --> E2["animateFadeOut(duration: TimeInterval)"]
```

---

## **9. Lifecycle and Use Cases**

### **a. Lifecycle Flowchart**
- **Purpose**: Demonstrate the typical lifecycle of a `UIView` within an application.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Initialization**
  - **Adding to View Hierarchy**
  - **Layout Cycle**
  - **Rendering**
  - **Interaction**
  - **Removal from Hierarchy**

```mermaid
flowchart TD
    Start[Start] --> Init[Initialize UIView]
    Init --> Add[Add to View Hierarchy]
    Add --> Layout[Layout Cycle]
    Layout --> Render[Render on Screen]
    Render --> Interaction[Handle User Interaction]
    Interaction --> Update[Update Changes]
    Update --> Render
    Interaction --> Remove[Remove from Hierarchy]
    Remove --> End[End]
```

### **b. Common Use Cases Diagram**
- **Purpose**: Outline the typical scenarios where `UIView` is utilized.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Displaying Content**
  - **Handling User Interaction**
  - **Animating Transitions**
  - **Custom Drawing**
  - **Managing Layouts**
  - **Embedding Subviews**

```mermaid
flowchart TD
    A[UIView Use Cases] --> B[Displaying Content]
    A --> C[Handling User Interaction]
    A --> D[Animating Transitions]
    A --> E[Custom Drawing]
    A --> F[Managing Layouts]
    A --> G[Embedding Subviews]

    B --> B1["Show images, labels, buttons"]
    C --> C1["Respond to taps, swipes"]
    D --> D1["Animate alpha, frame changes"]
    E --> E1["Override draw(_:) for custom graphics"]
    F --> F1["Auto Layout constraints, stack views"]
    G --> G1["Add buttons, labels as subviews"]
```

---

## **10. Feature Availability Timeline**

### **a. Feature Availability Gantt Chart**
- **Purpose**: Show when various `UIView` features were introduced across iOS versions.
- **Diagram Type**: `gantt`
- **Contents**:
  - **iOS Versions**: 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0, 11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0
  - **Features Introduced**: Auto Layout, Gesture Recognizers, UIAppearance, LayoutMargins, Safe Area Layout Guides, Drag and Drop, Context Menus, etc.

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title UIView Feature Availability

    section iOS 2.0
    Basic UIView Initialization          :done, des1, 2008-07-11, 2008-07-11

    section iOS 3.0
    Gesture Recognizers                  :done, des2, 2009-06-17, 2009-06-17

    section iOS 4.0
    Autoresizing Masks                   :done, des3, 2010-06-21, 2010-06-21

    section iOS 5.0
    UIAppearance Protocol                :done, des4, 2011-10-12, 2011-10-12

    section iOS 6.0
    LayoutMargins                        :done, des5, 2012-09-19, 2012-09-19

    section iOS 7.0
    Advanced Animations                  :done, des6, 2013-09-18, 2013-09-18

    section iOS 8.0
    Safe Area Layout Guides              :done, des7, 2014-09-17, 2014-09-17

    section iOS 9.0
    UIVisualEffectView Enhancements      :done, des8, 2015-09-16, 2015-09-16

    section iOS 10.0
    UILayoutGuide Enhancements           :done, des9, 2016-09-19, 2016-09-19

    section iOS 11.0
    Drag and Drop Support                :done, des10, 2017-09-19, 2017-09-19

    section iOS 13.0
    Context Menus                        :done, des11, 2019-09-19, 2019-09-19

    section iOS 15.0
    Layout Enhancements                  :done, des12, 2021-09-20, 2021-09-20

    section iOS 16.0
    Multiple Window Support              :done, des13, 2022-09-12, 2022-09-12

    section iOS 17.0
    Advanced Rendering Techniques         :done, des14, 2023-09-18, 2023-09-18
```

---

## **11. Data Handling and Formats**

### **a. View State Management Diagram**
- **Purpose**: Explain how `UIView` handles different states and data representations.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **State Preservation**: `encodeRestorableState(with:)`, `decodeRestorableState(with:)`
  - **Snapshotting**: `snapshotView(afterScreenUpdates:)`, `resizableSnapshotView(from:afterScreenUpdates:withCapInsets:)`
  - **Accessibility Data**: `accessibilityLabel`, `accessibilityHint`, `accessibilityValue`

```mermaid
graph LR
    A[UIView Data Handling] --> B{State Management}
    A --> C{Snapshotting}
    A --> D{Accessibility Data}

    B --> B1["encodeRestorableState(with coder: NSCoder)"]
    B --> B2["decodeRestorableState(with coder: NSCoder)"]

    C --> C1["snapshotView(afterScreenUpdates: Bool) -> UIView?"]
    C --> C2["resizableSnapshotView(from rect: CGRect, afterScreenUpdates: Bool, withCapInsets insets: UIEdgeInsets) -> UIView?"]

    D --> D1["accessibilityLabel: String?"]
    D --> D2["accessibilityHint: String?"]
    D --> D3["accessibilityValue: String?"]
```

---

## **12. Integration with Drawing Contexts**

### **a. Drawing Methods Usage Diagram**
- **Purpose**: Show how `UIView` methods are used within drawing contexts.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Custom Drawing**: `draw(_:)`
  - **Snapshotting**: `snapshotView(afterScreenUpdates:)`
  - **Rendering Layers**: `layer.render(in:)`

```mermaid
flowchart TD
    UIView -->|Custom Drawing| DrawCustom["draw(_ rect: CGRect)"]
    UIView -->|Snapshotting| Snapshot["snapshotView(afterScreenUpdates: Bool)"]
    UIView -->|Rendering Layers| RenderLayer["layer.render(in: CGContext)"]

    DrawCustom -->|Override for custom graphics| Usage1[Implement custom drawing logic]
    Snapshot -->|Create snapshot view| Usage2[Capture current view state]
    RenderLayer -->|Render CALayer contents| Usage3[Render layer into context]
```

---

## **13. Summary and Best Practices**

### **a. Summary Diagram**
- **Purpose**: Provide a high-level overview of `UIView`'s key characteristics and functionalities.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Versatile Initialization**
  - **Robust Layout System**
  - **Advanced Rendering Options**
  - **Gesture and Interaction Handling**
  - **Performance Optimizations**
  - **Accessibility Support**
  - **Seamless Integration**

```mermaid
graph LR
    A[UIView] --> B[Versatile Initialization]
    A --> C[Robust Layout System]
    A --> D[Advanced Rendering Options]
    A --> E[Gesture and Interaction Handling]
    A --> F[Performance Optimizations]
    A --> G[Accessibility Support]
    A --> H[Seamless Integration]

    B --> B1[Multiple Initializers]
    C --> C1[Auto Layout, Stack Views]
    D --> D1[Custom Drawing, Animations]
    E --> E1[Gesture Recognizers, User Interaction]
    F --> F1[Efficient Rendering, Snapshotting]
    G --> G1[Accessibility Labels, Hints]
    H --> H1[Integration with View Controllers, Layers]
```


---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---