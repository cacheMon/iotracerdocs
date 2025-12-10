# Technical Details - Windows

## Event Tracing for Windows (ETW) Libraries

- `Microsoft.Diagnostics.Tracing` Primary library for ETW interaction
- `TraceEventSession` Manages kernel-level tracing sessions
- `KernelTraceEventParser` Parses kernel events in real-time

## Implementation Details
### Session Management
The system creates a unique ETW session per process ID to avoid conflicts and ensure isolated tracing. It requires elevated privileges for kernel provider access, as kernel-level events can only be captured by administrators.

### Event Processing
Events are processed in real-time as they occur via the `source.Process()` methods. The architecture uses a handler-based approach with dedicated handlers for filesystem and disk operations. Kernel integration is achieved through direct subscription to specific kernel events such as FileIORead and DiskIOWrite.
