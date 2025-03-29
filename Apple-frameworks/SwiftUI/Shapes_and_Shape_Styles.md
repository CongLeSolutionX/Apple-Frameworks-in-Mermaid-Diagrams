---
created: 2025-03-28 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Shapes & Shape Styles - A Diagrammatic Guide 
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---


Representing the `Shape` protocol, concrete shapes, and how `ShapeStyle` is used.

```mermaid
---
title: "SwiftUI Framework - Shapes & Shape Styles"
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
    'classDiagram': { 'htmlLabels': false, 'curve': 'linear' },
    'fontFamily': 'Comic Sans MS',
    'themeVariables': {
      'primaryColor': '#ffff',
      'primaryTextColor': '#2ff9',
      'primaryBorderColor': '#7c2',
      'lineColor': '#F8B229',
      'secondaryColor': '#006100',
      'tertiaryColor': '#fff'
    }
  }
}%%
classDiagram
    direction LR
    class Shape {
        + Animatable
        + View
        + Sendable
        + path(in: CGRect) Path
        + role : ShapeRole
        + layoutDirectionBehavior : LayoutDirectionBehavior
        + sizeThatFits(ProposedViewSize) CGSize
        + fill(ShapeStyle) View
        + stroke(ShapeStyle) View
    }
    class InsettableShape {
        + Shape
        + inset(by: CGFloat) InsetShape
        + strokeBorder(ShapeStyle) View
    }
    class Path {
        + Shape
        + cgPath CGPath
        + isEmpty Bool
        + boundingRect CGRect
        + contains(CGPoint) Bool
        %% + forEach((Element)->Void)
        %% + Element { move, line, quadCurve, curve, closeSubpath }
        + addLine(to: CGPoint)
        + addRect(CGRect)
        + addEllipse(in: CGRect)
        + addArc(...)
        + addPath(Path)
        + applying(CGAffineTransform) Path
    }
    class ShapeStyle {
        + Sendable
        + resolve(in: EnvironmentValues) Resolved
    }
    class Color {
        + ShapeStyle
        + View
        + Resolved
        + RGBColorSpace
        + init(...)
        + opacity(Double) Color
    }
    class LinearGradient {
        + ShapeStyle
        + View
        + gradient Gradient
        + startPoint UnitPoint
        + endPoint UnitPoint
    }
    class RadialGradient {
        + ShapeStyle
        + View
        + gradient Gradient
        + center UnitPoint
        + startRadius CGFloat
        + endRadius CGFloat
    }
    class AngularGradient {
        + ShapeStyle
        + View
        + gradient Gradient
        + center UnitPoint
        + startAngle Angle
        + endAngle Angle
    }
    class EllipticalGradient {
         + ShapeStyle
         + View
         + gradient Gradient
         + center UnitPoint
         + startRadiusFraction CGFloat
         + endRadiusFraction CGFloat
    }
    class ImagePaint {
        + ShapeStyle
        + image Image
        + sourceRect CGRect
        + scale CGFloat
    }
    class Material {
        + ShapeStyle
        + Sendable
        + .regular
        + .thick
        + .thin
        + .ultraThin
        + .ultraThick
        + .bar
    }
    class HierarchicalShapeStyle {
        + ShapeStyle
        + .primary
        + .secondary
        + .tertiary
        + .quaternary
        + .quinary
    }
     class BackgroundStyle {
        + ShapeStyle
    }
     class ForegroundStyle {
        + ShapeStyle
    }
     class TintShapeStyle {
        + ShapeStyle
    }
     class SeparatorShapeStyle {
         + ShapeStyle
     }
    class AnyShapeStyle {
        + ShapeStyle
        + init(ShapeStyle)
    }
     class AnyGradient{
        + ShapeStyle
        + init(Gradient)
    }
     class Shader{
         + ShapeStyle
         + function ShaderFunction
         + arguments [Argument]
     }
     class MeshGradient{
          + ShapeStyle
          + View
          + width Int
          + height Int
          + locations Locations
          + colors Colors
      }


    Shape <|-- InsettableShape
    Shape <|-- Path
    Shape <|-- Rectangle
    Shape <|-- Circle
    Shape <|-- Capsule
    Shape <|-- Ellipse
    Shape <|-- RoundedRectangle
    Shape <|-- UnevenRoundedRectangle
    Shape <|-- OffsetShape
    Shape <|-- RotatedShape
    Shape <|-- ScaledShape
    Shape <|-- TransformedShape
    Shape <|-- ContainerRelativeShape
    Shape <|-- AnyShape

    InsettableShape <|-- Rectangle
    InsettableShape <|-- Circle
    InsettableShape <|-- Capsule
    InsettableShape <|-- Ellipse
    InsettableShape <|-- RoundedRectangle
    InsettableShape <|-- UnevenRoundedRectangle

    <<protocol>> Shape
    <<protocol>> InsettableShape
    <<protocol>> ShapeStyle

    ShapeStyle <|-- Color
    ShapeStyle <|-- LinearGradient
    ShapeStyle <|-- RadialGradient
    ShapeStyle <|-- AngularGradient
    ShapeStyle <|-- EllipticalGradient
    ShapeStyle <|-- ImagePaint
    ShapeStyle <|-- Material
    ShapeStyle <|-- HierarchicalShapeStyle
    ShapeStyle <|-- BackgroundStyle
    ShapeStyle <|-- ForegroundStyle
    ShapeStyle <|-- TintShapeStyle
    ShapeStyle <|-- SeparatorShapeStyle
    ShapeStyle <|-- AnyShapeStyle
    ShapeStyle <|-- AnyGradient
    ShapeStyle <|-- Shader
    ShapeStyle <|-- MeshGradient

    Shape --o ShapeStyle : uses for fill/stroke
    
```

----


**Explanation:** This class diagram shows the `Shape` protocol hierarchy, including `InsettableShape`, and examples of concrete shapes. It also shows the `ShapeStyle` protocol and various conforming types used for filling and stroking shapes.


---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---