---
created: 2024-12-07 04:58:55
url: https://developer.apple.com/documentation/metal/mtlcommandqueue
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---

# MTLCommandQueue
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---

Below is a comprehensive and organized set of Mermaid diagrams for the `MTLCommandQueue` class. Each section includes a brief explanation followed by the corresponding Mermaid diagram.

---

## **1. Class Structure and Hierarchy**

### **a. Core Class Diagram**
- **Purpose**: Illustrate the primary structure of `MTLCommandQueue`, including its properties, methods, and any related enumerations.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Properties**: Key attributes like `device`, `label`, `commandBufferCount`, etc.
  - **Methods**: Essential functions like `commandBuffer()`, `submit()`, `insertDebugCaptureBoundary()`, etc.
  - **Relationships**: Associations with other Metal classes like `MTLDevice`, `MTLCommandBuffer`.

```mermaid
classDiagram
    class MTLCommandQueue {
        +device: MTLDevice
        +label: String?
        +commandBufferCount: UInt
        +maxCommandBufferCount: UInt
        +commandBufferRetentionInterval: TimeInterval
        +currentSampleIndex: UInt
        +currentSampleBufferIndex: UInt
        +isImageStoreSupported: Bool
        +retainedResources: [AnyObject]
        +isCommandBufferResourceStateTrackingEnabled: Bool
        +supportedTextureFormats: [MTLPixelFormat]
        
        +commandBuffer() -> MTLCommandBuffer
        +insertDebugCaptureBoundary()
        +enqueue()
        +commit()
        +addScheduledHandler(_ handler: @escaping (MTLCommandQueue) -> Void)
        +waitUntilCompleted()
    }
    
    MTLCommandQueue --> MTLDevice
    MTLCommandQueue --> MTLCommandBuffer
```

---

## **2. Initializers Overview**

### **a. Initialization Methods Diagram**
- **Purpose**: Break down the various ways to instantiate `MTLCommandQueue`.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Device-Based Initializers**: Typically instantiated via `MTLDevice`.
  - **Configuration Options**: Setting labels and other configurations post-initialization.

```mermaid
graph LR
    A[MTLCommandQueue Initialization] --> B[Via MTLDevice]
    B --> B1["device.makeCommandQueue() -> MTLCommandQueue?"]
    
    A --> C[Set Properties]
    C --> C1["label: String?"]
    C --> C2["commandBufferRetentionInterval: TimeInterval"]
    C --> C3["isCommandBufferResourceStateTrackingEnabled: Bool"]
```

---

## **3. Properties Breakdown**

### **a. Key Properties Diagram**
- **Purpose**: Detail the main properties of `MTLCommandQueue`.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Device Association**
  - **Labeling and Identification**
  - **Command Buffer Management**
  - **Resource Tracking**
  - **Supported Formats**

```mermaid
graph LR
    A[MTLCommandQueue Properties] --> B[Device Association]
    A --> C[Labeling & Identification]
    A --> D[Command Buffer Management]
    A --> E[Resource Tracking]
    A --> F[Supported Formats]
    
    B --> B1[device: MTLDevice]
    
    C --> C1[label: String?]
    
    D --> D1[commandBufferCount: UInt]
    D --> D2[maxCommandBufferCount: UInt]
    
    E --> E1[isCommandBufferResourceStateTrackingEnabled: Bool]
    E --> E2["retainedResources: [AnyObject]"]
    
    F --> F1["supportedTextureFormats: [MTLPixelFormat]"]
    
```


---

## **4. Methods Grouped by Functionality**

### **a. Command Buffer Management Methods**
- **Purpose**: Group methods related to creating and managing command buffers.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Creation**: `commandBuffer()`
  - **Boundary Insertion**: `insertDebugCaptureBoundary()`
  - **Enqueuing & Committing**: `enqueue()`, `commit()`
  - **Completion Handling**: `waitUntilCompleted()`

```mermaid
flowchart TD
    A[MTLCommandQueue Methods] --> B[Command Buffer Management]
    
    B --> B1["commandBuffer() -> MTLCommandBuffer"]
    B --> B2["insertDebugCaptureBoundary()"]
    B --> B3["enqueue()"]
    B --> B4["commit()"]
    B --> B5["waitUntilCompleted()"]
```

### **b. Scheduling & Handlers**
- **Purpose**: Categorize methods related to scheduling and handling command queue events.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Handlers**: `addScheduledHandler(_:)`

```mermaid
flowchart TD
    A[MTLCommandQueue Methods] --> C[Scheduling & Handlers]
    
    C --> C1["addScheduledHandler(_ handler: @escaping (MTLCommandQueue) -> Void)"]
```

### **c. Profiling & Debugging**
- **Purpose**: Highlight methods used for profiling and debugging command queues.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Debug Boundaries**: `insertDebugCaptureBoundary()`

```mermaid
flowchart TD
    A[MTLCommandQueue Methods] --> D[Profiling & Debugging]
    
    D --> D1["insertDebugCaptureBoundary()"]
```

---

## **5. Enumerations and Configurations**

### **a. Enumerations Diagram**
- **Purpose**: Highlight any enums associated with `MTLCommandQueue` and their possible values.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **No specific enums**: `MTLCommandQueue` does not define its own enumerations but may use enums from related Metal classes.

```mermaid
classDiagram
    class MTLCommandQueue {
        // No specific enums
    }
    
    %% Example of related enum
    class MTLCommandBufferStatus {
        <<enum>>
        +statusNotEnqueued
        +statusEnqueued
        +statusCommitted
        +statusScheduled
        +statusCompleted
        +statusError
    }
    
    MTLCommandQueue --> MTLCommandBufferStatus
```

### **b. Configuration Classes Diagram**
- **Purpose**: Show the relationship between `MTLCommandQueue` and its configuration classes if any.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **No direct configuration classes**: Configuration is typically handled through properties and related Metal objects.

```mermaid
classDiagram
    class MTLCommandQueue {
        +label: String?
        +commandBufferRetentionInterval: TimeInterval
        +isCommandBufferResourceStateTrackingEnabled: Bool
    }
    
    %% No separate configuration classes
```

---

## **6. Protocol Conformances**

### **a. Protocols Diagram**
- **Purpose**: Display the protocols that `MTLCommandQueue` conforms to and their impact.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **NSObject**
  - **NSCopying**
  - **MTLResourceStateCommand**

```mermaid
classDiagram
    class MTLCommandQueue {
        <<class>>
    }
    
    class NSObject {
        <<protocol>>
    }
    
    class NSCopying {
        <<protocol>>
    }
    
    class MTLResourceStateCommand {
        <<protocol>>
    }
    
    MTLCommandQueue --|> NSObject
    MTLCommandQueue --|> NSCopying
    MTLCommandQueue --|> MTLResourceStateCommand
```

---

## **7. Relationships with Other Classes**

### **a. Related Classes Diagram**
- **Purpose**: Illustrate how `MTLCommandQueue` interacts with other Metal classes and frameworks.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **MTLDevice**: The device associated with the command queue.
  - **MTLCommandBuffer**: Command buffers created from the queue.
  - **MTLCommandEncoder**: Encoders used within command buffers.
  - **MTLFence**: Synchronization fences.
  - **Metal Framework Components**: Interaction with shaders and pipelines.

```mermaid
flowchart TD
    A[MTLCommandQueue] --> B[MTLDevice]
    A --> C[MTLCommandBuffer]
    A --> D[MTLCommandEncoder]
    A --> E[MTLFence]
    A --> F[MTLLibrary]
    A --> G[MTLRenderPipelineState]
    
    B --> |Creates| A
    A --> |Creates| C
    C --> |Uses| D
    C --> |Synchronizes with| E
    C --> |Utilizes| F
    D --> |Configures| G
```

---

## **8. Extensions and Additional Functionalities**

### **a. MTLCommandQueue Extensions Diagram**
- **Purpose**: Showcase the additional functionalities provided through extensions.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Debugging Extensions**
  - **Synchronization Extensions**

```mermaid
classDiagram
    class MTLCommandQueue {
        <<class>>
    }
    
    class MTLCommandQueueExtensions {
        <<extension>>
        +insertDebugCaptureBoundary()
        +addScheduledHandler(_:)
        // Additional extended methods
    }
    
    MTLCommandQueue <-- MTLCommandQueueExtensions
```

### **b. Extensions Functionalities Flowchart**
- **Purpose**: Detail specific extended methods and their purposes.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Debug Capture Boundaries**
  - **Scheduled Handlers**
  
```mermaid
flowchart LR
    A[MTLCommandQueue Extensions] --> B[Debug Capture Boundaries]
    A --> C[Scheduled Handlers]
    
    B --> B1["insertDebugCaptureBoundary()"]
    C --> C1["addScheduledHandler(_ handler: @escaping (MTLCommandQueue) -> Void)"]
```

---

## **9. Lifecycle and Use Cases**

### **a. Lifecycle Flowchart**
- **Purpose**: Demonstrate the typical lifecycle of a `MTLCommandQueue` within an application.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Initialization**
  - **Command Buffer Creation**
  - **Encoding Commands**
  - **Submission**
  - **Execution**
  - **Completion**

```mermaid
flowchart TD
    Start[Start] --> Init[Initialize MTLCommandQueue]
    Init --> CreateBuffer[Create MTLCommandBuffer]
    CreateBuffer --> Encode[Encode Commands]
    Encode --> Submit[Submit Command Buffer]
    Submit --> Execute[GPU Execution]
    Execute --> Complete[Completion & Cleanup]
    Complete --> End[End]
```

### **b. Common Use Cases Diagram**
- **Purpose**: Outline the typical scenarios where `MTLCommandQueue` is utilized.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Rendering Frames**
  - **Compute Operations**
  - **Resource Synchronization**
  - **Debugging GPU Commands**
  - **Profiling Performance**
  
```mermaid
flowchart TD
    A[MTLCommandQueue Use Cases] --> B[Rendering Frames]
    A --> C[Compute Operations]
    A --> D[Resource Synchronization]
    A --> E[Debugging GPU Commands]
    A --> F[Profiling Performance]
    
    B --> B1["Encoding Render Commands"]
    C --> C1["Dispatching Compute Shaders"]
    D --> D1["Using MTLFence for Sync"]
    E --> E1["Inserting Debug Boundaries"]
    F --> F1["Measuring Command Buffer Execution"]
```

---

## **10. Feature Availability Timeline**

### **a. Feature Availability Gantt Chart**
- **Purpose**: Show when various `MTLCommandQueue` features were introduced across Metal versions and corresponding Apple platforms.
- **Diagram Type**: `gantt`
- **Contents**:
  - **Metal Versions**: Metal 1.0, Metal 2.0, Metal 3.0, etc.
  - **Features Introduced**: Command buffer retention, debug capture boundaries, scheduled handlers, etc.

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title MTLCommandQueue Feature Availability

    section Metal 1.0
    Basic Command Queue            :done, des1, 2014-06-04, 2014-06-04

    section Metal 2.0
    Command Buffer Retention       :done, des2, 2016-09-19, 2016-09-19
    Debug Capture Boundaries       :done, des3, 2016-09-19, 2016-09-19

    section Metal 3.0
    Scheduled Handlers             :done, des4, 2022-06-06, 2022-06-06
    Enhanced Profiling Tools       :done, des5, 2022-06-06, 2022-06-06

    section Future Releases
    %% // Placeholder for future features  %%
    
```

---

## **11. Data Handling and Formats**

### **a. Command Buffer Handling Diagram**
- **Purpose**: Explain how `MTLCommandQueue` manages different command buffer types and their formats.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Standard Command Buffers**
  - **Concurrent Command Buffers**
  - **Resource State Tracking**
  - **GPU-Driven Rendering**

```mermaid
graph LR
    A[MTLCommandQueue] --> B[Command Buffer Types]
    A --> C[Resource State Tracking]
    A --> D[GPU-Driven Rendering]
    
    B --> B1[Standard Command Buffers]
    B --> B2[Concurrent Command Buffers]
    
    C --> C1[isCommandBufferResourceStateTrackingEnabled]
    C --> C2[retainedResources]
    
    D --> D1[Encoding GPU Commands]
    D --> D2[Synchronizing Resources]
```

---

## **12. Integration with Rendering Pipelines**

### **a. Rendering Pipeline Integration Diagram**
- **Purpose**: Show how `MTLCommandQueue` integrates within the Metal rendering pipeline.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **MTLDevice**
  - **MTLCommandQueue**
  - **MTLCommandBuffer**
  - **MTLRenderCommandEncoder**
  - **GPU Execution**

```mermaid
flowchart TD
    A[MTLDevice] --> B[MTLCommandQueue]
    B --> C[MTLCommandBuffer]
    C --> D[MTLRenderCommandEncoder]
    D --> E[Encoding Render Commands]
    E --> F[Submit to GPU]
    F --> G[GPU Execution]
    G --> H[Rendered Output]
```

---

## **13. Summary and Best Practices**

### **a. Summary Diagram**
- **Purpose**: Provide a high-level overview of `MTLCommandQueue`'s key characteristics and functionalities.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Efficient Command Management**
  - **Robust Debugging Tools**
  - **Enhanced Performance Profiling**
  - **Seamless Integration with Metal Pipeline**
  - **Scalability and Flexibility**

```mermaid
graph LR
    A[MTLCommandQueue] --> B[Efficient Command Management]
    A --> C[Robust Debugging Tools]
    A --> D[Enhanced Performance Profiling]
    A --> E[Seamless Integration with Metal Pipeline]
    A --> F[Scalability and Flexibility]
    
    B --> B1[Create and Submit Command Buffers]
    C --> C1[Insert Debug Boundaries]
    D --> D1[Measure Execution Times]
    E --> E1[Integrate with Render and Compute Pipelines]
    F --> F1[Handle Concurrent Command Buffers]
```

### **b. Best Practices Diagram**
- **Purpose**: Highlight best practices when using `MTLCommandQueue`.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Optimize Command Buffer Usage**
  - **Utilize Debugging Tools**
  - **Leverage Resource State Tracking**
  - **Profile and Monitor Performance**
  - **Manage Synchronization Efficiently**

```mermaid
graph LR
    A[Best Practices for MTLCommandQueue] --> B[Optimize Command Buffer Usage]
    A --> C[Utilize Debugging Tools]
    A --> D[Leverage Resource State Tracking]
    A --> E[Profile and Monitor Performance]
    A --> F[Manage Synchronization Efficiently]
    
    B --> B1[Reuse Command Buffers]
    B --> B2[Minimize Command Buffer Retention]
    
    C --> C1[Insert Debug Boundaries]
    C --> C2[Use Scheduled Handlers]
    
    D --> D1[Enable Resource State Tracking]
    D --> D2[Retain Necessary Resources]
    
    E --> E1[Use Profiling Tools to Identify Bottlenecks]
    E --> E2[Monitor GPU Performance Metrics]
    
    F --> F1[Use MTLFence for Synchronization]
    F --> F2[Avoid Race Conditions]
```

---

## **Conclusion**

The `MTLCommandQueue` is a pivotal class within the Metal framework, responsible for managing command buffers that encapsulate GPU commands. Proper understanding and utilization of its properties, methods, and integrations ensure efficient GPU operations, robust debugging, and optimal performance in graphics and compute-intensive applications.

**Best Practices Summary**:
- **Efficient Command Management**: Reuse command buffers and manage their retention wisely to optimize memory usage.
- **Robust Debugging**: Utilize debug capture boundaries and scheduled handlers to trace and debug GPU commands effectively.
- **Performance Profiling**: Regularly profile command queues to identify and mitigate performance bottlenecks.
- **Synchronization**: Implement synchronization mechanisms like `MTLFence` to ensure data consistency and prevent race conditions.
- **Resource Tracking**: Enable and leverage resource state tracking to manage resource dependencies and lifecycles efficiently.

By adhering to these practices and fully leveraging the capabilities of `MTLCommandQueue`, developers can harness the full power of Metal to create high-performance, GPU-accelerated applications.

---

Explore detailed information on complex processes and pipelines that integrate `MTLCommandQueue` in the documentation page section below: 

`Complexed-processes-in-Mermaid-diagrams/MTLCommandQueue_IntegrationWithMetalRenderingPipeline.md`