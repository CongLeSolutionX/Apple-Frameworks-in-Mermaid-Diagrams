---
created: 2024-12-07 04:49:40
reference_url: https://developer.apple.com/documentation/quartzcore
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---

# Core Animation


## **1. Class Structure and Hierarchy**

### **a. Core Class Diagram**
- **Purpose**: Illustrate the primary structure of the Core Animation framework, including its main classes, properties, methods, and relationships.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Classes**: `CALayer`, `CAAnimation`, `CAShapeLayer`, `CATransform3D`, `CATransaction`, etc.
  - **Properties**: Key attributes like `bounds`, `position`, `opacity`, etc.
  - **Methods**: Essential functions like `addAnimation`, `removeAllAnimations`, etc.
  - **Enumerations**: Nested enums such as `CAMediaTimingFunctionName`, `CAFillMode`, `CATransitionType`, etc.

```mermaid
classDiagram
    class CALayer {
        +CGRect bounds
        +CGPoint position
        +CGFloat opacity
        +UIColor backgroundColor
        +CGSize shadowOffset
        +CGFloat shadowRadius
        +CGColor shadowColor
        +CGFloat cornerRadius
        +init()
        +addSublayer(CALayer layer)
        +removeFromSuperlayer()
        +layoutIfNeeded()
        // Additional properties and methods...
    }

    class CAAnimation {
        +String keyPath
        +CFTimeInterval duration
        +CFTimeInterval beginTime
        +Float repeatCount
        +CAMediaTimingFunction timingFunction
        +CAEasingFunction easingFunction
        +init()
        +start()
        +stop()
        // Additional properties and methods...
    }

    class CAShapeLayer {
        +CGPath path
        +UIColor strokeColor
        +UIColor fillColor
        +CGFloat lineWidth
        +CAShapeLayer()
        // Additional properties and methods...
    }

    class CATransform3D {
        +Float m11
        +Float m12
        +Float m13
        +Float m14
        +Float m21
        +Float m22
        +Float m23
        +Float m24
        +Float m31
        +Float m32
        +Float m33
        +Float m34
        +Float m41
        +Float m42
        +Float m43
        +Float m44
        +init()
        // Additional properties and methods...
    }

    class CATransaction {
        +CFTimeInterval animationDuration
        +Void commit()
        +Void begin()
        +Void setDisableActions(Bool)
        +Void setAnimationTimingFunction(CAMediaTimingFunction function)
        // Additional properties and methods...
    }

    class CAMediaTimingFunction {
        +init(controlPoints: Float, Float, Float, Float)
        +init(name: CAMediaTimingFunctionName)
        // Additional properties and methods...
    }

    CALayer <|-- CAShapeLayer
    CAAnimation <|-- CABasicAnimation
    CAAnimation <|-- CAKeyframeAnimation
    CAAnimation <|-- CATransition

    CALayer "1" -- "many" CALayer : sublayers
    CALayer "1" -- "many" CAAnimation : animations
```

---

## **2. Initializers Overview**

### **a. Initialization Methods Diagram**
- **Purpose**: Break down the various ways to instantiate Core Animation classes.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Layer Initialization**: `init()`, `init(layer:)`
  - **Animation Initialization**: `init()`, `init(keyPath:)`
  - **Transform Initialization**: `CATransform3DMakeRotation`, `CATransform3DScale`, etc.
  - **Timing Function Initialization**: `init(name:)`, `init(controlPoints:)`
  - **Transaction Initialization**: `begin()`, `commit()`

```mermaid
graph LR
    A[Core Animation Initializers] --> B[Layer Initialization]
    A --> C[Animation Initialization]
    A --> D[Transform Initialization]
    A --> E[Timing Function Initialization]
    A --> F[Transaction Initialization]

    B --> B1["init()"]
    B --> B2["init(layer: Any)"]

    C --> C1["CABasicAnimation(keyPath: String)"]
    C --> C2["CAKeyframeAnimation(keyPath: String)"]
    C --> C3["CATransition()"]

    D --> D1["CATransform3DMakeRotation(angle: CGFloat, x: CGFloat, y: CGFloat, z: CGFloat)"]
    D --> D2["CATransform3DScale(transform: CATransform3D, sx: CGFloat, sy: CGFloat, sz: CGFloat)"]
    D --> D3["CATransform3DTranslate(transform: CATransform3D, tx: CGFloat, ty: CGFloat, tz: CGFloat)"]

    E --> E1["init(name: CAMediaTimingFunctionName)"]
    E --> E2["init(controlPoints: Float, Float, Float, Float)"]

    F --> F1["begin()"]
    F --> F2["commit()"]
```

---

## **3. Properties Breakdown**

### **a. Key Properties Diagram**
- **Purpose**: Detail the main properties of Core Animation classes, focusing on `CALayer` and `CAAnimation`.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **CALayer Properties**:
    - **Appearance**: `backgroundColor`, `cornerRadius`, `borderWidth`, `borderColor`
    - **Geometry**: `bounds`, `position`, `anchorPoint`, `transform`
    - **Shadow**: `shadowOpacity`, `shadowOffset`, `shadowRadius`, `shadowColor`
    - **Content**: `contents`, `contentsGravity`, `contentsScale`
  - **CAAnimation Properties**:
    - **Timing**: `duration`, `beginTime`, `timingFunction`, `fillMode`
    - **Behavior**: `repeatCount`, `autoreverses`, `isRemovedOnCompletion`
    - **KeyPath**: `keyPath`

```mermaid
graph LR
    A[Core Animation Properties] --> B[CALayer Properties]
    A --> C[CAAnimation Properties]

    B --> B1[Appearance]
    B1 --> B11[backgroundColor: CGColor?]
    B1 --> B12[cornerRadius: CGFloat]
    B1 --> B13[borderWidth: CGFloat]
    B1 --> B14[borderColor: CGColor?]

    B --> B2[Geometry]
    B2 --> B21[bounds: CGRect]
    B2 --> B22[position: CGPoint]
    B2 --> B23[anchorPoint: CGPoint]
    B2 --> B24[transform: CATransform3D]

    B --> B3[Shadow]
    B3 --> B31[shadowOpacity: Float]
    B3 --> B32[shadowOffset: CGSize]
    B3 --> B33[shadowRadius: CGFloat]
    B3 --> B34[shadowColor: CGColor?]

    B --> B4[Content]
    B4 --> B41[contents: Any?]
    B4 --> B42[contentsGravity: String]
    B4 --> B43[contentsScale: CGFloat]

    C --> C1[Timing]
    C1 --> C11[duration: CFTimeInterval]
    C1 --> C12[beginTime: CFTimeInterval]
    C1 --> C13[timingFunction: CAMediaTimingFunction?]
    C1 --> C14[fillMode: String]

    C --> C2[Behavior]
    C2 --> C21[repeatCount: Float]
    C2 --> C22[autoreverses: Bool]
    C2 --> C23[isRemovedOnCompletion: Bool]

    C --> C3[KeyPath]
    C3 --> C31[keyPath: String]
```

---

## **4. Methods Grouped by Functionality**

### **a. Animation Management Methods**
- **Purpose**: Categorize methods based on their roles in managing animations within Core Animation.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Adding Animations**: `add(_ animation: CAAnimation, forKey key: String?)`
  - **Removing Animations**: `removeAnimation(forKey key: String)`, `removeAllAnimations()`
  - **Animation Configuration**: `beginTransaction()`, `commitTransaction()`, `setValue(_:forKey:)`
  - **Timing Adjustments**: `convertTime(_:from:)`, `convertTime(_:to:)`

```mermaid
flowchart TD
    A[Core Animation Methods] --> B[Animation Management]
    A --> C[Layer Manipulation]
    A --> D[Transform Manipulation]
    A --> E[Shadow and Appearance]
    A --> F[Content Management]

    B --> B1["add(_ animation: CAAnimation, forKey key: String?)"]
    B --> B2["removeAnimation(forKey key: String)"]
    B --> B3["removeAllAnimations()"]
    B --> B4["beginTransaction()"]
    B --> B5["commitTransaction()"]
    B --> B6["setValue(_: Any?, forKey: String)"]

    C --> C1["addSublayer(_ layer: CALayer)"]
    C --> C2["removeFromSuperlayer()"]

    D --> D1["setTransform(_ transform: CATransform3D)"]
    D --> D2["getTransform() -> CATransform3D"]

    E --> E1["setShadowOpacity(_ opacity: Float)"]
    E --> E2["setShadowOffset(_ offset: CGSize)"]
    E --> E3["setShadowRadius(_ radius: CGFloat)"]
    E --> E4["setShadowColor(_ color: CGColor)"]

    F --> F1["setContents(_ contents: Any?)"]
    F --> F2["getContents() -> Any?"]
```

---

## **5. Enumerations and Configurations**

### **a. Enumerations Diagram**
- **Purpose**: Highlight the enums used within Core Animation and their possible values.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **CAMediaTimingFunctionName**
  - **CAFillMode**
  - **CATransitionType**
  - **CATransitionSubtype**
  - **CABasicAnimationKey**

```mermaid
classDiagram
    class CoreAnimation {
        <<enumeration>> CAMediaTimingFunctionName
        <<enumeration>> CAFillMode
        <<enumeration>> CATransitionType
        <<enumeration>> CATransitionSubtype
        <<enumeration>> CABasicAnimationKey
    }

    class CAMediaTimingFunctionName {
        +linear
        +easeIn
        +easeOut
        +easeInEaseOut
        +default
    }

    class CAFillMode {
        +removed
        +forwards
        +backwards
        +both
    }

    class CATransitionType {
        +fade
        +moveIn
        +push
        +reveal
        +suckEffect
        +oglFlip
        +pageCurl
        +pageUnCurl
        // Additional types...
    }

    class CATransitionSubtype {
        +fromLeft
        +fromRight
        +fromTop
        +fromBottom
    }

    class CABasicAnimationKey {
        +position
        +opacity
        +transform
        // Additional key paths...
    }

    CoreAnimation --> CAMediaTimingFunctionName
    CoreAnimation --> CAFillMode
    CoreAnimation --> CATransitionType
    CoreAnimation --> CATransitionSubtype
    CoreAnimation --> CABasicAnimationKey
```

### **b. Configuration Classes Diagram**
- **Purpose**: Show the relationship between Core Animation classes and their configuration classes.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **CAMediaTimingFunction**
  - **CAAnimation**
  - **CATransform3D**
  - **CATransaction**

```mermaid
classDiagram
    class CAAnimation {
        +duration: CFTimeInterval
        +timingFunction: CAMediaTimingFunction?
        +fillMode: String
    }

    class CAMediaTimingFunction {
        +init(name: CAMediaTimingFunctionName)
        +init(controlPoints: Float, Float, Float, Float)
    }

    class CATransform3D {
        +m11: Float
        +m12: Float
        // Other matrix elements...
    }

    class CATransaction {
        +animationDuration: CFTimeInterval
        +setDisableActions(_ disable: Bool)
    }

    CAAnimation --> CAMediaTimingFunction
    CAAnimation --> CATransform3D
    CAAnimation --> CATransaction
```

---

## **6. Protocol Conformances**

### **a. Protocols Diagram**
- **Purpose**: Display the protocols that Core Animation classes conform to and their impact.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **CAAnimationDelegate**
  - **NSCopying**
  - **NSObject**
  - **CAAction**
  - **CALayoutManager**

```mermaid
classDiagram
    class CAAnimation {
        <<open class>>
    }

    class CAAnimationDelegate {
        <<protocol>>
        +animationDidStart(_ anim: CAAnimation)
        +animationDidStop(_ anim: CAAnimation, finished flag: Bool)
    }

    class NSCopying {
        <<protocol>>
        +copy(with zone: NSZone? = nil) -> Any
    }

    class NSObject {
        <<protocol>>
    }

    class CAAction {
        <<protocol>>
        +run(forKey event: String, object anObject: Any, arguments dict: [String : Any]?)
    }

    class CALayoutManager {
        <<protocol>>
        +layoutLayer(_ layer: CALayer)
    }

    CAAnimation ..|> CAAnimationDelegate
    CAAnimation ..|> NSCopying
    CALayer ..|> CAAction
    CALayer ..|> CALayoutManager
    CALayer ..|> NSObject
```

---

## **7. Relationships with Other Classes**

### **a. Related Classes Diagram**
- **Purpose**: Illustrate how Core Animation interacts with other UIKit classes and frameworks.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **UIView**: Hosts `CALayer` as its backing layer.
  - **UIKit Classes**: `UIButton`, `UILabel`, `UIImageView` utilizing Core Animation for animations.
  - **QuartzCore Framework**: Provides Core Animation classes.
  - **CADisplayLink**: Synchronizes drawing with the display’s refresh rate.
  - **CAEmitterLayer**: For particle effects.
  - **Core Graphics**: Interoperability with graphics contexts.
  - **Metal**: Advanced rendering and performance optimizations.

```mermaid
flowchart TD
    A[Core Animation] --> B[UIView]
    A --> C[UIKit Classes]
    A --> D[QuartzCore Framework]
    A --> E[CADisplayLink]
    A --> F[CAEmitterLayer]
    A --> G[Core Graphics]
    A --> H[Metal]

    B --> |hosts| A[CALayer]
    C --> |uses animations from| A
    D --> |provides Core Animation| A
    E --> |synchronizes drawing with| A
    F --> |particle effects using| A
    G --> |interop with| A
    H --> |enhances rendering with| A
```

---

## **8. Extensions and Additional Functionalities**

### **a. Core Animation Extensions Diagram**
- **Purpose**: Showcase the additional functionalities provided through extensions in Core Animation.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **CALayer Extensions**
  - **CAAnimation Helpers**
  - **Animation Blocks**

```mermaid
classDiagram
    class CALayer {
        <<open class>>
    }

    class CALayerExtensions {
        <<extension>>
        +func addFadeAnimation(duration: CFTimeInterval)
        +func addBounceAnimation()
        +func shake()
        // Additional extended methods...
    }

    class CAAnimationExtensions {
        <<extension>>
        +static func springAnimation() -> CAKeyframeAnimation
        +static func fadeAnimation() -> CABasicAnimation
        // Additional extended methods...
    }

    CALayer <-- CALayerExtensions
    CAAnimation <-- CAAnimationExtensions
```

### **b. Extensions Functionalities Flowchart**
- **Purpose**: Detail specific extended methods and their purposes.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Layer Animations**
  - **Custom Animation Sequences**
  - **Convenience Methods**

```mermaid
flowchart LR
    A[CALayer Extensions] --> B[Layer Animations]
    A --> C[Custom Animation Sequences]
    A --> D[Convenience Methods]

    B --> B1["addFadeAnimation(duration: CFTimeInterval)"]
    B --> B2["addBounceAnimation()"]

    C --> C1["createSpringAnimation() -> CAKeyframeAnimation"]
    C --> C2["createPathAnimation() -> CAKeyframeAnimation"]

    D --> D1["shake()"]
    D --> D2["pulse()"]
```

---

## **9. Lifecycle and Use Cases**

### **a. Lifecycle Flowchart**
- **Purpose**: Demonstrate the typical lifecycle of Core Animation objects within an application.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Initialization**
  - **Configuration**
  - **Adding to Layer**
  - **Running Animation**
  - **Completion Handling**
  - **Cleanup**

```mermaid
flowchart TD
    Start[Start] --> Init[Initialize CAAnimation or CALayer]
    Init --> Config[Configure Properties]
    Config --> Add[Add to CALayer]
    Add --> Run[Run Animation]
    Run --> Completion[Handle Completion]
    Completion --> Cleanup[Cleanup and Remove]
    Cleanup --> End[End]
```

### **b. Common Use Cases Diagram**
- **Purpose**: Outline the typical scenarios where Core Animation is utilized.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **View Animations**: Fading, scaling, rotating views.
  - **Layer Manipulations**: Changing layer properties like bounds, position.
  - **Complex Animations**: Keyframe animations, spring animations.
  - **Transitions**: Transitioning between views or states.
  - **Particle Effects**: Using CAEmitterLayer for particle systems.
  - **3D Transformations**: Applying 3D transforms to layers.
  - **Performance Optimizations**: Leveraging implicit animations for smooth UI.

```mermaid
flowchart TD
    A[Core Animation Use Cases] --> B[View Animations]
    A --> C[Layer Manipulations]
    A --> D[Complex Animations]
    A --> E[Transitions]
    A --> F[Particle Effects]
    A --> G[3D Transformations]
    A --> H[Performance Optimizations]

    B --> B1[Fading Views]
    B --> B2[Scaling Views]
    B --> B3[Rotating Views]

    C --> C1[Changing Bounds]
    C --> C2[Moving Position]

    D --> D1[Keyframe Animations]
    D --> D2[Spring Animations]

    E --> E1[View Transitions]
    E --> E2[State Transitions]

    F --> F1[Emitter Layers]
    F --> F2[Custom Particle Systems]

    G --> G1[3D Transforms]
    G --> G2[Perspective Effects]

    H --> H1[Implicit Animations]
    H --> H2[Performance Profiling]
```

---

## **10. Feature Availability Timeline**

### **a. Feature Availability Gantt Chart**
- **Purpose**: Show when various Core Animation features were introduced across iOS versions.
- **Diagram Type**: `gantt`
- **Contents**:
  - **iOS Versions**: 2.0, 4.0, 5.0, 6.0, 7.0, 8.0, 10.0, 11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0
  - **Features Introduced**: Keyframe animations, 3D transforms, implicit animations, CAEmitterLayer, CATransition types, etc.

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title Core Animation Feature Availability

    section iOS 2.0
    Basic CALayer Initialization       :done, des1, 2008-07-11, 2008-07-11

    section iOS 4.0
    Basic Animations                   :done, des2, 2010-06-21, 2010-06-21

    section iOS 5.0
    CAEmitterLayer Introduction        :done, des3, 2011-10-12, 2011-10-12

    section iOS 6.0
    3D Transformations                 :done, des4, 2012-09-19, 2012-09-19

    section iOS 7.0
    CATransition Enhancements           :done, des5, 2013-09-18, 2013-09-18

    section iOS 8.0
    Implicit Animations Control        :done, des6, 2014-09-17, 2014-09-17

    section iOS 10.0
    Keyframe Animations Enhancements    :done, des7, 2016-09-19, 2016-09-19

    section iOS 11.0
    Enhanced Animation Timing Functions :done, des8, 2017-09-19, 2017-09-19

    section iOS 12.0
    Advanced 3D Transformations        :done, des9, 2018-09-17, 2018-09-17

    section iOS 13.0
    New CAAnimation Types               :done, des10, 2019-09-19, 2019-09-19

    section iOS 14.0
    Enhanced CAEmitterLayer Features    :done, des11, 2020-09-16, 2020-09-16

    section iOS 15.0
    Performance Optimizations           :done, des12, 2021-09-20, 2021-09-20

    section iOS 16.0
    New Animation APIs                  :done, des13, 2022-09-12, 2022-09-12

    section iOS 17.0
    Advanced 3D Manipulations          :done, des14, 2023-09-18, 2023-09-18
```

---

## **11. Data Handling and Formats**

### **a. Animation Data Handling Diagram**
- **Purpose**: Explain how Core Animation handles different animation data formats and configurations.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **CAAnimation Types**: `CABasicAnimation`, `CAKeyframeAnimation`, `CATransition`, `CAAnimationGroup`
  - **Data Formats**: JSON-based animation descriptions, programmatic animations
  - **Export & Import**: Archiving animations, using CAAnimation in Storyboards

```mermaid
graph LR
    A[Core Animation] --> B[CAAnimation Types]
    A --> C[Data Formats]
    A --> D[Export & Import]

    B --> B1[CABasicAnimation]
    B --> B2[CAKeyframeAnimation]
    B --> B3[CATransition]
    B --> B4[CAAnimationGroup]

    C --> C1[Programmatic Animations]
    C --> C2[JSON-based Descriptions]

    D --> D1[Archiving Animations]
    D --> D2[Using in Storyboards]
```

---

## **12. Integration with Drawing Contexts**

### **a. Drawing Methods Usage Diagram**
- **Purpose**: Show how Core Animation methods are used within drawing contexts.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Layer Customization**: Setting properties like `bounds`, `position`
  - **Adding Sublayers**: `addSublayer(_:)`
  - **Drawing Paths**: Using `CAShapeLayer` for custom shapes
  - **Applying Transforms**: `setTransform(_:)`
  - **Animating Properties**: Adding `CAAnimation` to layers

```mermaid
flowchart TD
    UIImage -->|Draws at point| DrawAtPoint[Draw at CGPoint]
    UIImage -->|Draws with blend mode| DrawWithBlend[Draw with CGBlendMode & Alpha]
    UIImage -->|Draws in rect| DrawInRect[Draw in CGRect]
    UIImage -->|Draws as pattern| DrawAsPattern[Draw as Pattern in CGRect]

    DrawAtPoint -->|Usage| Usage1[Rendering Image at Specific Coordinates]
    DrawWithBlend -->|Usage| Usage2[Applying Blend Modes and Transparency]
    DrawInRect -->|Usage| Usage3[Scaling or Tiling Image within Rect]
    DrawAsPattern -->|Usage| Usage4[Creating Repeating Patterns]
```

---

## **13. Summary and Best Practices**

### **a. Summary Diagram**
- **Purpose**: Provide a high-level overview of Core Animation's key characteristics and functionalities.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Versatile Animations**: Basic, keyframe, transitions
  - **Layer Management**: Hierarchical layers, sublayers
  - **3D Transformations**: Advanced 3D effects
  - **Performance Optimizations**: Implicit animations, efficient layering
  - **Seamless Integration**: With UIKit, Core Graphics, Metal

```mermaid
graph LR
    A[Core Animation] --> B[Versatile Animations]
    A --> C[Layer Management]
    A --> D[3D Transformations]
    A --> E[Performance Optimizations]
    A --> F[Seamless Integration]

    B --> B1[Basic Animations]
    B --> B2[Keyframe Animations]
    B --> B3[Transitions]

    C --> C1[Hierarchical Layers]
    C --> C2[Sublayers Management]

    D --> D1[Advanced 3D Effects]
    D --> D2[Perspective and Depth]

    E --> E1[Implicit Animations]
    E --> E2[Efficient Layering]

    F --> F1[Integration with UIKit]
    F --> F2[Interoperability with Core Graphics]
    F --> F3[Enhanced by Metal]
```

---

## **Best Practices**

1. **Utilize Implicit Animations**: Leverage implicit animations for smoother and more efficient UI updates without excessive code.

2. **Layer Hierarchy Management**: Maintain a clear and efficient layer hierarchy to optimize rendering performance and memory usage.

3. **Use CAEmitterLayer for Particle Effects**: Implement particle systems using `CAEmitterLayer` for visually appealing and performant effects.

4. **Optimize 3D Transforms**: Apply 3D transformations judiciously, understanding their impact on performance and visual complexity.

5. **Leverage CAAnimation Groups**: Combine multiple animations using `CAAnimationGroup` to synchronize and manage complex animation sequences.

6. **Control Animation Lifecycles**: Appropriately begin and commit `CATransaction` blocks to manage animation properties and timing effectively.

7. **Adopt Modern Animation Techniques**: Stay updated with the latest Core Animation features introduced in recent iOS versions to enhance app interactivity and responsiveness.

8. **Profile and Optimize**: Regularly use profiling tools like Instruments to identify and address performance bottlenecks related to animations and layer rendering.

By adhering to these best practices and leveraging the detailed structure provided in the diagrams, developers can effectively implement and manage Core Animation within their iOS applications, ensuring both aesthetic appeal and optimal performance.

