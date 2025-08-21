# Welcome to Documentation Page for IO-Tracer!
Technical documentation for Linux kernel-level I/O tracing system using [eBPF](https://ebpf.io/what-is-ebpf/) technology.

## What is IO-Tracer?
IO-Tracer is a research tool that collects data about how computers use their storage systems. Researchers use this tool to understand real-world computer workloads, essentially studying patterns of how different processes and users interact with files and storage devices.

## Background

Most operations occurring within our computers remain invisible to users. This design choice makes sense because the average user doesn't need detailed information about every process running under the hood. However, researchers have a different perspective. They're deeply interested in understanding and visualizing the intricate pathways of computational operations that power our digital experiences.

To understand these computational pathways, we need a specialized program capable of monitoring them. This is where IO-Tracer comes in. IO-Tracer operates as an intermediary layer between your daily applications and your computer's hardware, residing within the operating system without disrupting existing operations. This tool captures all the necessary data for research purposes while maintaining strict privacy standards. It cannot access the content within your files and only collects metadata such as file names and system calls.

## What do we collect?

IO-Tracer collects ***five key types of data*** to provide comprehensive insights into computational operations. 

First, it captures the **precise timestamp** of each operation to establish when activities occur. Second, it records the **type of operation** being performed, whether it's opening, reading, writing, or closing files. Third, it identifies which specific process (**process name**) is performing each operation. Finally, it logs the **file location** information, including both the file path and technical identifiers that specify where operations are taking place. Finally, it measures the **size of data** being requested during each operation.

## How do we use the collected data?

The data collected by IO-Tracer serves as valuable input for academic research. Individual datasets are aggregated with data from other participants to reveal meaningful patterns and generate statistical insights about computational behavior. Access to this research data is strictly limited to authorized researchers. 

Throughout the data collection process, all information remains securely stored on the user's personal computer, ensuring complete user control over their data. The research team can only access this data through direct user consent. we must explicitly request permission from each participant before any data is transferred from their system to our research infrastructure.
