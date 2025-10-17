# Fields Collected

## Filesystem

- Request:

| Field      | Data Type   | Description                                                                 | Platform  |
|--------------------|-------------|------------------------------------------------------------------------------|------------------------|
| `timestamp`        | `datetime` | The exact time when the request occurred.                       | Linux & Windows |
| `op_name`          | `string`    | Operation type of the reqeust         | Linux & Windows |
| `pid`              | `int`       | Process ID that performed the requst.                                     | Linux & Windows |
| `process_name`     | `string`    | Name of the process performing the request.                                | Linux & Windows |
| `filename`         | `string`    | The full path or name of the file being access.                            | Linux & Windows |
| `inode`            | `int` | The inode number associated with the file.    | Linux         |
| `size_val_bytes`   | `int` | Data transfer amount in bytes.           | Linux & Windows        |
| `flags_str`        | `string`    | String representation of file operation flags.       | Linux        |

- State:

| Field         | Data Type   | Description                                                                 | Platform  |
|----------------------|-------------|------------------------------------------------------------------------------|------------------------|
| `path`              | `string`    | Full path of the file being recorded. This will be anonimized if enabled.       | Linux & Windows         |
| `file_size`         | `int`  | Size of the file in bytes.                                              | Linux & Windows       |
| `created_time`      | `float` | Timestamp when the file was created.                                | Linux & Windows        |
| `modified_time`     | `float` | Timestamp when the file was last modified.                           | Linux & Windows        |


## Block

- Request:

| Field         | Data Type         | Description                                                                 | Platform  |
|-----------------------|------------------|------------------------------------------------------------------------------|------------------------|
| `timestamp`           | `datetime` | The time when the block I/O operation occurred.                            | Linux & Windows |
| `pid`                 | `int`            | Process ID that issued the I/O request.                                     | Linux & Windows |
| `tid`                 | `int`            | Thread ID within the process that performed the I/O operation.              | Linux        |
| `process_name`        | `string`         | Name of the process performing the block I/O.                               | Linux & Windows |
| `lba`                 | `int` | Identifies the location of the I/O on disk.         | Linux & Windows |
| `op_type`             | `string`         | Operation type.                                         | Linux & Windows       |
| `size`                | `int` | Size of the I/O request in bytes.                                           | Linux & Windows      |
| `nr_sectors`          | `int`            | Number of 512-byte sectors affected by the operation.                       | Linux         |
| `cpu_id`              | `int`            | CPU core ID where the I/O request was executed.                             | Linux        |
| `parent_process_id`   | `int`            | Process ID of the parent process that triggered the I/O.                    | Linux        |
| `parent_process`      | `string`         | Name of the parent process that triggered the I/O.                          | Linux         |


## Cache

- Request:

| Field | Data Type | Description | Platform |
|-------|-----------|-------------|---------------|
| `timestamp` | `int` | The time when the block I/O operation occurred. | Linux |
| `pid` | `int` | Process identifier | Linux |
| `comm` | `string` | Process command name | Linux |
| `status` | `string` | HIT or MISS | Linux |

## Process

- State:

| Column Name        | Data Type           | Description                                                                 | Platform Availability |
|---------------------|--------------------|------------------------------------------------------------------------------|------------------------|
| `timestamp`         | `datetime` | Time when the process state snapshot was taken.                            | Windows       |
| `pid`               | `int`              | Process ID.                                                                 | Linux & Windows |
| `name`              | `string`           | Process name.                                                               | Linux & Windows |
| `cmd`               | `string`           | Full command line used to start the process. | Linux & Windows      |
| `virtual_size`      | `int` | Virtual memory size of the process in bytes.                                | Windows only      |
| `working_set_size`  | `int`  | Amount of physical memory (RAM) currently used by the process, in bytes.    | Windows only       |
| `memory_info`       | `int` | Resident Set Size (RSS), actual physical memory used by the process.       | Linux only      |
| `creation_date`     | `datetime` | Time when the process was created.                                         | Linux & Windows       |
| `status`            | `string`         | Current process state.                    | Linux         |
| `cpu_usage`         | `float` | CPU utilization percentage for the process.                                 | Linux & Windows |
