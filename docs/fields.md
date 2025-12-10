# Fields Collected

## Filesystem

- Request:

| Field      | Data Type   | Description                                                                 | Platform  |
|--------------------|-------------|------------------------------------------------------------------------------|------------------------|
| `timestamp`        | `datetime` | The exact time when the request occurred                       | Linux & Windows |
| `op_name`          | `string`    | Operation type of the reqeust         | Linux & Windows |
| `pid`              | `int`       | Process ID that performed the requst                                     | Linux & Windows |
| `process_name`     | `string`    | Name of the process performing the request                                | Linux & Windows |
| `filename`         | `string`    | The full path or name of the file being access                            | Linux & Windows |
| `inode`            | `int` | The inode number associated with the file    | Linux         |
| `size`   | `int` | Data transfer amount in bytes           | Linux & Windows        |
| `flags_str`        | `string`    | String representation of file operation flags       | Linux        |

- State:

| Field         | Data Type   | Description                                                                 | Platform  |
|----------------------|-------------|------------------------------------------------------------------------------|------------------------|
| `path`              | `string`    | Full path of the file being recorded This will be anonimized if enabled       | Linux & Windows         |
| `file_size`         | `int`  | Size of the file in bytes                                              | Linux & Windows       |
| `created_time`      | `float` | Timestamp when the file was created                                | Linux & Windows        |
| `modified_time`     | `float` | Timestamp when the file was last modified                           | Linux & Windows        |


## Block

- Request:

| Field         | Data Type         | Description                                                                 | Platform  |
|-----------------------|------------------|------------------------------------------------------------------------------|------------------------|
| `timestamp`           | `datetime` | The time when the block I/O operation occurred                            | Linux & Windows |
| `pid`                 | `int`            | Process ID that issued the I/O request                                     | Linux & Windows |
| `tid`                 | `int`            | Thread ID within the process that performed the I/O operation              | Linux        |
| `process_name`        | `string`         | Name of the process performing the block I/O                               | Linux & Windows |
| `lba`                 | `int` | Identifies the location of the I/O on disk         | Linux & Windows |
| `op_type`             | `string`         | Operation type                                         | Linux & Windows       |
| `size`                | `int` | Size of the I/O request in bytes                                           | Linux & Windows      |
| `nr_sectors`          | `int`            | Number of 512-byte sectors affected by the operation                       | Linux         |
| `cpu_id`              | `int`            | CPU core ID where the I/O request was executed                             | Linux        |
| `parent_process_id`   | `int`            | Process ID of the parent process that triggered the I/O                    | Linux        |
| `latency`      | `float`         | Time it takes for a block request to finish                          | Linux & Windows     |


## Cache

- Request:

| Field | Data Type | Description | Platform |
|-------|-----------|-------------|---------------|
| `timestamp` | `int` | The time when the block I/O operation occurred | Linux |
| `pid` | `int` | Process identifier | Linux |
| `process_name` | `string` | Process command name | Linux |
| `status` | `string` | HIT or MISS | Linux |

## Network

| Field | Data Type | Description | Platform |
| --- | --- | --- | --- |
| `timestamp` | `datetime` | Time when the request was taken | Linux & Windows |
| `pid` | `int` | Process ID | Linux & Windows |
| `process_name` | `int` | Name of process that trigger the network request | Linux & Windows |
| `source_address` | `string` | Address source of the requests | Linux & Windows |
| `destination_address` | `string` | Address destination of the requests | Linux & Windows |
| `source_port` | `int` | Port source of the requests | Linux & Windows |
| `destination_port` | `int` | Port destination of the requests | Linux & Windows |
| `size` | `int` | Size of the request in bytes | Linux & Windows |
| `type` | `string` | The type of the request (send / receive) | Linux & Windows |



## Process

- State:

| Column Name        | Data Type           | Description                                                                 | Platform Availability |
|---------------------|--------------------|------------------------------------------------------------------------------|------------------------|
| `timestamp`         | `datetime` | Time when the process state snapshot was taken                            | Windows       |
| `pid`               | `int`              | Process ID                                                                 | Linux & Windows |
| `name`              | `string`           | Process name                                                               | Linux & Windows |
| `cmd`               | `string`           | Full command line used to start the process | Linux & Windows      |
| `virtual_size`      | `int` | Virtual memory size of the process in bytes                                | Windows only      |
| `working_set_size`  | `int`  | Amount of physical memory (RAM) currently used by the process, in bytes    | Windows only       |
| `memory_info`       | `int` | Resident Set Size (RSS), actual physical memory used by the process       | Linux only      |
| `creation_date`     | `datetime` | Time when the process was created                                         | Linux & Windows       |
| `status`            | `string`         | Current process state                    | Linux         |
| `cpu_usage_5s`         | `float` | CPU utilization percentage for the process, calculated in 5 second interval | Linux & Windows |
| `cpu_usage_2m`         | `float` | CPU utilization percentage for the process, calculated in 2 minute interval | Linux & Windows |
| `cpu_usage_1h`         | `float` | CPU utilization percentage for the process, calculated in 1 hour interval | Linux & Windows |
