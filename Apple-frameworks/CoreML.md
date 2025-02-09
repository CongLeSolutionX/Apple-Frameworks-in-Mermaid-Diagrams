---
created: 2024-12-07 03:31:00
reference_url: https://developer.apple.com/documentation/coreml/
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---

# Core ML
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---


## **1. Class Structure and Hierarchy**

### **a. Core Class Diagram**
- **Purpose**: Illustrate the primary structure of `MLModel`, including its properties, methods, and enumerations.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Properties**: Key attributes like `modelDescription`, `computeUnits`, `modelParameters`, etc.
  - **Methods**: Essential functions like initializers, `prediction()`, `modelDescription`, etc.
  - **Enumerations**: Nested enums such as `ComputeUnits`, `Error`, etc.

```mermaid
classDiagram
    class MLModel {
        +ModelDescription modelDescription
        +ComputeUnits computeUnits
        +ModelParameters modelParameters
        +MLModelConfiguration configuration
        +init(contentsOf: URL) throws
        +init(contentsOf: URL, configuration: MLModelConfiguration) throws
        +prediction(from: MLFeatureProvider) throws -> MLFeatureProvider
        +predictions(from: MLBatchProvider) throws -> MLBatchProvider
        // Additional properties and methods...
    }

    class ComputeUnits {
        <<enum>>
        +cpuOnly
        +cpuAndGPU
        +all
    }

    class Error {
        <<enum>>
        +invalidModel
        +predictionFailed
        +loadingFailed
    }

    MLModel --> ComputeUnits
    MLModel --> Error
```

---

## **2. Initializers Overview**

### **a. Initialization Methods Diagram**
- **Purpose**: Break down the various ways to instantiate `MLModel`.
- **Diagram Type**: `flowchart` or `graph LR`
- **Contents**:
  - **URL-Based Initializers**: `init(contentsOf:)`, `init(contentsOf:configuration:)`
  - **Bundle-Based Initializers**: `init(modelName:)`, `init(modelName:configuration:)`
  - **Data-Based Initializers**: `init(data:)`, `init(data:configuration:)`
  - **Serialization & Deserialization**: `init(serializedModel:configuration:)`

```mermaid
graph LR
    A[MLModel Initializers] --> B[URL-Based]
    A --> C[Bundle-Based]
    A --> D[Data-Based]
    A --> E[Serialization & Deserialization]

    B --> B1["init(contentsOf: URL) throws"]
    B --> B2["init(contentsOf: URL, configuration: MLModelConfiguration) throws"]
    
    C --> C1["init(modelName: String) throws"]
    C --> C2["init(modelName: String, configuration: MLModelConfiguration) throws"]
    
    D --> D1["init(data: Data) throws"]
    D --> D2["init(data: Data, configuration: MLModelConfiguration) throws"]
    
    E --> E1["init(serializedModel: Data, configuration: MLModelConfiguration) throws"]
```

---

## **3. Properties Breakdown**

### **a. Key Properties Diagram**
- **Purpose**: Detail the main properties of `MLModel`.
- **Diagram Type**: `graph LR` or `classDiagram`
- **Contents**:
  - **Model Information**: `modelDescription`, `modelParameters`
  - **Configuration**: `computeUnits`, `configuration`
  - **State**: `isLoaded`, `isRunning`
  - **Metadata**: `metadata`

```mermaid
graph LR
    A[MLModel Properties] --> B[Model Information]
    A --> C[Configuration]
    A --> D[State]
    A --> E[Metadata]

    B --> B1[modelDescription: ModelDescription]
    B --> B2[modelParameters: ModelParameters]

    C --> C1[computeUnits: ComputeUnits]
    C --> C2[configuration: MLModelConfiguration]

    D --> D1[isLoaded: Bool]
    D --> D2[isRunning: Bool]

    E --> E1["metadata: [String: Any]"]
    
```

---

## **4. Methods Grouped by Functionality**

### **a. Prediction Methods**
- **Purpose**: Categorize methods based on their roles in making predictions.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Single Prediction**: `prediction(from:)`, `prediction(input:)`
  - **Batch Predictions**: `predictions(from:)`, `predictions(inputs:)`
  - **Asynchronous Predictions**: `prediction(from:completionHandler:)`, `predictions(from:completionHandler:)`
  - **Custom Predictions**: `prediction(input:options:)`, `predictions(inputs:options:)`

```mermaid
flowchart TD
    A[MLModel Methods] --> B[Single Prediction]
    A --> C[Batch Predictions]
    A --> D[Asynchronous Predictions]
    A --> E[Custom Predictions]

    B --> B1["prediction(from: MLFeatureProvider) throws -> MLFeatureProvider"]
    B --> B2["prediction(input: Features) throws -> Prediction"]

    C --> C1["predictions(from: MLBatchProvider) throws -> MLBatchProvider"]
    C --> C2["predictions(inputs: [Features]) throws -> [Prediction]"]

    D --> D1["prediction(from: MLFeatureProvider, completionHandler: (Result<MLFeatureProvider, Error>) -> Void)"]
    D --> D2["predictions(from: MLBatchProvider, completionHandler: (Result<MLBatchProvider, Error>) -> Void)"]

    E --> E1["prediction(input: Features, options: MLPredictionOptions) throws -> Prediction"]
    E --> E2["predictions(inputs: [Features], options: MLPredictionOptions) throws -> [Prediction]"]
```

---

## **5. Enumerations and Configurations**

### **a. Enumerations Diagram**
- **Purpose**: Highlight the enums used within `MLModel` and their possible values.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **ComputeUnits**
  - **Error**
  - **ModelConfigurationOptions**

```mermaid
classDiagram
    class MLModel {
        <<enumeration>> ComputeUnits
        <<enumeration>> Error
        <<enumeration>> ModelConfigurationOptions
    }

    class ComputeUnits {
        +cpuOnly
        +cpuAndGPU
        +all
    }

    class Error {
        +invalidModel
        +predictionFailed
        +loadingFailed
    }

    class ModelConfigurationOptions {
        +allowLowPrecisionAccumulationOnGPU
        +useNeuralEngine
    }

    MLModel --> ComputeUnits
    MLModel --> Error
    MLModel --> ModelConfigurationOptions
    
```

### **b. Configuration Classes Diagram**
- **Purpose**: Show the relationship between `MLModel` and its configuration classes.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **MLModelConfiguration**
  - **MLBatchProvider**
  - **MLFeatureProvider**

```mermaid
classDiagram
    class MLModel {
        +configuration: MLModelConfiguration
    }

    class MLModelConfiguration {
        +computeUnits: ComputeUnits
        +allowLowPrecisionAccumulationOnGPU: Bool
        +useNeuralEngine: Bool
        // Additional configuration properties
    }

    class MLBatchProvider {
        // Batch provider properties and methods
    }

    class MLFeatureProvider {
        // Feature provider properties and methods
    }

    MLModel --> MLModelConfiguration
    MLModel --> MLBatchProvider
    MLModel --> MLFeatureProvider
```

---

## **6. Protocol Conformances**

### **a. Protocols Diagram**
- **Purpose**: Display the protocols that `MLModel` conforms to and their impact.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **NSCoding**
  - **NSSecureCoding**
  - **NSCopying**
  - **Sendable**

```mermaid
classDiagram
    class MLModel {
        <<open class>>
    }

    class NSCoding {
        <<protocol>>
    }

    class NSSecureCoding {
        <<protocol>>
    }

    class NSCopying {
        <<protocol>>
    }

    class Sendable {
        <<protocol>>
    }

    MLModel ..|> NSCoding
    MLModel ..|> NSSecureCoding
    MLModel ..|> NSCopying
    MLModel ..|> Sendable
```

---

## **7. Relationships with Other Classes**

### **a. Related Classes Diagram**
- **Purpose**: Illustrate how `MLModel` interacts with other Core ML classes and frameworks.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **MLFeatureProvider**: Supplies input features for predictions.
  - **MLBatchProvider**: Supplies batches of input features.
  - **MLPredictionOptions**: Configures prediction behavior.
  - **MLModelConfiguration**: Configures model parameters.
  - **ModelDescription**: Describes the model's input and output.
  - **ModelParameters**: Contains the parameters of the model.
  - **ResultsHandler**: Handles asynchronous prediction results.
  - **MLComputeUnits**: Specifies computation resources.

```mermaid
flowchart TD
    A[MLModel] --> B[MLFeatureProvider]
    A --> C[MLBatchProvider]
    A --> D[MLPredictionOptions]
    A --> E[MLModelConfiguration]
    A --> F[ModelDescription]
    A --> G[ModelParameters]
    A --> H[ResultsHandler]
    A --> I[MLComputeUnits]

    B --> |supplies input| A
    C --> |supplies batch inputs| A
    D --> |configures prediction| A
    E --> |configures model| A
    F --> |describes inputs/outputs| A
    G --> |contains model parameters| A
    H --> |handles async results| A
    I --> |specifies compute resources| A
    
```

---

## **8. Extensions and Additional Functionalities**

### **a. MLModel Extensions Diagram**
- **Purpose**: Showcase the additional functionalities provided through extensions.
- **Diagram Type**: `classDiagram`
- **Contents**:
  - **Model Loading Extensions**
  - **Prediction Extensions**
  - **Serialization Extensions**

```mermaid
classDiagram
    class MLModel {
        <<open class>>
    }

    class MLModelExtensions {
        <<extension>>
        +loadModel(from: URL, completionHandler: (Result<MLModel, Error>) -> Void)
        +saveModel(to: URL) throws
        +batchPrediction(from: MLBatchProvider, completionHandler: (Result<MLBatchProvider, Error>) -> Void)
        // Additional extended methods
    }

    MLModel <-- MLModelExtensions
```

### **b. Extensions Functionalities Flowchart**
- **Purpose**: Detail specific extended methods and their purposes.
- **Diagram Type**: `flowchart LR`
- **Contents**:
  - **Model Loading**
  - **Batch Predictions**
  - **Model Serialization**

```mermaid
flowchart LR
    A[MLModel Extensions] --> B[Model Loading]
    A --> C[Batch Predictions]
    A --> D[Model Serialization]

    B --> B1["loadModel(from: URL, completionHandler: (Result<MLModel, Error>) -> Void)"]
    C --> C1["batchPrediction(from: MLBatchProvider, completionHandler: (Result<MLBatchProvider, Error>) -> Void)"]
    D --> D1["saveModel(to: URL) throws"]
```

---

## **9. Lifecycle and Use Cases**

### **a. Lifecycle Flowchart**
- **Purpose**: Demonstrate the typical lifecycle of an `MLModel` within an application.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Initialization**
  - **Configuration**
  - **Loading**
  - **Predictions**
  - **Updating**
  - **Caching**
  - **Termination**

```mermaid
flowchart TD
    Start[Start] --> Init[Initialize MLModel]
    Init --> Config[Configure MLModel]
    Config --> Load[Load Model]
    Load --> Predict[Make Predictions]
    Predict --> Update[Update Model Configuration]
    Update --> Cache[Cache Model]
    Cache --> Terminate[Terminate Model Usage]
    Terminate --> End[End]
```

### **b. Common Use Cases Diagram**
- **Purpose**: Outline the typical scenarios where `MLModel` is utilized.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Image Classification**
  - **Natural Language Processing**
  - **Recommendation Systems**
  - **Anomaly Detection**
  - **Speech Recognition**
  - **Time Series Forecasting**
  - **Custom Model Integration**

```mermaid
flowchart TD
    A[MLModel Use Cases] --> B[Image Classification]
    A --> C[Natural Language Processing]
    A --> D[Recommendation Systems]
    A --> E[Anomaly Detection]
    A --> F[Speech Recognition]
    A --> G[Time Series Forecasting]
    A --> H[Custom Model Integration]
```

---

## **10. Feature Availability Timeline**

### **a. Feature Availability Gantt Chart**
- **Purpose**: Show when various `MLModel` features were introduced across iOS versions.
- **Diagram Type**: `gantt`
- **Contents**:
  - **iOS Versions**: 11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0
  - **Features Introduced**: Core ML integration, Swift support, Batch predictions, Asynchronous predictions, Custom compute units, Model quantization, On-device training.

```mermaid
gantt
    dateFormat  YYYY-MM-DD
    title MLModel Feature Availability

    section iOS 11.0
    Core ML Integration          :done, des1, 2017-09-19, 2017-09-19

    section iOS 12.0
    Swift Support                :done, des2, 2018-09-17, 2018-09-17

    section iOS 13.0
    Batch Predictions            :done, des3, 2019-09-19, 2019-09-19
    On-device Training           :done, des4, 2019-09-19, 2019-09-19

    section iOS 14.0
    Custom Compute Units         :done, des5, 2020-09-16, 2020-09-16

    section iOS 15.0
    Asynchronous Predictions     :done, des6, 2021-09-20, 2021-09-20
    Model Quantization           :done, des7, 2021-09-20, 2021-09-20

    section iOS 16.0
    Enhanced Model Serialization :done, des8, 2022-09-12, 2022-09-12

    section iOS 17.0
    On-device Training Enhancements :done, des9, 2023-09-18, 2023-09-18
    Real-time Batch Predictions      :done, des10, 2023-09-18, 2023-09-18
```

---

## **11. Data Handling and Formats**

### **a. Data Format Handling Diagram**
- **Purpose**: Explain how `MLModel` handles different model data formats.
- **Diagram Type**: `graph LR`
- **Contents**:
  - **Core ML Models**: `.mlmodel`, `.mlmodelc`
  - **ONNX Models**: `.onnx`
  - **TensorFlow Models**: `.pb`, `.tflite`
  - **Custom Models**: `.custom`

```mermaid
graph LR
    A[MLModel] --> B{Model Data Formats}
    B --> C["Core ML (.mlmodel, .mlmodelc)"]
    B --> D["ONNX (.onnx)"]
    B --> E["TensorFlow (.pb, .tflite)"]
    B --> F["Custom (.custom)"]

    C --> C1[".mlmodel"]
    C --> C2[".mlmodelc"]
    D --> D1[".onnx"]
    E --> E1[".pb"]
    E --> E2[".tflite"]
    F --> F1[".custom"]
    
```

---

## **12. Integration with Other Frameworks**

### **a. Integration Methods Diagram**
- **Purpose**: Show how `MLModel` integrates with other Apple frameworks and services.
- **Diagram Type**: `flowchart TD`
- **Contents**:
  - **Vision Framework**: Image analysis, object detection.
  - **Natural Language Framework**: Text processing, sentiment analysis.
  - **Create ML**: Model training and creation.
  - **Core Graphics**: Rendering model outputs.
  - **UIKit**: Displaying prediction results in UI.
  - **SwiftUI**: Binding predictions to UI components.

```mermaid
flowchart TD
    A[MLModel Integration] --> B[Vision Framework]
    A --> C[Natural Language Framework]
    A --> D[Create ML]
    A --> E[Core Graphics]
    A --> F[UIKit]
    A --> G[SwiftUI]

    B --> B1[Image Analysis]
    B --> B2[Object Detection]

    C --> C1[Text Processing]
    C --> C2[Sentiment Analysis]

    D --> D1[Model Training]
    D --> D2[Model Creation]

    E --> E1[Rendering Outputs]

    F --> F1[Display Predictions]

    G --> G1[Bind Predictions to UI]
```

---

## **13. Summary and Best Practices**

### **a. Summary Diagram**
- **Purpose**: Provide a high-level overview of `MLModel`'s key characteristics and functionalities.
- **Diagram Type**: `graph LR` or `mindmap`
- **Contents**:
  - **Versatile Initialization**
  - **Advanced Prediction Options**
  - **Performance Optimizations**
  - **Data Format Flexibility**
  - **Seamless Integration**
  - **Robust Error Handling**

```mermaid
graph LR
    A[MLModel] --> B[Versatile Initialization]
    A --> C[Advanced Prediction Options]
    A --> D[Performance Optimizations]
    A --> E[Data Format Flexibility]
    A --> F[Seamless Integration]
    A --> G[Robust Error Handling]

    B --> B1[Multiple Initializers]
    C --> C1[Single and Batch Predictions]
    D --> D1[Custom Compute Units]
    E --> E1[Support for Various Formats]
    F --> F1[Integration with Vision, NLP, SwiftUI]
    G --> G1[Comprehensive Error Types]
```

---