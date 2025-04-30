---
created: 2025-04-29 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Metal Function Library
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution 4.0 International License (CC BY 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---



## Core Class & Protocol Relationships

This diagram shows the main protocols (`MTLFunction`, `MTLLibrary`) and the primary configuration class (`MTLCompileOptions`), along with their key properties and connections to supporting types.

```mermaid
---
title: "Core Class & Protocol Relationships"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  look: handDrawn
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'classDiagram': { 'htmlLabels': false},
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#BB28',
      'primaryTextColor': '#000',
      'lineColor': '#F8B229',
      'primaryBorderColor': '#7C3',
      'secondaryColor': '#DD15'
    }
  }
}%%
classDiagram
  direction LR
%%   title Metal Function, Library, and Compile Options

  class MTLDevice

  class NSObject
  class NSCopying

  class MTLFunction {
    <<protocol>>
    <<NSObjectProtocol>>
    +label: String? get set
    +device: MTLDevice get
    +functionType: MTLFunctionType get
    +patchType: MTLPatchType get -- iOS 10.0+ --
    +patchControlPointCount: Int get -- iOS 10.0+ --
    +vertexAttributes: [MTLVertexAttribute]? get
    +stageInputAttributes: [MTLAttribute]? get -- iOS 10.0+ --
    +name: String get
    +functionConstantsDictionary: [String : MTLFunctionConstant] get -- iOS 10.0+ --
    +options: MTLFunctionOptions get -- iOS 14.0+ --
    +makeArgumentEncoder(bufferIndex: Int): MTLArgumentEncoder -- iOS 11.0+ --
    +makeArgumentEncoder_deprecated(bufferIndex: Int, reflection): MTLArgumentEncoder -- iOS 11.0+, deprecated 16.0 --
  }

  class MTLLibrary {
      <<protocol>>
      <<NSObjectProtocol>>
     +label: String? get set
     +device: MTLDevice get
     +functionNames: [String] get
     +type: MTLLibraryType get -- iOS 14.0+ --
     +installName: String? get -- iOS 14.0+ --
     +makeFunction(name: String): MTLFunction?
     +makeFunction(name: String, constantValues: MTLFunctionConstantValues): MTLFunction throws -- iOS 10.0+ --
     +makeFunctionAsync(name: String, constantValues: ...) -- iOS 10.0+ --
     +makeFunctionAsyncWithDescriptor(descriptor: MTLFunctionDescriptor, ...) -- iOS 14.0+ --
     +makeFunctionSyncWithDescriptor(descriptor: MTLFunctionDescriptor): MTLFunction throws -- iOS 14.0+ --
     +makeIntersectionFunctionAsync(descriptor: MTLIntersectionFunctionDescriptor, ...) -- iOS 14.0+ --
     +makeIntersectionFunctionSync(descriptor: MTLIntersectionFunctionDescriptor): MTLFunction throws -- iOS 14.0+ --
  }

  class MTLCompileOptions {
    <<NSObject>>
    <<NSCopying>>
    +preprocessorMacros: [String : NSObject]?
    +fastMathEnabled: Bool -- deprecated 18.0 --
    +mathMode: MTLMathMode -- iOS 18.0+ --
    +mathFloatingPointFunctions: MTLMathFloatingPointFunctions -- iOS 18.0+ --
    +languageVersion: MTLLanguageVersion -- iOS 9.0+ --
    +libraryType: MTLLibraryType -- iOS 14.0+ --
    +installName: String? -- iOS 14.0+ --
    +libraries: [MTLDynamicLibrary]? -- iOS 14.0+ --
    +preserveInvariance: Bool -- iOS 14.0+ --
    +optimizationLevel: MTLLibraryOptimizationLevel -- iOS 16.0+ --
    +compileSymbolVisibility: MTLCompileSymbolVisibility -- iOS 16.4+ --
    +allowReferencingUndefinedSymbols: Bool -- iOS 16.4+ --
    +maxTotalThreadsPerThreadgroup: Int -- iOS 16.4+ --
    +enableLogging: Bool -- iOS 18.0+ --
  }

  class MTLVertexAttribute {
    <<NSObject>>
    +name: String get
    +attributeIndex: Int get
    +attributeType: MTLDataType get -- iOS 8.3+ --
    +isActive: Bool get
    +isPatchData: Bool get -- iOS 10.0+ --
    +isPatchControlPointData: Bool get -- iOS 10.0+ --
  }

  class MTLAttribute {
    <<NSObject>>
    +name: String get
    +attributeIndex: Int get
    +attributeType: MTLDataType get
    +isActive: Bool get
    +isPatchData: Bool get -- iOS 10.0+ --
    +isPatchControlPointData: Bool get -- iOS 10.0+ --
  }

  class MTLFunctionConstant {
    <<NSObject>>
    +name: String get
    +type: MTLDataType get
    +index: Int get
    +required: Bool get
  }

  class MTLAutoreleasedArgument {
    <<typealias>>
    = MTLArgument -- deprecated 16.0 --
  }

  MTLDevice --> MTLLibrary : Creates/Owns
  MTLDevice --> MTLFunction : Owns

  MTLLibrary "1" *-- "*" MTLFunction : Contains/Creates
  MTLLibrary ..> MTLCompileOptions : Uses during creation

  MTLFunction  "1" *-- "*" MTLVertexAttribute : Describes (vertexAttributes)
  MTLFunction  "1" *-- "*" MTLAttribute : Describes (stageInputAttributes)
  MTLFunction  "1" *-- "*" MTLFunctionConstant : Describes (functionConstantsDictionary)
  MTLFunction --> MTLAutoreleasedArgument : Uses in makeArgumentEncoder

  MTLCompileOptions ..> MTLMathMode : Uses
  MTLCompileOptions ..> MTLMathFloatingPointFunctions : Uses
  MTLCompileOptions ..> MTLLanguageVersion : Uses
  MTLCompileOptions ..> MTLLibraryType : Uses
  MTLCompileOptions ..> MTLLibraryOptimizationLevel : Uses
  MTLCompileOptions ..> MTLCompileSymbolVisibility : Uses

  MTLFunction ..> MTLFunctionType : Uses
  MTLFunction ..> MTLPatchType : Uses

  MTLCompileOptions --|> NSObject
  MTLCompileOptions ..> NSCopying

  MTLVertexAttribute --|> NSObject
  MTLAttribute --|> NSObject
  MTLFunctionConstant --|> NSObject

```

**Explanation:**

*   This diagram focuses on the main types and their direct relationships.
*   `MTLLibrary` and `MTLFunction` are central protocols.
*   `MTLCompileOptions` holds configuration settings used when creating an `MTLLibrary`.
*   Auxiliary classes (`MTLVertexAttribute`, `MTLAttribute`, `MTLFunctionConstant`) provide metadata for `MTLFunction`.
*   Arrows indicate dependencies or creation/ownership relationships (e.g., `MTLLibrary` creates `MTLFunction`).
*   Dotted lines (`..>`) often indicate usage or association. Solid lines with composition (`*--`) show parts of a whole. Inheritance (`--|>`) and protocol conformance (`..>`) are also shown where base types are included.
*   Availability and deprecation are noted with `-- comments --`.

---



## Core Types, Protocols, and Relationships

This diagram shows the main protocols, classes, enumerations, and their interconnections, including properties, methods, and conformances. Availability and deprecation information are included as comments or notes where feasible.

```mermaid
---
title: "Metal Function, Library, Compile Options & Related Types"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  look: handDrawn
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'classDiagram': { 'htmlLabels': false},
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#BB28',
      'primaryTextColor': '#000',
      'lineColor': '#F8B229',
      'primaryBorderColor': '#7C3',
      'secondaryColor': '#DD15'
    }
  }
}%%
classDiagram
  direction LR

  %% ---------- Base/External Types ---------- %%
  class NSObject
  class NSCopying
  class MTLDevice
  class MTLArgumentEncoder
  %% Base type for MTLAutoreleasedArgument
  class MTLArgument

 %% Used in makeFunction methods
  class MTLFunctionConstantValues

  %% Used in makeFunction methods
  class MTLFunctionDescriptor

  %% Used in makeIntersectionFunction methods
  class MTLIntersectionFunctionDescriptor 

   %% Used in MTLCompileOptions.libraries
  class MTLDynamicLibrary


  %% ---------- Typealias ---------- %%
  class MTLAutoreleasedArgument {
    <<typealias>>
    = MTLArgument
  }
  note for MTLAutoreleasedArgument "iOS 8.0+, deprecated 16.0\n'Use MTLBinding... instead'"


  %% ---------- Enumerations ---------- %%
  class MTLPatchType {
    <<enumeration>>
    <<@unchecked Sendable>>
    %% iOS 10.0+ %%
    +none = 0
    +triangle = 1
    +quad = 2
  }

  class MTLFunctionType {
    <<enumeration>>
    <<@unchecked Sendable>>
    %% iOS 8.0+ %%
    +vertex = 1
    +fragment = 2
    +kernel = 3
    +visible = 5 %% iOS 14.0+ %%
    +intersection = 6 %% iOS 14.0+ %%
    +mesh = 7 %% iOS 16.0+ %%
    +object = 8 %% iOS 16.0+ %%
  }

   class MTLLanguageVersion {
     <<enumeration>>
     <<@unchecked Sendable>>
     %% iOS 9.0+ %%
     +version1_0 = 65536 %% Deprecated 16.0 %%
     +version1_1 = 65537 %% iOS 9.0+ %%
     +version1_2 = 65538 %% iOS 10.0+ %%
     +version2_0 = 131072 %% iOS 11.0+ %%
     +version2_1 = 131073 %% iOS 12.0+ %%
     +version2_2 = 131074 %% iOS 13.0+ %%
     +version2_3 = 131075 %% iOS 14.0+ %%
     +version2_4 = 131076 %% iOS 15.0+ %%
     +version3_0 = 196608 %% iOS 16.0+ %%
     +version3_1 = 196609 %% iOS 17.0+ %%
     +version3_2 = 196610 %% iOS 18.0+ %%
  }

   class MTLLibraryType {
     <<enumeration>>
      <<@unchecked Sendable>>
     %% iOS 14.0+ %%
     +executable = 0
     +dynamic = 1
  }

  class MTLLibraryOptimizationLevel {
    <<enumeration>>
     <<@unchecked Sendable>>
    %% iOS 16.0+ %%
    +default = 0
    +size = 1
  }

  class MTLCompileSymbolVisibility {
    <<enumeration>>
     <<@unchecked Sendable>>
    %% iOS 16.4+ %%
    +default = 0
    +hidden = 1
  }

 class MTLMathMode {
    <<enumeration>>
    <<@unchecked Sendable>>
    +safe = 0
    +relaxed = 1
    +fast = 2
    %% Note: Available iOS 18.0+, but enum defined without specific version attr. Options using it are versioned %%
  }

 class MTLMathFloatingPointFunctions {
    <<enumeration>>
    <<@unchecked Sendable>>
    +fast = 0
    +precise = 1
    %% Note: Available iOS 18.0+, but enum defined without specific version attr. Options using it are versioned %%
  }


  %% ---------- Attribute/Constant Classes ---------- %%
  class MTLVertexAttribute {
    <<open class>>
    <<NSObject>>
    %% iOS 8.0+ %%
    +name: String get
    +attributeIndex: "Int get"
    +attributeType: MTLDataType get %% iOS 8.3+ %%
    +isActive: Bool get
    +isPatchData: Bool get %% iOS 10.0+ %%
    +isPatchControlPointData: Bool get %% iOS 10.0+ %%
  }

  class MTLAttribute {
    <<open class>>
    <<NSObject>>
    %% iOS 10.0+ %%
    +name: String get
    +attributeIndex: Int get
    +attributeType: MTLDataType get
    +isActive: Bool get
    +isPatchData: Bool get %% iOS 10.0+ %%
    +isPatchControlPointData: Bool get %% iOS 10.0+ %%
  }

  class MTLFunctionConstant {
    <<open class>>
    <<NSObject>>
    %% iOS 10.0+ %%
    +name: String get
    +type: MTLDataType get
    +index: Int get
    +required: Bool get
  }


  %% ---------- Core Protocols/Classes ---------- %%
  class MTLFunction {
    <<protocol>>
    <<NSObjectProtocol>>
    %% iOS 8.0+ %%
    +label: String? get set %% iOS 10.0+ %%
    +device: MTLDevice get
    +functionType: MTLFunctionType get
    +patchType: MTLPatchType get %% iOS 10.0+ %%
    +patchControlPointCount: Int get %% iOS 10.0+ %%
    +vertexAttributes: [MTLVertexAttribute]? get
    +stageInputAttributes: [MTLAttribute]? get %% iOS 10.0+ %%
    +name: String get
    +functionConstantsDictionary: [String : MTLFunctionConstant] get %% iOS 10.0+ %%
    +options: MTLFunctionOptions get %% iOS 14.0+ %%
    +makeArgumentEncoder(bufferIndex: Int): any MTLArgumentEncoder %% iOS 11.0+ %%
    +makeArgumentEncoder(bufferIndex: Int, reflection: AutoreleasingUnsafeMutablePointer<MTLAutoreleasedArgument?>?): any MTLArgumentEncoder %% iOS 11.0+, deprecated 16.0, msg: 'Use MTLDevice...' %%
  }

   class MTLLibrary {
      <<protocol>>
      <<NSObjectProtocol>>
      %% iOS 8.0+ %%
     +label: String? get set
     +device: MTLDevice get
     +functionNames: [String] get
     +type: MTLLibraryType get %% iOS 14.0+ %%
     +installName: String? get %% iOS 14.0+ %%
     +makeFunction(name: String): (any MTLFunction)?
     +makeFunction(name: String, constantValues: MTLFunctionConstantValues): throws -> any MTLFunction %% iOS 10.0+ %%
     +makeFunction(name: String, constantValues: MTLFunctionConstantValues, completionHandler: @escaping ((any MTLFunction)?, (any Error)?) -> Void) %% iOS 10.0+ %%
     +makeFunction(name: String, constantValues: MTLFunctionConstantValues): async throws -> any MTLFunction %% iOS 10.0+ %%
     +makeFunction(descriptor: MTLFunctionDescriptor, completionHandler: @escaping ((any MTLFunction)?, (any Error)?) -> Void) %% iOS 14.0+ %%
     +makeFunction(descriptor: MTLFunctionDescriptor): async throws -> any MTLFunction %% iOS 14.0+ %%
     +makeFunction(descriptor: MTLFunctionDescriptor): throws -> any MTLFunction %% iOS 14.0+ %%
     +makeIntersectionFunction(descriptor: MTLIntersectionFunctionDescriptor, completionHandler: @escaping ((any MTLFunction)?, (any Error)?) -> Void) %% iOS 14.0+ %%
     +makeIntersectionFunction(descriptor: MTLIntersectionFunctionDescriptor): async throws -> any MTLFunction %% iOS 14.0+ %%
     +makeIntersectionFunction(descriptor: MTLIntersectionFunctionDescriptor): throws -> any MTLFunction %% iOS 14.0+ %%
  }

  class MTLCompileOptions {
    <<open class>>
    <<NSObject>>
    <<NSCopying>>
    %% iOS 8.0+ %%
    +preprocessorMacros: [String : NSObject]? get set
    +fastMathEnabled: Bool get set %% iOS 8.0+, deprecated 18.0, msg: 'Use mathMode instead' %%
    +mathMode: MTLMathMode get set %% iOS 18.0+ %%
    +mathFloatingPointFunctions: MTLMathFloatingPointFunctions get set %% iOS 18.0+ %%
    +languageVersion: MTLLanguageVersion get set %% iOS 9.0+ %%
    +libraryType: MTLLibraryType get set %% iOS 14.0+ %%
    +installName: String? get set %% iOS 14.0+ %%
    +libraries: [any MTLDynamicLibrary]? get set %% iOS 14.0+ %%
    +preserveInvariance: Bool get set %% iOS 14.0+ %%
    +optimizationLevel: MTLLibraryOptimizationLevel get set %% iOS 16.0+ %%
    +compileSymbolVisibility: MTLCompileSymbolVisibility get set %% iOS 16.4+ %%
    +allowReferencingUndefinedSymbols: Bool get set %% iOS 16.4+ %%
    +maxTotalThreadsPerThreadgroup: Int get set %% iOS 16.4+ %%
    +enableLogging: Bool get set %% iOS 18.0+ %%
  }


  %% ---------- Error Structure ---------- %%
  %% Swift Standard Library Protocol %%
  class Error

  %% Swift Standard Library Protocol %%
  class CustomNSError

  %% Swift Standard Library Protocol %%
  class Hashable

  class MTLLibraryError {
      <<struct>>
      <<Error>>
      <<CustomNSError>>
      <<Hashable>>
      %% iOS 8.0+ %%
      +init(_nsError: NSError)
      +errorDomain: String get
      +Code: enum get
  }
  class MTLLibraryError_Code {
     <<enumeration>>
      <<UInt>>
      <<Sendable>>
      <<Equatable>>
      %% iOS 8.0+ %%
     +unsupported = 1
     +internal = 2
     +compileFailure = 3
     +compileWarning = 4
     +functionNotFound = 5 %% iOS 10.0+ %%
     +fileNotFound = 6 %% iOS 10.0+ %%
  }


  %% ---------- Relationships ---------- %%
  MTLCompileOptions --|> NSObject
  MTLCompileOptions ..> NSCopying

  MTLVertexAttribute --|> NSObject
  MTLAttribute --|> NSObject
  MTLFunctionConstant --|> NSObject

  MTLFunction ..> NSObjectProtocol
  MTLLibrary ..> NSObjectProtocol

  MTLFunction --> MTLDevice : "device {get}"
  MTLLibrary --> MTLDevice : "device {get}"

  MTLLibrary "1" *--> "0..*" MTLFunction : Creates/Contains
  MTLLibrary --> MTLLibraryError : Can Throw/Produce
  MTLLibrary ..> MTLFunctionConstantValues : uses in makeFunction
  MTLLibrary ..> MTLFunctionDescriptor : uses in makeFunction
  MTLLibrary ..> MTLIntersectionFunctionDescriptor : uses in makeIntersectionFunction

  MTLDevice --> MTLLibrary : Creates

  MTLCompileOptions ..> MTLLanguageVersion : "languageVersion {get set}"
  MTLCompileOptions ..> MTLLibraryType : "libraryType {get set}"
  MTLCompileOptions ..> MTLLibraryOptimizationLevel : "optimizationLevel {get set}"
  MTLCompileOptions ..> MTLCompileSymbolVisibility: "compileSymbolVisibility {get set}"
  MTLCompileOptions ..> MTLMathMode : "mathMode {get set}"
  MTLCompileOptions ..> MTLMathFloatingPointFunctions : "mathFloatingPointFunctions {get set}"
  MTLCompileOptions ..> MTLDynamicLibrary : "libraries {get set}"


  MTLFunction --> MTLFunctionType : "functionType {get}"
  MTLFunction --> MTLPatchType : "patchType {get}"
  MTLFunction "1" o--> "0..*" MTLVertexAttribute : "vertexAttributes {get}"
  MTLFunction "1" o--> "0..*" MTLAttribute : "stageInputAttributes {get}"
  MTLFunction "1" o--> "0..*" MTLFunctionConstant : "functionConstantsDictionary {get}"
  MTLFunction ..> MTLArgumentEncoder : returns from makeArgumentEncoder
  MTLFunction ..> MTLAutoreleasedArgument : uses in makeArgumentEncoder

  MTLLibraryError ..> Error
  MTLLibraryError ..> CustomNSError
  MTLLibraryError ..> Hashable
  MTLLibraryError o-- MTLLibraryError_Code : "Code enum"
  
  MTLAutoreleasedArgument --|> MTLArgument : (is typealias for)

```


**Explanation of Changes and Consolidation:**

1.  **Single Diagram Focus:** Merged the core types, enumerations, and error structure into one comprehensive class diagram. This makes relationships clearer.
2.  **Type Representation:** Used `<<protocol>>`, `<<open class>>`, `<<enumeration>>`, `<<struct>>`, `<<typealias>>` stereotypes for better type identification.
3.  **Full Signatures:** Included more complete method signatures in `MTLLibrary` and `MTLFunction`, showing parameters (`name`, `constantValues`, `descriptor`, `completionHandler`), return types (`-> (any MTLFunction)?`, `throws -> any MTLFunction`), and asynchronous variations (`async`, completion handlers).
4.  **Property Details:** Added ` { get }` or ` { get set }` to properties where specified in the code or implied by `open class` declarations.
5.  **Conformances:** Explicitly showed conformances like `NSObjectProtocol`, `NSCopying`, `Error`, `CustomNSError`, `Hashable`, and `@unchecked Sendable` (represented via stereotype or note).
6.  **Availability/Deprecations:** Incorporated availability (`%% iOS X.Y+ %%`) and deprecation comments (`%% Deprecated X.Y, msg: '...' %%`) directly within the type/member definitions where possible for conciseness. Added notes for more complex messages like the `MTLAutoreleasedArgument` deprecation.
7.  **External Types:** Added placeholders for types referenced but not defined in the snippet (e.g., `MTLDevice`, `MTLArgumentEncoder`, `MTLDataType`, `MTLDynamicLibrary`, `MTLFunctionConstantValues`, etc.) to show connections.
8.  **Relationship Clarity:** Refined relationship arrows (`-->` dependency/usage, `*-->` composition/creation, `o--` aggregation, `--|>` inheritance, `..>` conformance/realization) to better reflect the code's structure. For instance, `MTLLibrary` *creates/contains* `MTLFunction`, while `MTLCompileOptions` *uses* various enums.
9.  **Error Structure Integration:** Modeled `MTLLibraryError` as a struct conforming to relevant protocols and containing the `Code` enum. Referenced the standard `Error` and `CustomNSError` protocols.
10. **Theme and Layout:** Adjusted theme (`default` with variables) and layout (`direction LR`) for readability.


----



## Enumeration Details

This section lists the key enumerations and their possible values. Representing each as a small separate diagram can be verbose, so a combination of listing within the main diagram and a summary table is effective.

```mermaid
---
title: "Enumeration Details"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  look: handDrawn
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'classDiagram': { 'htmlLabels': false},
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#BB28',
      'primaryTextColor': '#000',
      'lineColor': '#F8B229',
      'primaryBorderColor': '#7C3',
      'secondaryColor': '#DD15'
    }
  }
}%%
classDiagram
  class MTLPatchType {
    <<enumeration>>
    -- iOS 10.0+ --
    none
    triangle
    quad
  }

  class MTLFunctionType {
    <<enumeration>>
    -- iOS 8.0+ --
    vertex
    fragment
    kernel
    visible -- iOS 14.0+ --
    intersection -- iOS 14.0+ --
    mesh -- iOS 16.0+ --
    object -- iOS 16.0+ --
  }

  class MTLLanguageVersion {
     <<enumeration>>
     -- iOS 9.0+ --
     version1_0 -- deprecated 16.0 --
     version1_1
     version1_2 -- iOS 10.0+ --
     version2_0 -- iOS 11.0+ --
     version2_1 -- iOS 12.0+ --
     version2_2 -- iOS 13.0+ --
     version2_3 -- iOS 14.0+ --
     version2_4 -- iOS 15.0+ --
     version3_0 -- iOS 16.0+ --
     version3_1 -- iOS 17.0+ --
     version3_2 -- iOS 18.0+ --
  }

  class MTLLibraryType {
     <<enumeration>>
     -- iOS 14.0+ --
     executable
     dynamic
  }

  class MTLLibraryOptimizationLevel {
    <<enumeration>>
    -- iOS 16.0+ --
    default
    size
  }

  class MTLCompileSymbolVisibility {
    <<enumeration>>
    -- iOS 16.4+ --
    default
    hidden
  }

  class MTLMathMode {
    <<enumeration>>
    -- iOS 18.0+ --
    safe
    relaxed
    fast
  }

   class MTLMathFloatingPointFunctions {
    <<enumeration>>
    -- iOS 18.0+ --
    fast
    precise
  }

  MTLFunction ..> MTLPatchType
  MTLFunction ..> MTLFunctionType
  MTLCompileOptions ..> MTLLanguageVersion
  MTLCompileOptions ..> MTLLibraryType
  MTLCompileOptions ..> MTLLibraryOptimizationLevel
  MTLCompileOptions ..> MTLCompileSymbolVisibility
  MTLCompileOptions ..> MTLMathMode
  MTLCompileOptions ..> MTLMathFloatingPointFunctions
  MTLLibrary ..> MTLLibraryType
  
```

**Summary Table of Enumerations:**

| Enumeration                   | Purpose                                        | Key Cases (Examples)                               | Availability |
| :---------------------------- | :--------------------------------------------- | :------------------------------------------------- | :----------- |
| `MTLPatchType`                | Type of patch for tessellation                 | `none`, `triangle`, `quad`                         | iOS 10.0+    |
| `MTLFunctionType`             | Role of the shader function                    | `vertex`, `fragment`, `kernel`, `mesh`, `object` | iOS 8.0+     |
| `MTLLanguageVersion`          | MSL version standard                           | `version1_x`, `version2_x`, `version3_x`           | iOS 9.0+     |
| `MTLLibraryType`              | Type of compiled library                       | `executable`, `dynamic`                            | iOS 14.0+    |
| `MTLLibraryOptimizationLevel` | Compiler optimization goal                      | `default`, `size`                                  | iOS 16.0+    |
| `MTLCompileSymbolVisibility`  | Default visibility for symbols                 | `default`, `hidden`                                | iOS 16.4+    |
| `MTLMathMode`                 | Floating-point optimization strictness         | `safe`, `relaxed`, `fast`                          | iOS 18.0+    |
| `MTLMathFloatingPointFunctions` | Default single-precision math function library | `fast`, `precise`                                  | iOS 18.0+    |

---


## Typical Metal Shader Workflow

This flowchart shows the typical sequence of steps from writing shader code to using it in a pipeline.

```mermaid
---
title: "Typical Metal Shader Workflow"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  layout: elk
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%%%%%%% Available curve styles include the following keywords:
%% basis, bumpX, bumpY, cardinal, catmullRom, linear, monotoneX, monotoneY, natural, step, stepAfter, stepBefore.
%%{
  init: {
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#D5F5E3',
      'primaryTextColor': '#145A32',
      'lineColor': '#F8B229',
      'primaryBorderColor': '#27AE60',
      'secondaryColor': '#EBDEF0',
      'secondaryTextColor': '#6C3483',
      'secondaryBorderColor': '#A569BD'
    }
  }
}%%
graph TD
    A["Step 1:<br/>Write Shader Code<br/>(.metal file or String)"] --> B("Step 2:<br/>Create MTLCompileOptions")
    B --> C{"Step 3:<br/>Create MTLLibrary"}
    C --> D["Step 4:<br/>Get MTLFunction(s) by Name"]
    D --> E("Step 5:<br/>Specialize Function?")
    E -- Yes --> F["Use MTLFunctionConstantValues"]
    E -- No --> G{"Step 6:<br/>Create Pipeline State Descriptor"}
    F --> G
    G --> H["Set Functions in Descriptor"]
    H --> I("Step 7:<br/>Create MTL*PipelineState")
    I --> J["Step 8:<br/>Use PipelineState in Render/Compute Pass"]

    subgraph Inputs["Inputs"]
        X["Shader Source Code"] --> A
        Y["Configuration<br/>(Macros, Version, etc.)"] --> B
        Z["Runtime Constants<br/>(Optional)"] --> F
    end

    subgraph Using_Device["Using MTLDevice"]
        Dev("MTLDevice") --> C
        Dev --> I
    end

    subgraph Possible_Error["Possible Error"]
        Err("MTLLibraryError") -.-> C
        Err -.-> D
        Err -.-> F
        Err -.-> I
    end

    style A fill:#E8DAEF,stroke:#884EA0
    style B fill:#D5F5E3,stroke:#27AE60
    style C fill:#FCF3CF,stroke:#F1C40F
    style D fill:#FCF3CF,stroke:#F1C40F
    style E fill:#FDEDEC,stroke:#E74C3C
    style F fill:#EBF5FB,stroke:#3498DB
    style G fill:#FEF5E7,stroke:#F39C12
    style H fill:#FEF5E7,stroke:#F39C12
    style I fill:#D6EAF8,stroke:#2E86C1
    style J fill:#D1F2EB,stroke:#16A085

    style Dev fill:#FADBD8, stroke:#C0392B
    style Err fill:#fadbd8, stroke:#C0392B, stroke-dasharray: 5 5

    linkStyle 9 stroke:#c0392b,stroke-width:1px,color:gray;
    linkStyle 10 stroke:#c0392b,stroke-width:1px,color:gray
    linkStyle 11 stroke:#c0392b,stroke-width:1px,color:gray
    linkStyle 12 stroke:#c0392b,stroke-width:1px,color:gray

```

**Explanation:** Shows the sequential steps, inputs at different stages, the central role of the `MTLDevice`, and potential error points.

---

## Asynchronous Function Creation

This sequence diagram illustrates the difference between synchronous and asynchronous function creation, highlighting the non-blocking nature of the latter.

```mermaid
---
title: "Asynchronous Function Creation"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'sequence': { 'mirrorActors': false, 'showSequenceNumbers': true },
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#A9DFBF',
      'primaryTextColor': '#196F3D',
      'lineColor': '#58D68D',
      'primaryBorderColor': '#229954',
      'actorTextColor': '#E2E'
    }
  }
}%%
sequenceDiagram
    participant AppThread as Application Thread
    participant MetalDriver as Metal Driver / Compiler
    participant CallbackQueue as Dispatch Queue<br/>(Callback)

    Note over AppThread, MetalDriver: Synchronous Creation<br/>(e.g., makeFunction(name:constantValues:))
    
    AppThread->>+MetalDriver: makeFunction(...) throws
    Note over MetalDriver: Compiles Shader... <br/>(Blocks AppThread)
    MetalDriver-->>-AppThread: Return MTLFunction OR Throw Error
    AppThread->>AppThread: Process Result / Continue

    Note over AppThread, MetalDriver: Asynchronous Creation<br/>(e.g., makeFunction(name:constantValues:completionHandler:))
    
    AppThread->>+MetalDriver: makeFunction(..., completionHandler)
    MetalDriver-->>-AppThread: Return Immediately<br/>(Non-blocking)
    AppThread->>AppThread: Continue Other Work...

    Note over MetalDriver: Compiles Shader in Background...
    
    MetalDriver->>+CallbackQueue: Enqueue Completion Block
    CallbackQueue-->>-AppThread: Execute Completion<br/>(MTLFunction?, Error?)
    AppThread->>AppThread: Process Async Result

```


**Explanation:** Contrasts the blocking nature of synchronous calls with the immediate return and background processing + callback mechanism of asynchronous calls.

---

## Evolution of Metal Features (Simplified Timeline)

This Gantt chart provides a simplified view of when major feature categories discussed (related to the code snippet) were introduced across iOS versions.

```mermaid
---
title: "Evolution of Metal Features (Simplified Timeline)"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'fontFamily': 'Monospace',
    'themeVariables': {
        'primaryColor': '#D6EAF8',
        'primaryTextColor': '#21618C',
        'lineColor': '#85C1E9',
        'primaryBorderColor': '#5DADE2',
        'sectionTextColor': '#154360',
        'taskTextColor': '#1A5276',
        'gantt': {
          'tickColor': '#AEB6BF',
          'sectionBkgColor': '#EBEDEF',
          'gridColor': '#D5DBDB'
        }
    }
  }
}%%
gantt
    title Metal Feature Introduction Timeline (Related to Snippet)
    dateFormat  YYYY
    axisFormat  %Y
    %% Define Sections based on iOSMajor.Minor or Year roughly %%
    section iOS 8 (2014)
        Core Function/Library API : milestone, m1, 2014-06-01, 0d
        Basic Function Types (V/F/K): milestone, m2, 2014-06-01, 0d
    section iOS 9 (2015)
        MSL Language Versioning (1.x) : milestone, m3, 2015-06-01, 0d
    section iOS 10 (2016)
        Function Constants API : milestone, m4, 2016-06-01, 0d
        Tessellation (Patch Types) : milestone, m5, 2016-06-01, 0d
        Stage Input Attributes : milestone, m6, 2016-06-01, 0d
    section iOS 11 (2017)
        MSL 2.0 : milestone, m7, 2017-06-01, 0d
        Argument Encoders (Function-based) : milestone, m8, 2017-06-01, 0d
    section iOS 14 (2020)
        Dynamic Libraries : milestone, m9, 2020-06-01, 0d
        New Function Types (Visible/Intersection) : milestone, m10, 2020-06-01, 0d
        Function/Intersection Descriptors : milestone, m11, 2020-06-01, 0d
        Preserve Invariance Option : milestone, m12, 2020-06-01, 0d
    section iOS 16 (2022)
        Mesh/Object Shaders (Types): milestone, m13, 2022-06-01, 0d
        Library Optimization Levels: milestone, m14, 2022-06-01, 0d
        MSL 3.0: milestone, m15, 2022-06-01, 0d
        Symbol Visibility / Undefined Symbol Options: milestone, m16_4, 2023-03-01, 0d %% iOS 16.4 approx %%
        Max Threads Option: milestone, m17_4, 2023-03-01, 0d %% iOS 16.4 approx %%
    section iOS 18 (2024)
        Math Mode Options: milestone, m18, 2024-06-01, 0d
        Enable Logging Option: milestone, m19, 2024-06-01, 0d
        MSL 3.2: milestone, m20, 2024-06-01, 0d

```

**Explanation:** Visually maps features to the approximate time (iOS major version release) they became available, emphasizing the framework's growth. *Note: Exact dates are approximate based on typical WWDC release cycles.*

---

## Compile-Time vs. Runtime Configuration/Specialization

This diagram contrasts the two main points of configuring shader behavior discussed.

```mermaid
---
title: "Compile-Time vs. Runtime Configuration/Specialization"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#FCF3CF',
      'primaryTextColor': '#B7950B',
      'lineColor': '#F4D03F',
      'primaryBorderColor': '#F1C40F',
      'secondaryColor': '#EBF5FB',
      'secondaryTextColor': '#2E86C1',
      'secondaryBorderColor': '#5DADE2'
    }
  }
}%%
graph TD
    subgraph Compile_Time_Configuration["Compile-Time Configuration"]
    direction LR
        A["Shader Source<br/>(.metal/String)"] --> B("MTLCompileOptions")
        B -- Defines --> Ba["Preprocessor Macros"]
        B -- Defines --> Bb["Language Version"]
        B -- Defines --> Bc["Optimization Level"]
        B -- Defines --> Bd["Library Type"]
        B -- Defines --> Be["Math Mode"]
        B -- Defines --> Bf["Other flags..."]
        B --> C{"MTLDevice.makeLibrary(...)"}
        C --> D[("MTLLibrary")]
    end

    subgraph Runtime_Specialization["Runtime Specialization"]
    direction LR
        E[("MTLLibrary")] --> F{"makeFunction(name: constantValues: ...)"}
        F -- Uses --> G["MTLFunctionConstantValues"]
        G -- Contains --> Ga["Shader Constant Name -> Value"]
        F --> H[/"Specialized MTLFunction"/]
    end

    style A fill:#f8d7da, stroke:#721c24
    style B fill:#FCF3CF, stroke:#F1C40F
    style C fill:#d4edda, stroke:#155724
    style D fill:#d1ecf1, stroke:#0c5460
    style E fill:#d1ecf1, stroke:#0c5460
    style F fill:#d4edda, stroke:#155724
    style G fill:#EBF5FB, stroke:#5DADE2
    style H fill:#e2e3e5, stroke:#383d41

    linkStyle 0 stroke-width:2px, stroke: #F1C40F
    linkStyle 6 stroke-width:2px, stroke: #155724
    linkStyle 7 stroke-width:2px, stroke: #5DADE2

```

**Explanation:** Clearly separates the two phases: `MTLCompileOptions` are applied when the *library* is created from source, influencing the compiled code globally. `MTLFunctionConstantValues` are applied later when retrieving a *specific function* from the library, allowing runtime-defined specialization of that function instance.

---

## Dynamic Library Concept

This diagram illustrates the creation and usage of Metal dynamic libraries.

```mermaid
---
title: "Dynamic Library Concept"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  layout: elk
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#FDEDEC',
      'primaryTextColor': '#7B241C',
      'lineColor': '#F1948A',
      'primaryBorderColor': '#E74C3C',
      'secondaryColor': '#EAECEE',
      'secondaryTextColor': '#1C2833',
      'secondaryBorderColor': '#566573'
    }
  }
}%%
graph TD
    subgraph Create_Dynamic_Lib["Phase 1:<br/>Create Dynamic Library"]
    style Create_Dynamic_Lib fill:#EEF8,stroke:#7D3C98
        A["Utils Source<br/>(.metal)"] --> B("Compile Options: <br/> libraryType = .dynamic <br/> installName = '@loader_path/Utils.metallib'")
        B --> C{"MTLDevice.makeLibrary(...)"}
        C --> D["Utils.metallib <br/> (MTLLibrary - Dynamic)"]
    end

    subgraph Create_Exectuable_Lib["Phase 2:<br/>Create Executable Library Linking Dynamic Lib"]
    style Create_Exectuable_Lib fill:#EFF9,stroke:#7D3C98
        E["Main Shaders<br/>(.metal) <br/> #include <Utils/utils.h>"] --> F("Compile Options: <br/> libraryType = .executable <br/> libraries = [Utils.metallib Ref]")
        F --> G{"MTLDevice.makeLibrary(...)"}
        G --> H["Main.metallib <br/> (MTLLibrary - Executable)"]
        H --> I{"makeFunction('mainVertex')"}

        %% Links Symbols At Runtime via installName
        I <--> D
        
        I --> J["mainVertex<br/>(MTLFunction)"]
    end

    subgraph Usage["Phase 3:<br/>Usage"]
    style Usage fill:#FEE9,stroke:#7D3C98
        K["MTLRenderPipelineDescriptor"] --> L{"Set vertexFunction=mainVertex"}
        L --> M{"MTLDevice.makeRenderPipelineState(...)"}
        M --> N["Executable Pipeline State"]
    end

    %% Connect Phases
    D -- Used By --> F
    H -- Used To Get --> K


    style A fill:#F5EEF8,stroke:#7D3C98
    style E fill:#F5EEF8,stroke:#7D3C98
    style B fill:#FDEDEC,stroke:#7B241C
    style F fill:#FDEDEC,stroke:#7B241C
    style C fill:#d4edda,stroke:#155724
    style G fill:#d4edda,stroke:#155724
    style M fill:#d4edda,stroke:#155724
    style D fill:#EAECEE,stroke:#566573
    style H fill:#EAECEE,stroke:#566573
    style K fill:#e2e3e5,stroke:#383d41
    style L fill:#e2e3e5,stroke:#383d41
    style N fill:#d1f2eb,stroke:#16A085
    style I fill:#d1f2eb,stroke:#16A085
    style J fill:#d1f2eb,stroke:#16A085

    linkStyle 10 stroke: #E74C3C,stroke-dasharray: 5 5
    linkStyle 11 stroke: #7B241C
    linkStyle 12 stroke: #154360

```

**Explanation:** Breaks down the process into phases: creating the dynamic library with an `installName`, creating an executable library that *links* against the dynamic one (referencing it in compile options), and finally using a function from the executable library, triggering the runtime link to the dynamic library.

---

## Error Handling Context (Simplified)

This highlights where `MTLLibraryError` typically occurs within the workflow.

```mermaid
---
title: "Error Handling Context (Simplified)"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  layout: elk
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#FDEDEC',
      'primaryTextColor': '#7B241C',
      'lineColor': '#F1948A',
      'primaryBorderColor': '#E74C3C',
      'secondaryColor': '#EAECEE',
      'secondaryTextColor': '#1C2833',
      'secondaryBorderColor': '#566573'
    }
  }
}%%
graph TD
    A["Input:<br/>Shader Source + Compile Options"] --> B{"MTLDevice.makeLibrary(...)"}
    B -- Success --> C["MTLLibrary"]
    B -- Failure --> D["MTLLibraryError <br/> (e.g., compileFailure, fileNotFound)"]

    C --> E{"MTLLibrary.makeFunction(...)"}
    E -- Success --> F["MTLFunction"]
    E -- Failure --> G["MTLLibraryError <br/> (e.g., functionNotFound, internal)"]

    style D fill:#f8d7da, stroke:#721c24
    style G fill:#f8d7da, stroke:#721c24
    
```


**Explanation:** A focused view showing the creation steps (`makeLibrary`, `makeFunction`) as the primary points where `MTLLibraryError` can be thrown, indicating potential failure modes.


---
## Error Handling Structure

This diagram shows the `MTLLibraryError` structure and its associated error codes.

```mermaid
---
title: "Error Handling Structure"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%%%%%%% Available curve styles include the following keywords:
%% basis, bumpX, bumpY, cardinal, catmullRom, linear, monotoneX, monotoneY, natural, step, stepAfter, stepBefore.
%%{
  init: {
    'graph': { 'htmlLabels': false},
    'fontFamily': 'Monospace',
    'themeVariables': {
      'primaryColor': '#BB28',
      'primaryTextColor': '#FFF',
      'primaryBorderColor': '#7C33',
      'secondaryColor': '#0615',
      'textColor': '#000',
      'lineColor': '#F8B229'
    }
  }
}%%
graph TD
  subgraph Error_Handling["Error Handling"]
    A[MTLLibrary] -->|Can Throw| B("MTLLibraryError")
    B -- Contains --> C{"MTLLibraryError.Code"}
    C -->|Cases| D["unsupported (1)"]
    C -->|Cases| E["internal (2)"]
    C -->|Cases| F["compileFailure (3)"]
    C -->|Cases| G["compileWarning (4)"]
    C -->|Cases| H["functionNotFound (5) <br/><i>iOS 10.0+</i>"]
    C -->|Cases| I["fileNotFound (6) <br/><i>iOS 10.0+</i>"]
    B -- Domain --> K(("MTLLibraryErrorDomain <br/> String Constant"))
  end

  style B fill:#f9d,stroke:#333,stroke-width:2px
  style C fill:#f9f,stroke:#333,stroke-width:1px
```

**Explanation:**

*   Shows that methods in `MTLLibrary` can result in an `MTLLibraryError`.
*   The error object contains a `Code` enum specifying the type of error.
*   Lists the specific error codes defined.
*   References the `MTLLibraryErrorDomain` constant used to identify this error type within the `NSError` ecosystem.



---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---