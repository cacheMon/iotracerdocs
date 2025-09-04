# Technical Details - Linux

## Data Collection Methodology
### Implementation
- Using eBPF-based kernel probes (kprobes)

### Kernel Probe Points
| Layer | Functions Traced |
|-------|------------------|
| VFS Layer | `vfs_read`, `vfs_write`, `vfs_open`, `vfs_fsync`, `vfs_fsync_range`, `__fput` |
| Block Layer | `blk_mq_start_request` |
| Page Cache | `filemap_add_folio` (miss), `folio_mark_accessed` (hit) |


### Output Directory Structures
```
result/IO_trace_analysis_YYYYMMDD_HHMMSS/
├─ raw_trace_YYYYMMDD_HHMMSS.tar.gz
├── vfs/log/vfs_trace_*.log
├── block/log/block_trace_*.log
└── cache/log/cache_trace_*.log
```

## Filesystem Trace Format

### Log Format
```
timestamp op_name pid comm filename inode size_val flags_str
```

### Field Specs
| Field | Data Type | Description | Privacy Level |
|-------|-----------|-------------|---------------|
| timestamp | uint64 | Nanoseconds since boot | Non-sensitive |
| op_name | string | Operation (READ/WRITE/OPEN/CLOSE/FSYNC) | Non-sensitive |
| pid | uint32 | Process identifier | Non-sensitive |
| comm | char[16] | Process command name | Non-sensitive (Does not contain personal info) |
| filename | char[256] | File name | Non-sensitive (Does not contain personal info) |
| inode | uint64 | File inode number | Non-sensitive |
| size_val | uint64 | I/O size in bytes | Non-sensitive |
| flags_str | string | Open flags (e.g., O_RDONLY) | Non-sensitive |

Example:
```
1234567890 READ 1234 firefox config.txt 98765 4096 O_RDONLY|O_DIRECT
```

## Block I/O Trace Format
### Log Format
```
timestamp pid tid comm sector nr_sectors operation cpu_id parent_info bio_size
```

### Field Spec

| Field | Data Type | Description | Privacy Level |
|-------|-----------|-------------|---------------|
| timestamp | uint64 | Nanoseconds since boot | Non-sensitive |
| pid | uint32 | Process identifier | Non-sensitive |
| tid | uint32 | Thread identifier | Non-sensitive |
| comm | char[16] | Process command name | Non-sensitive (Does not contain personal info) |
| sector | uint64 | Disk sector (LBA) | Non-sensitive |
| nr_sectors | uint32 | Number of sectors | Non-sensitive |
| operation | string | Operation type (REQ_OP_READ/WRITE) | Non-sensitive |
| cpu_id | uint32 | CPU core identifier | Non-sensitive |
| parent_info | string | Parent process information | Non-sensitive (Does not contain personal info) |
| bio_size | uint64 | Block I/O size in bytes | Non-sensitive |

Example:
```
1234567890 1234 5678 mysqld 2048576 256 REQ_OP_WRITE cpu:0 ppid:1(systemd) 131072
```

## Page Cache Trace Data Format
### Log Format
```
timestamp pid comm status
```

### Field Spec

| Field | Data Type | Description | Privacy Level |
|-------|-----------|-------------|---------------|
| timestamp | uint64 | Nanoseconds since boot | Non-sensitive |
| pid | uint32 | Process identifier | Non-sensitive |
| comm | char[16] | Process command name | Non-sensitive |
| status | string | HIT or MISS | Non-sensitive |

Example:
```
1234567890 1234 chrome HIT
```