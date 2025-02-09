---
created: 2024-12-07 04:58:55
url: https://developer.apple.com/documentation/compression
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---

# Compression
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---

Below is a comprehensive set of Mermaid diagrams for the `Compression` framework. These diagrams cover various aspects of the `Compression` framework, including class structures, initializers, properties, methods, enumerations, protocols, relationships, extensions, lifecycle, feature availability, data handling, integration, and best practices.

---

## **1. Class Structure and Hierarchy**

### **a. Core Class Diagram**
- **Purpose**: Illustrate the primary structure of the `Compression` framework, including its types, functions, and enumerations.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Structures**: `CompressionStream`
  - **Enumerations**: `CompressionAlgorithm`, `CompressionOptions`
  - **Functions**: `compression_encode_buffer`, `compression_decode_buffer`
  - **Classes**: `CompressionSession`

```mermaid
classDiagram
    class CompressionStream {
        +initialize(compression algorithm: CompressionAlgorithm, options: Int32) -> Bool
        +update(input: UnsafePointer<UInt8>, inputSize: Int, output: UnsafeMutablePointer<UInt8>, outputSize: Int) -> Int
        +finalize(output: UnsafeMutablePointer<UInt8>, outputSize: Int) -> Int
        +deinitialize() -> Void
    }

    class CompressionAlgorithm {
        <<enumeration>>
        +zlib
        +lzfse
        +lz4
    }

    class CompressionOptions {
        <<enumeration>>
        +default
        +heapBuffer
        +strideBuffer
    }

    class CompressionSession {
        +init(algorithm: CompressionAlgorithm, options: CompressionOptions)
        +encode(data: Data) -> Data?
        +decode(data: Data) -> Data?
        +close() -> Void
    }

    CompressionSession --> CompressionAlgorithm
    CompressionSession --> CompressionOptions
    CompressionStream --> CompressionAlgorithm
    CompressionStream --> CompressionOptions
```

---

## **2. Initializers Overview**

### **a. Initialization Methods Diagram**
- **Purpose**: Break down the various ways to instantiate `Compression` components.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **CompressionSession Initializers**
  - **CompressionStream Initializers**
  - **Algorithm Selection**

```mermaid
graph LR
    A[Compression Initializers] --> B[CompressionSession]
    A --> C[CompressionStream]
    A --> D[Algorithm Selection]

    B --> B1["init(algorithm: CompressionAlgorithm, options: CompressionOptions)"]
    C --> C1["initialize(algorithm: CompressionAlgorithm, options: Int32)"]
    D --> D1["CompressionAlgorithm.zlib"]
    D --> D2["CompressionAlgorithm.lzfse"]
    D --> D3["CompressionAlgorithm.lz4"]
```

---

## **3. Properties Breakdown**

### **a. Key Properties Diagram**
- **Purpose**: Detail the main properties of the `Compression` framework types.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **CompressionSession Properties**
  - **CompressionStream Properties**
  - **CompressionAlgorithm Attributes**

```mermaid
graph LR
    A[Compression Framework Properties] --> B[CompressionSession]
    A --> C[CompressionStream]
    A --> D[CompressionAlgorithm]

    B --> B1[algorithm: CompressionAlgorithm]
    B --> B2[options: CompressionOptions]
    B --> B3[isActive: Bool]

    C --> C1[currentAlgorithm: CompressionAlgorithm]
    C --> C2[bufferSize: Int]
    C --> C3[state: Int]

    D --> D1[zlib Description]
    D --> D2[lzfse Description]
    D --> D3[lz4 Description]
```

---

## **4. Methods Grouped by Functionality**

### **a. Compression Methods Diagram**
- **Purpose**: Categorize methods based on their roles in data compression and decompression.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Session Management**
  - **Encoding Methods**
  - **Decoding Methods**
  - **Stream Handling**

```mermaid
flowchart TD
    A[Compression Methods] --> B[Session Management]
    A --> C[Encoding]
    A --> D[Decoding]
    A --> E[Stream Handling]

    B --> B1["init(algorithm: CompressionAlgorithm, options: CompressionOptions)"]
    B --> B2["close()"]

    C --> C1["encode(data: Data) -> Data?"]
    C --> C2["compression_encode_buffer(...)"]

    D --> D1["decode(data: Data) -> Data?"]
    D --> D2["compression_decode_buffer(...)"]

    E --> E1["initialize(...)"]
    E --> E2["update(input:, output:)"]
    E --> E3["finalize(output:)"]
    E --> E4["deinitialize()"]
```

---

## **5. Enumerations and Configurations**

### **a. Enumerations Diagram**
- **Purpose**: Highlight the enums used within the `Compression` framework and their possible values.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **CompressionAlgorithm**
  - **CompressionOptions**

```mermaid
classDiagram
    class CompressionAlgorithm {
        <<enumeration>>
        +zlib
        +lzfse
        +lz4
    }

    class CompressionOptions {
        <<enumeration>>
        +default
        +heapBuffer
        +strideBuffer
    }

    CompressionAlgorithm --> CompressionOptions
```

---

## **6. Protocol Conformances**

### **a. Protocols Diagram**
- **Purpose**: Display the protocols that `Compression` framework types conform to and their impact.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Codable**
  - **SecureCoding**

```mermaid
classDiagram
    class CompressionSession {
        <<class>>
    }

    class Codable {
        <<protocol>>
    }

    class SecureCoding {
        <<protocol>>
    }

    CompressionSession ..|> Codable
    CompressionSession ..|> SecureCoding
```

---

## **7. Relationships with Other Classes**

### **a. Related Classes Diagram**
- **Purpose**: Illustrate how `Compression` interacts with other frameworks and classes.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **NSData**
  - **NSStream**
  - **URLSession**
  - **FileManager**
  - **Data**
  - **Third-Party Libraries**

```mermaid
flowchart TD
    A[Compression Framework] --> B[NSData]
    A --> C[NSStream]
    A --> D[URLSession]
    A --> E[FileManager]
    A --> F[Data]
    A --> G[Third-Party Libraries]

    B --> |Compress/Decompress| A
    C --> |Stream Data| A
    D --> |Network Data Compression| A
    E --> |File Compression| A
    F --> |Data Handling| A
    G --> |Integration| A
```

---

## **8. Extensions and Additional Functionalities**

### **a. Compression Extensions Diagram**
- **Purpose**: Showcase the additional functionalities provided through extensions.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Data Extensions**
  - **Stream Extensions**
  - **Error Handling Extensions**

```mermaid
classDiagram
    class Data {
        <<extension>>
        +compressed(using algorithm: CompressionAlgorithm) -> Data?
        +decompressed(using algorithm: CompressionAlgorithm) -> Data?
    }

    class NSStream {
        <<extension>>
        +compressStream(with algorithm: CompressionAlgorithm)
        +decompressStream(with algorithm: CompressionAlgorithm)
    }

    class CompressionError {
        <<extension>>
        +description: String
        +recoverySuggestion: String
    }

    Data --> CompressionAlgorithm
    NSStream --> CompressionAlgorithm
    CompressionError --> CompressionAlgorithm
```

### **b. Extensions Functionalities Flowchart**
- **Purpose**: Detail specific extended methods and their purposes.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Data Compression**
  - **Data Decompression**
  - **Stream Compression**
  - **Stream Decompression**
  - **Error Handling**

```mermaid
flowchart LR
    A[Compression Extensions] --> B[Data Compression]
    A --> C[Data Decompression]
    A --> D[Stream Compression]
    A --> E[Stream Decompression]
    A --> F[Error Handling]

    B --> B1["compressed(using: CompressionAlgorithm) -> Data?"]
    C --> C1["decompressed(using: CompressionAlgorithm) -> Data?"]
    D --> D1["compressStream(with: CompressionAlgorithm)"]
    E --> E1["decompressStream(with: CompressionAlgorithm)"]
    F --> F1["Handling Compression Errors"]
```

---

## **9. Lifecycle and Use Cases**

### **a. Lifecycle Flowchart**
- **Purpose**: Demonstrate the typical lifecycle of a compression operation within an application.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Initialization**
  - **Compression/Decompression**
  - **Usage**
  - **Finalization**
  - **Error Handling**

```mermaid
flowchart TD
    Start[Start Compression] --> Init[Initialize CompressionSession]
    Init --> Compress[Compress Data]
    Compress --> Use[Use Compressed Data]
    Use --> Finalize[Finalize Session]
    Finalize --> End[End]
    
    Compress -->|Error| HandleError[Handle Compression Error]
    HandleError --> End
```

### **b. Common Use Cases Diagram**
- **Purpose**: Outline the typical scenarios where the `Compression` framework is utilized.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **File Compression**
  - **Data Transmission**
  - **Caching Mechanisms**
  - **Memory Optimization**
  - **Network Requests**
  - **Third-Party Integrations**

```mermaid
flowchart TD
    A[Compression Use Cases] --> B[File Compression]
    A --> C[Data Transmission]
    A --> D[Caching Mechanisms]
    A --> E[Memory Optimization]
    A --> F[Network Requests]
    A --> G[Third-Party Integrations]

    B --> B1["Compressing files before saving"]
    C --> C2["Compressing data for transmission"]
    D --> D3["Storing compressed cache data"]
    E --> E4["Reducing memory footprint"]
    F --> F5["Compressing payloads in API requests"]
    G --> G6["Integrating with compression libraries"]
```

---

## **10. Feature Availability Timeline**

### **a. Feature Availability Gantt Chart**
- **Purpose**: Show when various `Compression` features were introduced across iOS versions.
- **Diagram Type**: `gantt`
- **Contents**:
  - **iOS Versions**: 9.0, 10.0, 11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0
  - **Features Introduced**: Core Compression API, CompressionSession, LZ4 support, LZFSE support, HEVC compression, Adaptive compression algorithms, Stream-based compression, Improved error handling.

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title Compression Framework Feature Availability

    section iOS 9.0
    Core Compression API         :done, des1, 2015-09-16, 2015-09-16

    section iOS 10.0
    CompressionSession Added    :done, des2, 2016-09-13, 2016-09-13

    section iOS 11.0
    LZ4 Support                 :done, des3, 2017-09-19, 2017-09-19
    LZFSE Support               :done, des4, 2017-09-19, 2017-09-19

    section iOS 12.0
    HEVC Compression Integration:done, des5, 2018-09-17, 2018-09-17

    section iOS 13.0
    Adaptive Compression Algorithms:done, des6, 2019-09-19, 2019-09-19

    section iOS 14.0
    Stream-Based Compression      :done, des7, 2020-09-16, 2020-09-16

    section iOS 15.0
    Improved Error Handling      :done, des8, 2021-09-20, 2021-09-20

    section iOS 16.0
    Enhanced Performance Optimizations:done, des9, 2022-09-12, 2022-09-12

    section iOS 17.0
    Advanced Compression Techniques:done, des10, 2023-09-18, 2023-09-18
```

---

## **11. Data Handling and Formats**

### **a. Compression Formats Handling Diagram**
- **Purpose**: Explain how the `Compression` framework handles different compression formats.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Supported Formats**: zlib, LZFSE, LZ4, HEVC
  - **Operations**: Compress, Decompress
  - **Functions**: `compression_encode_buffer`, `compression_decode_buffer`
  - **Sessions**: `CompressionSession`, `CompressionStream`

```mermaid
graph LR
    A[Compression Framework] --> B{Supported Formats}
    B --> C[zlib]
    B --> D[LZFSE]
    B --> E[LZ4]
    B --> F[HEVC]

    A --> G{Operations}
    G --> H[Compress]
    G --> I[Decompress]

    H --> J[compression_encode_buffer]
    I --> K[compression_decode_buffer]

    H --> L["CompressionSession.encode(data:)"]
    I --> M["CompressionSession.decode(data:)"]

    C --> H
    D --> H
    E --> H
    F --> H

    C --> I
    D --> I
    E --> I
    F --> I
    
```

---

## **12. Integration with Data Streams**

### **a. Stream Compression Methods Diagram**
- **Purpose**: Show how `Compression` methods are used within data streams.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Input Streams**
  - **Compression Process**
  - **Output Streams**
  - **Error Handling**

```mermaid
flowchart TD
    A[Data Streams Integration] --> B[Input Stream]
    B --> C[CompressionSession]
    C --> D[CompressionStream]
    D --> E[Output Stream]

    E --> F[Compressed Data Output]
    D --> |Error| G[Handle Compression Error]

    F --> H[Further Processing]
    G --> H
```

---

## **13. Summary and Best Practices**

### **a. Summary Diagram**
- **Purpose**: Provide a high-level overview of the `Compression` framework's key characteristics and functionalities.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Efficient Data Handling**
  - **Multiple Compression Algorithms**
  - **Stream-Based Processing**
  - **Robust Error Handling**
  - **Seamless Integration**
  - **Performance Optimizations**

```mermaid
graph LR
    A[Compression Framework] --> B[Efficient Data Handling]
    A --> C[Multiple Compression Algorithms]
    A --> D[Stream-Based Processing]
    A --> E[Robust Error Handling]
    A --> F[Seamless Integration]
    A --> G[Performance Optimizations]

    B --> B1[Fast Compression/Decompression]
    C --> C1[zlib, LZFSE, LZ4, HEVC]
    D --> D1[Streaming APIs]
    E --> E1[Comprehensive Error Management]
    F --> F1[Integration with NSData, NSStream]
    G --> G1[Optimized for Performance]
```

---

## **Best Practices for Using the Compression Framework**

1. **Choose the Right Algorithm**:
   - **zlib**: Suitable for general-purpose compression with a good balance between speed and compression ratio.
   - **LZFSE**: Optimized for Apple platforms with higher compression speeds.
   - **LZ4**: Best for scenarios requiring extremely fast compression/decompression.
   - **HEVC**: Ideal for high-efficiency video compression.

2. **Utilize Stream-Based APIs for Large Data**:
   - For handling large datasets or real-time data streams, prefer `CompressionStream` over buffer-based methods to manage memory efficiently.

3. **Handle Errors Gracefully**:
   - Implement comprehensive error handling to manage scenarios like unsupported algorithms, data corruption, or buffer overflows.

4. **Optimize Buffer Sizes**:
   - Adjust buffer sizes based on the data type and compression algorithm to achieve optimal performance.

5. **Leverage Compression Sessions**:
   - Use `CompressionSession` for managing the lifecycle of compression tasks, ensuring resources are properly allocated and released.

6. **Integrate with Existing Frameworks**:
   - Seamlessly integrate with `NSData`, `NSStream`, and other Apple frameworks to enhance data processing workflows.

7. **Profile and Benchmark**:
   - Regularly profile compression tasks to identify bottlenecks and optimize performance using tools like Instruments.

8. **Stay Updated with iOS Releases**:
   - Keep abreast of updates in the `Compression` framework to leverage new features and improvements introduced in the latest iOS versions.



---
**Licenses:**

- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).

---