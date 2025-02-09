---
created: 2024-12-07 04:58:55
url:
author(s): Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---

# CUDA and OpenCL - GPU Compute Pipelines

Here are the Mermaid diagrams for CUDA and OpenCL, structured for clarity and comparison.


---


# CUDA Diagrams

## 1. High-Level Overview of CUDA Compute Pipeline

```mermaid
flowchart TD
    A["Host (CPU)"] -->|1. Allocate Memory| B["Device (GPU)"]
    A -->|2. Copy Data| B
    A -->|3. Load Kernel| C[CUDA Kernel]
    C -->|4. Launch Kernel| D[Grid of Blocks]
    D -->|5. Execute in Parallel| E[Threads within Blocks]
    E -->|6. Kernel Completion| F[Results in Device Memory]
    B -->|7. Copy Data Back| A
    A -->|8. Free Memory| B

```
Note: 
My updated diagram version: 

```mermaid
flowchart TD
    A["Host (CPU)"] -->|Step 1 - Allocate Memory| B["Device (GPU)"]
    A -->|Step 2 - Copy Data| B
    A -->|Step 3 - Load Kernel| C[CUDA Kernel]
    C -->|Step 4 - Launch Kernel| D[Grid of Blocks]
    D -->|Step 5 - Execute in Parallel| E[Threads within Blocks]
    E -->|Step 6 - Kernel Completion| F[Results in Device Memory]
    B -->|Step 7 - Copy Data Back| A
    A -->|Step 8 - Free Memory| B
    
```

---

**Explanation:**

1. **Host (CPU):** Initiates and controls the process.
2. **Device (GPU):** Performs parallel computations.
3. **Allocate Memory:** Allocate memory on the GPU.
4. **Copy Data:** Transfer data from host to device.
5. **Load Kernel:** Load the compute kernel code.
6. **Launch Kernel:** Execute the kernel on a grid of thread blocks.
7. **Execute in Parallel:** Threads within blocks execute concurrently.
8. **Kernel Completion:** Results are stored in device memory.
9. **Copy Data Back:** Transfer results back to the host.
10. **Free Memory:** Release allocated memory.

## 2. Detailed CUDA Kernel Execution and Memory Hierarchy

Note: This diagram still have missing information for subgraph `Memory_Hierarchy` . 

```mermaid
graph TD
    subgraph Host
        A[CPU] -->|cudaMalloc| B(GPU Memory Allocation)
        A -->|"cudaMemcpy (Host to Device)"| C[Global Memory]
        A -->|Load Kernel| D[CUDA Kernel Code]
    end
    
    subgraph Device
        D -->|Kernel Launch| E(Grid)
        E -->|1..N| F(Block)
        F -->|1..N| G(Thread)
        G -->|Read/Write| H[Shared Memory]
        G -->|Read/Write| C
        G -->|Read/Write| I[Registers]
        G -->|Read/Write| J[Local Memory]

    end
        
    subgraph Memory_Hierarchy
        C -- Largest, Slowest --> H
        H -- Smaller, Faster --> I
        H -- Larger, Slower --> J
       
    end

    A -->|"cudaMemcpy (Device to Host)"| K[Results]

    classDef gpu fill:#f9f9,stroke:#333,stroke-width:2px
    classDef cpu fill:#f2f2,stroke:#333,stroke-width:2px
    classDef mem fill:#f12,stroke:#333,stroke-width:2px
    class E,F,G gpu
    class A,K cpu
    class C,H,I,J mem

```

**Explanation:**

*   **Host:**
    *   Allocates GPU memory using `cudaMalloc`.
    *   Copies data to the GPU using `cudaMemcpy`.
    *   Loads the CUDA kernel.
*   **Device:**
    *   The kernel is launched on a grid of blocks.
    *   Each block contains multiple threads.
    *   Threads access different levels of memory:
        *   **Global Memory:** Large, slow, accessible by all threads and the host.
        *   **Shared Memory:** Smaller, faster, shared among threads within a block.
        *   **Registers:** Fastest, private to each thread.
        *   **Local Memory:** Used when registers are insufficient, slower than registers.
*   **Memory Hierarchy:** Illustrates the size and speed relationship between memory types.
*   **Results:** Data is copied back to the host using `cudaMemcpy`.

---

# OpenCL Diagrams

## 1. High-Level Overview of OpenCL Compute Pipeline

```mermaid
flowchart TD
    A["Host (CPU)"] -->|Step 1 <br> Query Platform & Devices| B[OpenCL Platform]
    B -->|Step 2 <br> Select Device| C["Device (CPU/GPU/Accelerator)"]
    A -->|Step 3 <br> Create Context| D[Context]
    D -->|Step 4 <br> Create Command Queue| E[Command Queue]
    A -->|Step 5 <br> Create/Load Program| F[Program Object]
    F -->|Step 6 <br> Build Program| G[Kernel Executable]
    A -->|Step 7 <br> Create Kernel| H[Kernel Object]
    A -->|Step 8 <br> Allocate Memory| C
    A -->|Step 9 <br> Copy Data to Device| C
    E -->|Step 10 <br> Enqueue Kernel| H
    E -->|Step 11 <br> Execute Kernel| I[Work-items in Work-groups]
    I -->|Step 12 <br> Kernel Completion| J[Results in Device Memory]
    C -->|Step 13 <br> Copy Data Back| A
    A -->|Step 14 <br> Release Resources| C
    A -->|Step 15 <br> Free Memory| C

```


**Explanation:**

1. **Host (CPU):** Manages the OpenCL environment.
2. **Query Platform & Devices:** Discover available OpenCL platforms and devices.
3. **Select Device:** Choose a device (CPU, GPU, or accelerator).
4. **Create Context:** Create a context for managing objects and operations.
5. **Create Command Queue:** Create a queue to submit commands to the device.
6. **Create/Load Program:** Create or load the OpenCL program (source code).
7. **Build Program:** Compile the program into a kernel executable.
8. **Create Kernel:** Create a kernel object from the program.
9. **Allocate Memory:** Allocate memory on the device.
10. **Copy Data to Device:** Transfer data to device memory.
11. **Enqueue Kernel:** Add the kernel to the command queue for execution.
12. **Execute Kernel:** Work-items within work-groups execute in parallel.
13. **Kernel Completion:** Results are stored in device memory.
14. **Copy Data Back:** Transfer results back to the host.
15. **Release Resources:** Release OpenCL objects (context, queue, program, kernel).
16. **Free Memory**: Release allocated memory.


**2. Detailed OpenCL Kernel Execution and Memory Regions**

```mermaid
graph TD
    subgraph Host
        A[CPU] -->|clCreateContext| B(Context)
        A -->|clCreateCommandQueue| C[Command Queue]
        A -->|clCreateProgramWithSource/clBuildProgram| D[Program/Kernel]
        A -->|clCreateBuffer| E(Device Memory Allocation)
        A -->|clEnqueueWriteBuffer| F[Global/Constant Memory]
    end
    
    subgraph Device
        D -->|clCreateKernel| G[Kernel Object]
        C -->|clEnqueueNDRangeKernel| G
        G -->|Execute| H(Work-group)
        H -->|1..N| I(Work-item)
        I -->|Read/Write| F
        I -->|Read/Write| J[Local Memory]
        I -->|Read/Write| K[Private Memory]
    end
        
    subgraph Memory_Regions
        F -- Largest, Slowest --> J
        J -- Smaller, Faster --> K
    end

    A -->|clEnqueueReadBuffer| L[Results]
    
    classDef device fill:#f916,stroke:#333,stroke-width:2px
    classDef host fill:#c2f,stroke:#333,stroke-width:2px
    classDef mem fill:#ff95,stroke:#333,stroke-width:2px
    class H,I device
    class A,L host
    class F,J,K mem

```

**Explanation:**

*   **Host:**
    *   Creates a context (`clCreateContext`).
    *   Creates a command queue (`clCreateCommandQueue`).
    *   Creates and builds the program/kernel (`clCreateProgramWithSource`, `clBuildProgram`).
    *   Allocates device memory (`clCreateBuffer`).
    *   Writes data to device memory (`clEnqueueWriteBuffer`).
*   **Device:**
    *   Creates a kernel object (`clCreateKernel`).
    *   Enqueues the kernel for execution (`clEnqueueNDRangeKernel`).
    *   The kernel executes in work-groups, each containing multiple work-items.
    *   Work-items access different memory regions:
        *   **Global/Constant Memory:** Large, slow, accessible by all work-items and the host.
        *   **Local Memory:** Smaller, faster, shared among work-items in a work-group.
        *   **Private Memory:** Fastest, private to each work-item.
*   **Memory Regions:** Illustrates the size and speed relationship between memory types.
*   **Results:** Data is read back to the host using `clEnqueueReadBuffer`.

**Key Differences and Unique Details Highlighted:**

*   **CUDA vs. OpenCL Terminology:** The diagrams highlight the different terms used (e.g., Grid/Block/Thread vs. Work-group/Work-item).
*   **OpenCL's Platform Model:** OpenCL has a more explicit platform and device model, allowing it to target a wider range of devices.
*   **OpenCL's Program Build Process:** OpenCL emphasizes the separate steps of creating, building, and loading programs.
*   **Memory Spaces:**  Both models have similar memory hierarchies, but OpenCL makes a clearer distinction between global and constant memory.
*   **Synchronization:** While not explicitly shown in these basic diagrams, both CUDA and OpenCL provide synchronization mechanisms (e.g., `__syncthreads` in CUDA, `barrier` in OpenCL) to coordinate threads/work-items within a block/work-group. These mechanisms are crucial for many parallel algorithms.

These diagrams provide a clear, concise, and informative comparison of CUDA and OpenCL compute pipelines, drawing parallels to the Metal rendering pipeline concepts we discussed earlier.

---