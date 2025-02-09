---
created: 2024-12-07 04:58:55
url:
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---

# AVFoundation - Image and Video Processing Pipelines
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---

Here are the `AVFoundation` diagrams, categorized for clarity, and drawing parallels to the Metal rendering pipeline where appropriate.

## 1. High-Level Overview of AVFoundation Pipelines

This diagram illustrates the three primary pipelines within `AVFoundation`: Capture, Processing, and Playback. It uses similar concepts from the Metal Command pipeline.

```mermaid
flowchart TD
    subgraph Capture
        A[AVCaptureSession] -- Configures --> B(AVCaptureInput)
        B -- Provides --> C{AVCaptureOutput}
        C -- Data --> D[Capture Data]
    end

    subgraph Processing
        E[AVAsset] -- Loads --> F(AVComposition)
        F -- Edits --> G[AVVideoComposition]
        G -- Filters --> H{Core Image}
        H -- Effects --> I[Processed Output]
        I--Exports --> J(AVAssetExportSession)
    end
    subgraph Playback
        K[AVPlayerItem] -- Loads --> L[AVPlayer]
        L -- Controls --> M{AVPlayerLayer/AVRoutePickerView}
        M -- Displays --> N[Video Output]
        L -- Controls --> O[Audio Output]
    end

    style A fill:#911,stroke:#333,stroke-width:2px
    style E fill:#4f15,stroke:#333,stroke-width:2px
    style K fill:#741,stroke:#333,stroke-width:2px
```

**Explanation:**

*   **Capture:**  Similar to how `MTLCommandQueue` initiates rendering, `AVCaptureSession` starts the capture process, managing inputs (camera, microphone) and outputs (data streams).
*   **Processing:** `AVAsset` (like a source texture in Metal) is manipulated using `AVComposition` and `AVVideoComposition` (analogous to `MTLRenderCommandEncoder` operations). Core Image filters are applied, and the result is exported using `AVAssetExportSession`.
*   **Playback:** `AVPlayerItem` (like a processed texture or render target) is loaded into `AVPlayer`, which controls playback through `AVPlayerLayer` (similar to presenting a drawable) or `AVRoutePickerView`.

## 2. Detailed AVAsset Editing and Composition Pipeline

This diagram focuses on the video editing and composition process, highlighting the track-based model and time manipulation.

```mermaid
graph TD
    A[AVAsset] --> B{AVMutableComposition}
        B -- Creates --> C[AVMutableCompositionTrack: Video]
        B -- Creates --> D[AVMutableCompositionTrack: Audio]
        C -- Inserts --> E[AVAssetTrack: Video Source 1]
        C -- Inserts --> F[AVAssetTrack: Video Source 2]
        D -- Inserts --> G[AVAssetTrack: Audio Source]
        B --> H[AVVideoComposition]
        H -- Applies --> I{AVVideoCompositionInstruction}
        I -- Contains --> J[AVVideoCompositionLayerInstruction]
        J -- Defines --> K[Transform, Opacity, Crop]
        H -- Uses --> L[Core Image Filters]
        L -- For --> M[Custom Video Compositor]
        B --> N[AVAudioMix]
        N -- Applies --> O{AVAudioMixInputParameters}
        O -- Defines --> P[Volume, Panning]
        B --> Q[AVAssetExportSession]
        Q -- Exports --> R[Processed AVAsset]
        
classDef object fill:#771f,stroke:#333,stroke-width:2px;
class A,R object;
class B,H,N,Q,I internal-obj;

```

**Explanation:**

*   **AVMutableComposition**: Like a `MTLCommandBuffer` that aggregates commands, it combines multiple assets' tracks.
*   **AVMutableCompositionTrack**: Represents a track within the composition (video or audio).
*   **AVAssetTrack**: Represents a track from a source asset.
*   **AVVideoComposition**:  Similar to a `MTLRenderPipelineState`, it defines how video frames are processed with instructions and layer instructions.
*   **AVVideoCompositionInstruction**: Specifies operations for a time range.
*   **AVVideoCompositionLayerInstruction**: Specifies operations for a layer within an instruction (transform, opacity, etc.). This is where you would set up transitions or other visual effects just as we do in shaders in Metal.
*   **Core Image Filters**: Can be used for custom video compositing.
*   **AVAudioMix**: Controls audio mixing.
*   **AVAudioMixInputParameters**: Sets parameters for audio tracks.
*   **AVAssetExportSession**: Similar to submitting a command buffer for execution, it exports the composed asset.

## 3. AVFoundation Capture Pipeline with Data Output

This diagram expands the capture pipeline, showing how data is captured from various inputs and directed to different outputs.

```mermaid
graph TD
    A[AVCaptureSession] -->|Manages| B(AVCaptureDeviceInput)
    A -->|Manages| C(AVCaptureOutput)
    B -->|Represents| D{AVCaptureDevice}
    D -.->|Camera| E[Front Camera]
    D -.->|Microphone| F[Built-in Microphone]
    C -->|Data| G{AVCaptureVideoDataOutput}
    C -->|Data| H{AVCaptureAudioDataOutput}
    C -->|Metadata| I{AVCaptureMetadataOutput}
    C -->|Still Image| J[AVCapturePhotoOutput]
    G -->|Video Frames| K[Process Video Frames]
    H -->|Audio Samples| L[Process Audio Samples]
    I -->|Metadata Objects| M[Process Metadata]
    J -->|Photo| N[Capture Photo]

    
    classDef devices fill:#f193,stroke:#333,stroke-width:2px;
    classDef outputs fill:#f1c9,stroke:#333,stroke-width:2px;
    class E,F,D devices;
    class G,H,I,J outputs;
```

Note: 
My updated diagram with some order arrangement:

```mermaid
graph TD
    A[AVCaptureSession] -->|Manages| B(AVCaptureDeviceInput)
    A -->|Manages| C(AVCaptureOutput)
    B -->|Represents| D{AVCaptureDevice}
    D -.->|Camera| E[Front Camera]
    D -.->|Microphone| F[Built-in Microphone]
    C -->|Data| G{AVCaptureVideoDataOutput}
    C -->|Data| H{AVCaptureAudioDataOutput}
    C -->|Metadata| I{AVCaptureMetadataOutput}
    C -->|Still Image| J[AVCapturePhotoOutput]
    G -->|Video Frames| K[Process Video Frames]
    H -->|Audio Samples| L[Process Audio Samples]
    I -->|Metadata Objects| M[Process Metadata]
    J -->|Photo| N[Capture Photo]
    
classDef devices fill:#f19f,stroke:#333,stroke-width:2px;
class E,F,D devices;

classDef outputs fill:#415f,stroke:#333,stroke-width:2px;
class G,H,I,J outputs;

```


---


**Explanation:**

*   **AVCaptureSession**: The central coordinator, like `MTLCommandQueue`.
*   **AVCaptureDeviceInput**: Represents an input source, connected to an `AVCaptureDevice` (e.g., camera, microphone). This is similar to setting up your render pipeline configurations that are tied to a specific `MTLDevice` in Metal.
*   **AVCaptureOutput**: A base class for capture outputs, directing data to different destinations.
*   **AVCaptureVideoDataOutput**: Provides access to video frames.
*   **AVCaptureAudioDataOutput**: Provides access to audio samples.
*   **AVCaptureMetadataOutput**: Provides access to metadata (e.g., QR codes, faces).
*   **AVCapturePhotoOutput**: Captures still photos.

## 4. Detailed AVPlayerItem and AVPlayer Playback Pipeline
This diagram showcases use of player layers and item tracks in the playback pipeline sequence.

```mermaid
graph TD
    A[AVPlayerItem] -->|Contains| B(AVPlayerItemTrack: Video)
    A -->|Contains| C(AVPlayerItemTrack: Audio)
    A -->|Contains| D(AVPlayerItemTrack: Subtitles)
    A -->|Status| E{Ready To Play}
    A -->|Loaded Time Ranges| F[Buffer Information]
    A -->|Presentation Size| G[Video Dimensions]
    B -->|Asset Track| H[AVAssetTrack: Video]
    C -->|Asset Track| I[AVAssetTrack: Audio]
    D -->|Asset Track| J[AVAssetTrack: Subtitles]
    A -->|Video Composition| K[AVVideoComposition]
    K -->|Custom Video Compositor| L[Core Image Integration]
    A -->|Audio Mix| M[AVAudioMix]
    M -->|Input Parameters| N[Volume, Panning]

    O[AVPlayer] -->|Plays| A
    O -->|Controls| P[Playback Controls]
    O -->|Outputs to| Q(AVPlayerLayer)
    O -->|Outputs to| R(AVRoutePickerView)
    Q -->|Displays| S[Video Output on Screen]
    R-->|Outputs to| T[External Screens & Devices]
    O -->|Observes| U[KVO: Status, Rate, Errors]

classDef output fill:#c52,stroke:#333,stroke-width:2px
class Q,R,T,S output

click O "https://developer.apple.com/documentation/avfoundation/avplayer"
click A "https://developer.apple.com/documentation/avfoundation/avplayeritem"

```

**Explanation:**

*   **AVPlayerItem**: Represents the media to be played, containing multiple tracks (video, audio, subtitles). It's analogous to a fully composed `MTLCommandBuffer` ready for execution.
*   **AVPlayerItemTrack**: Represents a track within the `AVPlayerItem`, linked to the corresponding `AVAssetTrack`.
*   **AVPlayer**: Controls playback of the `AVPlayerItem`, similar to how `MTLCommandQueue` manages the execution of a command buffer.
*   **AVPlayerLayer**: A `CALayer` subclass that displays the video output, comparable to a `CAMetalDrawable` in Metal rendering. The difference here is that it is specifically made to display AV playback content.
*   **AVRoutePickerView**: Allows the user to choose the output route for audio and video (e.g., AirPlay, headphones).
*   **Key-Value Observing (KVO):** Used to observe changes in `AVPlayer`'s status, rate, and errors, which is vital for managing playback state and responding to events.

---