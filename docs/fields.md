# Fields Collected

## Linux Traces

### Filesystem

- Request:

| Field      | Data Type   | Description                                                                 |
|------------|-------------|-------------|
| `timestamp` | `datetime` | The exact time when the request occurred |
| `operation` | `string` | Operation type (read, write, open, close, fsync, etc.) |
| `pid` | `int` | Process ID that performed the request |
| `tid` | `int` | Thread ID within the process |
| `command` | `string` | Name of the process performing the request (truncated to 16 chars) |
| `filename` | `string` | The full path or name of the file being accessed |
| `size` | `int` | Data transfer amount in bytes |
| `offset` | `int` | Offset within the file where the operation occurred |
| `bytes_completed` | `int` | Number of bytes actually transferred |
| `inode` | `int` | The inode number associated with the file |
| `device` | `string` | Device where the file is located |
| `flags` | `string` | String representation of file operation flags |
| `duration_ns` | `int` | Duration of the operation in nanoseconds |
| `return_value` | `int` | Return value of the system call |
| `errno` | `int` | Error number if the operation failed |
| `mmap_prot` | `string` | Memory protection flags for mmap operations |
| `mmap_flags` | `string` | Flags for mmap operations |
| `address` | `string` | Memory address involved in the operation |
| `cmdline` | `string` | Full command line of the process |
| `ppid` | `int` | Parent Process ID |
| `container_id` | `string` | Container ID if running in a container |
| `fs_type` | `string` | Filesystem type (ext4, btrfs, etc.) |

---

### Block

- Request:

| Field         | Data Type         | Description                                                                 |
|--------------|------------------|-------------|
| `timestamp` | `datetime` | The time when the block I/O operation occurred |
| `operation` | `string` | Operation type (read, write, flush, discard, etc.) |
| `pid` | `int` | Process ID that issued the I/O request |
| `tid` | `int` | Thread ID within the process that performed the I/O operation |
| `command` | `string` | Name of the process performing the block I/O |
| `sector` | `int` | Logical block address on disk |
| `size` | `int` | Size of the I/O request in bytes |
| `latency_ms` | `float` | Time it takes for a block request to finish in milliseconds |
| `device` | `string` | Device where the I/O operation occurred |
| `flags` | `string` | String representation of I/O flags (sync, meta, ahead, etc.) |
| `cpu_id` | `int` | CPU core ID where the I/O request was executed |
| `ppid` | `int` | Parent Process ID |
| `queue_latency_ms` | `float` | Time spent waiting in the I/O queue in milliseconds |
| `command_flags` | `string` | Command-specific flags (empty on kernel ≥ 5.17) |
| `operation_code` | `int` | Operation code (empty on kernel ≥ 5.17) |
| `request_id` | `int` | Unique request identifier |

---

### Cache

- Request:

| Field | Data Type | Description |
|-------|-----------|-------------|
| `timestamp` | `datetime` | The time when the cache operation occurred |
| `pid` | `int` | Process identifier |
| `command` | `string` | Process command name |
| `event_type` | `string` | Type of cache event (HIT, MISS, DIRTY, WRITEBACK, EVICTION, etc.) |
| `inode` | `int` | Inode number of the file |
| `page_index` | `int` | Index of the page in the file (multiply by 4096 for byte offset) |
| `size_pages` | `int` | Number of pages involved in the operation |
| `cpu_id` | `int` | CPU core ID where the operation occurred |
| `device_id` | `string` | Device identifier |
| `count` | `int` | Count of affected pages or events |

---

### Network

| Field | Data Type | Description |
| --- | --- | --- |
| `timestamp` | `datetime` | Time when the request was taken |
| `event_type` | `string` | Type of network event (connect, accept, send, recv, close, etc.) |
| `pid` | `int` | Process ID |
| `tid` | `int` | Thread ID |
| `command` | `string` | Name of process that triggered the network request |
| `domain` | `string` | Address family (AF_INET, AF_INET6, AF_UNIX, etc.) |
| `sock_type` | `string` | Socket type (SOCK_STREAM, SOCK_DGRAM, etc.) |
| `ipver` | `string` | IP version (IPv4, IPv6) |
| `local_addr` | `string` | Local address of the connection |
| `remote_addr` | `string` | Remote address of the connection |
| `sport` | `int` | Source port of the requests |
| `dport` | `int` | Destination port of the requests |
| `fd` | `int` | File descriptor number |
| `backlog` | `int` | Listen backlog for server sockets |
| `shutdown_how` | `string` | How the socket was shut down (read, write, both) |
| `latency_ns` | `int` | Operation latency in nanoseconds |
| `return_value` | `int` | Return value of the socket operation |
| `size` | `int` | Size of the request/response in bytes |
| `proto` | `string` | Protocol type (TCP, UDP, etc.) |
| `drop_reason` | `string` | Reason for packet drop |
| `tcp_state` | `string` | TCP connection state at time of drop |

---

### Process

- State:

| Column Name        | Data Type           | Description                                                                 |
|---------------------|--------------------|------------------------------------------------------------------------------|
| `timestamp` | `datetime` | Time when the process state snapshot was taken |
| `pid` | `int` | Process ID |
| `name` | `string` | Process name (truncated to 16 chars) |
| `cmdline` | `string` | Full command line used to start the process |
| `vms_kb` | `int` | Virtual memory size of the process in kilobytes |
| `rss_kb` | `int` | Resident Set Size (RSS), actual physical memory used in kilobytes |
| `creation_time` | `datetime` | Time when the process was created |
| `cpu_5s` | `float` | CPU utilization percentage for the process, calculated in 5 second interval |
| `cpu_2m` | `float` | CPU utilization percentage for the process, calculated in 2 minute interval |
| `cpu_1h` | `float` | CPU utilization percentage for the process, calculated in 1 hour interval |
| `status` | `string` | Current process state |

---

## Windows Traces

### Disk

- Request:

| Field         | Data Type   | Description                                                         |
|--------------|-------------|-------------|
| `Ts` | `datetime` | Timestamp (local wall-clock) |
| `Pid` | `int` | Process ID |
| `ThreadId` | `int` | Thread ID |
| `Comm` | `string` | Command/Process name |
| `Sector` | `int` | Logical sector number on the disk |
| `Operation` | `string` | Operation type (read, write, etc.) |
| `TraceSize` | `int` | Size of the I/O request in bytes |
| `Latency` | `float` | Duration of the operation in milliseconds |
| `DiskNumber` | `int` | Disk number |
| `Irp` | `string` | I/O Request Packet pointer (hex format: 0x...) |
| `IrpFlags` | `string` | IRP Flags |

---

### Filesystem

- Request:

| Field         | Data Type   | Description                                                         |
|--------------|-------------|-------------|
| `timestamp` | `datetime` | Event time (local wall-clock) |
| `operation` | `string` | Canonical lowercase operation name (create, read, write, close, fsync, getattr, setattr, readdir, mmap, fsctl, etc.) |
| `pid` | `int` | Process ID initiating the operation (-1 when unattributed) |
| `tid` | `int` | Thread ID of the operation |
| `command` | `string` | Command/process name (empty when unavailable) |
| `filename` | `string` | Full path of the file involved (hashed if anonymous mode enabled) |
| `size` | `int` | Requested transfer size in bytes |
| `offset` | `int` | Byte offset of the operation (read, write only) |
| `bytes_completed` | `int` | Bytes actually transferred (mirrors size for read/write) |
| `flags` | `string` | IRP/I/O flags (read, write only) |
| `create_options` | `string` | CreateOptions (open only) |
| `share_access` | `string` | File sharing mode flags (open only) |
| `create_disposition` | `string` | Create/open disposition (open only) |
| `view_size` | `int` | Size of the mapped view (mmap family only) |
| `file_info_class` | `string` | FILE_INFORMATION_CLASS for metadata queries/sets (getattr, setattr only) |
| `fsctl_code` | `string` | FSCTL control code (fsctl only) |
| `irp` | `string` | I/O Request Packet pointer (hex 0x...) |
| `file_key` | `string` | Kernel file-object identity (hex 0x...; Windows analog of inode) |
| `file_attributes` | `string` | File attribute flags (open only) |
| `command_line` | `string` | Full command line of the process |
| `nt_status` | `string` | Final NTSTATUS of the completed IRP (hex 0x....; op_end rows only) |

---

### Filesystem Snapshot

- State:

| Field         | Data Type   | Description                                                         |
|--------------|-------------|-------------|
| `timestamp` | `datetime` | Snapshot timestamp |
| `path` | `string` | Full path to the file |
| `size` | `int` | File size in bytes |
| `CreationDate` | `datetime` | File creation timestamp |
| `modificationDate` | `datetime` | File last modification timestamp |
| `LastAccessTime` | `datetime` | File last access timestamp |
| `Attributes` | `string` | File attributes (e.g., Archive, Directory, Hidden) |
| `Extension` | `string` | File extension including the dot (e.g., .txt) |
| `IsReadOnly` | `boolean` | Whether the file is read-only (True or False) |

---

### Memory

- Request:

| Field         | Data Type   | Description                                                         |
|--------------|-------------|-------------|
| `Ts` | `datetime` | Timestamp (local wall-clock) |
| `Pid` | `int` | Process ID |
| `ThreadId` | `int` | Thread ID of the thread that triggered the event |
| `Comm` | `string` | Command/Process name (quoted if contains spaces) |
| `Type` | `string` | Event Type (memory event classification) |
| `VirtualAddress` | `string` | Virtual Address (hexadecimal format, e.g., 0x7FF...; 0 if not applicable) |
| `ByteCount` | `int` | Size or Auxiliary Data (number of bytes involved or specific value) |

---

### Network

- Aggregated Connection Statistics (1-minute window):

| Field         | Data Type   | Description                                                         |
|--------------|-------------|-------------|
| `Ts` | `datetime` | Flush time (local wall-clock) marking the end of the 1-minute window |
| `Pid` | `int` | Process ID owning the connection |
| `Comm` | `string` | Command/Process name |
| `Proto` | `int` | IP protocol number (6 = TCP, 17 = UDP) |
| `Saddr` | `string` | Local (this host) IP address |
| `Daddr` | `string` | Remote peer IP address |
| `Sport` | `int` | Local port |
| `Dport` | `int` | Remote port |
| `ConnId` | `int` | Connection ID (kernel connection identifier when available, else 0) |
| `BytesSent` | `int` | Bytes sent on this connection during the window |
| `BytesReceived` | `int` | Bytes received on this connection during the window |

---

### Process Snapshot

- State (captured every 5 minutes):

| Field         | Data Type   | Description                                                         |
|--------------|-------------|-------------|
| `Ts` | `datetime` | Timestamp (local wall-clock) of the snapshot |
| `ProcessId` | `int` | Process ID |
| `Name` | `string` | Process name |
| `CommandLine` | `string` | Process command line arguments |
| `VirtualSize` | `int` | Virtual memory size in bytes |
| `WorkingSetSize` | `int` | Working set (physical memory) size in bytes |
| `CreationDate` | `datetime` | Process creation time |
| `CpuUsage_5s` | `float` | CPU usage over the last 5 seconds (percentage) |
| `CpuUsage_2m` | `float` | CPU usage over the last 2 minutes (percentage) |
| `CpuUsage_1h` | `float` | CPU usage over the last 1 hour (percentage) |

---

### System Snapshots

System specifications are captured in separate JSON files at trace start:

| File | Description |
|------|-------------|
| `cpu_info.json` | CPU model, cores, frequency |
| `memory_info.json` | Total RAM, available memory, page file (swap) |
| `disk_info.json` | Storage devices, partitions, and GPUs |
| `network_info.json` | Network interfaces and addresses |
| `os_info.json` | Windows version, build, hostname, country |

#### cpu_info.json

| Field | Type | Description |
|-------|------|-------------|
| `brand` | `string` | CPU model name (from WMI Win32_Processor); null if unavailable |
| `cores_logical` | `integer` | Number of logical CPU cores (including hyperthreads) |
| `cores_physical` | `integer` | Number of physical CPU cores |
| `frequency_mhz` | `float` | Maximum CPU frequency in MHz; null if unavailable |
| `frequency_min_mhz` | `float` | Minimum CPU frequency in MHz; null (not available on Windows) |
| `frequency_max_mhz` | `float` | Maximum CPU frequency in MHz; null if unavailable |

#### memory_info.json

| Field | Type | Description |
|-------|------|-------------|
| `total_bytes` | `integer` | Total system RAM in bytes |
| `available_bytes` | `integer` | Currently available RAM in bytes |
| `used_bytes` | `integer` | Used RAM in bytes |
| `percent_used` | `float` | Memory usage percentage |
| `total_gb` | `float` | Total system RAM in GB (rounded to 2 decimals) |
| `available_gb` | `float` | Available RAM in GB (rounded to 2 decimals) |
| `swap_total_bytes` | `integer` | Total page file (swap) space in bytes |
| `swap_used_bytes` | `integer` | Used page file space in bytes |
| `swap_free_bytes` | `integer` | Free page file space in bytes |

#### disk_info.json

| Field | Type | Description |
|-------|------|-------------|
| `storage_devices` | `array[string]` | List of storage devices with name, model, size (from WMI Win32_DiskDrive) |
| `partitions` | `array[object]` | List of mounted partitions with usage details |
| `gpus` | `array[string]` | List of GPU names (from WMI Win32_VideoController); empty if none detected |

**Partition Object Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `device` | `string` | Device path (e.g., C:\, D:\) |
| `mountpoint` | `string` | Mount point path (same as device on Windows) |
| `fstype` | `string` | Filesystem type (e.g., NTFS, FAT32) |
| `opts` | `string` | Drive type (e.g., Fixed, Removable, CDRom) |
| `total_bytes` | `integer` | Total partition size in bytes |
| `used_bytes` | `integer` | Used space in bytes |
| `free_bytes` | `integer` | Free space in bytes |
| `percent_used` | `float` | Usage percentage |

#### network_info.json

| Field | Type | Description |
|-------|------|-------------|
| `interfaces` | `object` | Map of interface name to interface details |
| `hostname` | `string` | System hostname |

**Interface Object Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `addresses` | `array[object]` | List of addresses assigned to interface |
| `is_up` | `boolean` | Whether interface is operational |
| `speed_mbps` | `integer` | Link speed in Mbps; null if unavailable |
| `mtu` | `integer` | Maximum transmission unit |

**Address Object Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `family` | `string` | Address family (AF_INET, AF_INET6, AF_PACKET) |
| `address` | `string` | IP or MAC address |
| `netmask` | `string` | Network mask; null for some address types |
| `broadcast` | `string` | Broadcast address; null for Windows/some types |

#### os_info.json

| Field | Type | Description |
|-------|------|-------------|
| `system` | `string` | Operating system name (always Windows) |
| `release` | `string` | OS version (e.g., 10.0.22000) |
| `version` | `string` | Full OS caption and build (e.g., Microsoft Windows 10 Pro (Build 19045)) |
| `machine` | `string` | Machine hardware architecture (x64 or x86) |
| `hostname` | `string` | System hostname |
| `country` | `string` | Two-letter country code from IP geolocation; XX if detection fails |
