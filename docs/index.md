# Welcome to Documentation Page for IO-Tracer!
Technical documentation for Linux and Windows kernel-level I/O tracing system using [eBPF](https://ebpf.io/what-is-ebpf/) and [ETW](https://learn.microsoft.com/en-us/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-) technology.

Source code:

- [https://github.com/cacheMon/io-tracer-win](https://github.com/cacheMon/io-tracer-win)
- [https://github.com/cacheMon/io-tracer](https://github.com/cacheMon/io-tracer)

## What is IO-Tracer?
IO-Tracer is a research tool that collects information about how hardware is utilized. Researchers use this tool to understand real-world computer workloads, essentially studying patterns of how different processes and users interact with files and storage devices.

## Background

Most operations occurring within our computers remain invisible to users. This design choice makes sense because the average user doesn't need detailed information about every process running under the hood. However, researchers have a different perspective. They're deeply interested in understanding and visualizing the intricate pathways of computational operations that power our digital experiences.

To understand these computational pathways, we need a specialized program capable of monitoring them. This is where IO-Tracer comes in. IO-Tracer operates as an intermediary layer between your daily applications and your computer's hardware, residing within the operating system without disrupting existing operations. This tool captures all the necessary hardware information for research purposes while maintaining strict privacy standards. It **cannot access** the content within your files and only collects metadata such as file names and system calls.

## What do we collect?

IO-Tracer gathers system metrics strictly related to hardware performance. We analyze the mechanism of data requests without ever inspecting the data contents. By monitoring the interaction between computer layers, IO-Tracer captures the system-specific dialogue between components while ensuring user data remains private.

## How do we use the collected information?

The information collected by IO-Tracer serves as valuable input for academic research. Individual datasets are aggregated with data from other participants to reveal meaningful patterns and generate statistical insights about computational behavior. Access to this research information is strictly limited to authorized researchers. 

Throughout the collection process, all information remains **securely** stored on the user's personal computer, ensuring complete user control over their data. The research team can only access the hardware information through **direct user consent**. We must explicitly request permission from each participant before any information is transferred from their system to our research infrastructure.
