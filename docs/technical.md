# Technical Implementation

## Overview

IO-Tracer captures kernel-level I/O events on both Linux and Windows. While both platforms trace I/O activities, they use different technologies and approaches optimized for each operating system.

---

## Linux Implementation

We are implementing [eBPF](https://ebpf.io/) through [BPF Compiler Collection](https://github.com/iovisor/bcc/tree/master). Kernel probes are attached to several system calls related to I/O activities in the [Linux Storage Stack](https://wxdublin.gitbooks.io/deep-into-linux-and-beyond/content/io.html).

### System Calls Traced

| Layer | Syscall Traced |
|-------|------------------|
| VFS Layer | `vfs_read`, `vfs_write`, `vfs_open`, `vfs_fsync`, `vfs_fsync_range`, `__fput` |
| Block Layer | `block_rq_issue`, `block_rq_complete` |
| Page Cache | `filemap_add_folio`, `folio_mark_accessed` |

---

## Windows Implementation

### Event Tracing for Windows (ETW) Libraries

- **`Microsoft.Diagnostics.Tracing`** — Primary library for ETW interaction
- **`TraceEventSession`** — Manages kernel-level tracing sessions
- **`KernelTraceEventParser`** — Parses kernel events in real-time

### Session Management

The system creates a unique ETW session per process ID to avoid conflicts and ensure isolated tracing. Elevated privileges are required for kernel provider access, as kernel-level events can only be captured by administrators.

### Event Processing

Events are processed in real-time as they occur via the `source.Process()` methods. The architecture uses a handler-based approach with dedicated handlers for filesystem and disk operations. Kernel integration is achieved through direct subscription to specific kernel events such as FileIORead and DiskIOWrite.
