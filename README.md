# Working Group Meeting Notes
## Working Group 2:00 - 3:30 p Tuesday, August 13, 2024
### AMD GPU Working Session

1. Introduction and Setup
        Primary Participants:
            Ben Welton, Timour Paltashev, John Mellor-Crummey, Kevin Huck
        Goal of the Session:
            Walkthrough of a sample included in rocprofiler 6.2.
            Primary focus on demonstrating how to collect hardware counters using buffered tracing methods.

3. In-Depth Discussion on Counter Collection Setup

    Rocprofiler Versions Comparison:
        Version 1/2 vs. Version 6.2:
            Earlier versions offered a more rigid structure, limiting flexibility in counter collection.
            The latest version (6.2) is highlighted for its modular approach, allowing dynamic counter selection and enhanced compatibility with newer GPU architectures.
        Simplified Counter Collection Process:
            Version 6.2's design simplifies the process of setting up and collecting hardware counters.
            Improved API allows for more precise data retrieval, crucial for optimizing application performance on AMD GPUs.
    Implementation in C++ Profiling Tools:
        Detailed discussion on integrating ROCm profiling capabilities into C++ tools.
        Focus on code modifications required to leverage the new features in version 6.2.
    Technical Hurdles:
        Specific mention of a participant facing issues with data reading.
        Timour’s guidance on how to modify the code to overcome these challenges.
        Querying counters based on the availability of GPU agents, ensuring accurate profiling in multi-GPU environments.

4. Detailed Examination of Technical Challenges and Solutions

    Handling Counter Collection Issues:
        Per-Architecture Counter Handling:
            Discussion on how the latest rocprofiler versions manage counters specific to different GPU architectures.
            Emphasis on the ability to map counter data directly to hardware features, improving data accuracy.
        Introduction of Unique Counter IDs:
            Explanation of how unique counter IDs simplify referencing across various GPU models.
            The role of these IDs in maintaining consistency in performance data collection.
    Software and Code Execution Issues:
        Detailed recount of the delays caused by software update issues, particularly with VS Code.
        Strategies discussed for overcoming these obstacles, ensuring the session's continuity.

5. Rocprofiler SDK Overview and Changes

    Philosophical Shift in the SDK:
        Counter Dimensionality:
            Introduction of dimensions in the latest SDK version to map counter data more accurately to hardware components.
            Acknowledgment of the shift from summarizing data across different compute units (CUs) to more granular data representation.
        Benefits of the New Approach:
            Discussion on the enhanced ability to correlate counter data with specific hardware features, leading to better performance tuning.
            The significance of these changes in providing developers with deeper insights into GPU performance.

6. Implementation and Tool Initialization Details

    ROCprofiler Tool Initialization:
        Tool Initialization Process:
            Step-by-step overview of initializing tools with the rocprofiler SDK.
            Key focus on the tool_init function, which serves as the entry point for setting up profiling tools.
        Context and Buffer Creation:
            Detailed discussion on how to create contexts and buffers for collecting profiling data.
            Importance of specifying callback information during initialization to ensure accurate data collection.
    Environment Variables and Their Role:
        ROCR_VISIBLE_DEVICES:
            In-depth explanation of the ROCR_VISIBLE_DEVICES environment variable and its impact on GPU visibility.
            Discussion on how this variable influences which GPUs are profiled, especially in multi-GPU systems.
        Challenges with GPU Selection:
            Exploration of potential issues arising from improper use of environment variables, such as profiling on inactive GPUs.
            Proposed strategies to avoid resource conflicts and ensure profiling is focused on the correct GPUs.

7. Agent Configuration and Visibility Management

    Managing GPU Agents:
        Detailed exploration of configuring and managing multiple GPU agents within the profiling environment.
        Importance of ensuring that only the relevant GPUs are visible and active during profiling sessions.
    Filtering and Visibility Solutions:
        Proposed solution of adding a visibility field in the device structure to indicate which GPUs are accessible to rocprofiler.
        Discussion on potential callbacks in the SDK to manage device visibility after initialization.
        The team explored options to address visibility management issues to prevent conflicts in multi-GPU setups.

8. Handling Multi-tool and Device Management

    Managing Multiple Tools:
        In-depth discussion on the complexities of handling multiple tools within the rocprofiler environment.
        Importance of proper context setup to avoid data corruption when using multiple profiling tools simultaneously.
    Counter Collection and PC Sampling:
        Exploration of the impact of clock gating on counter collection and PC sampling.
        Detailed analysis of how these operations might interfere with each other and potential solutions to mitigate this.

9. Power Management and Clock Gating

    Challenges with Clock Gating:
        Detailed discussion on the impact of clock gating on counter accuracy and profiling stability.
        Mention of ongoing efforts to manage and stabilize counter data by controlling clock gating features.
        Consideration of how to extract and handle clock gating data to ensure reliable performance metrics.

10. Discussion on PC Sampling and Counter Collection Interference

    Key Technical Questions:
        Detailed discussion on whether PC sampling and counter collection can be performed simultaneously without causing data distortion.
        Exploration of the potential for timing perturbations during simultaneous data collection operations.
    Consultation with Experts:
        Plan to consult with hardware experts (e.g., Vladimir) for deeper insights into the hardware's handling of these operations.
        Emphasis on gathering more technical details to ensure accurate and reliable profiling results.

11. Conclusion and Next Steps

    Final Remarks:
        Summary of key points discussed and the importance of accurate device visibility management in multi-GPU environments.
        Mention of the L3 slides and notes available for further reference.
        Plans to verify details about counter collection and PC sampling interference with experts.
    Follow-Up Actions:
        Continued discussions with AMD to address the tooling and environment variable issues identified during the session.
        Emphasis on the need for ongoing collaboration to refine and improve the ROCm Profiler SDK for developer use.
