# Technical Details - Linux

We are implementing [eBPF](https://ebpf.io/) through [BPF Compiler Collection](https://github.com/iovisor/bcc/tree/master). Kernel probes are then attached to several system calls that are related to I/O activities. These system calls are in a group of [Linux Storage Stack](https://wxdublin.gitbooks.io/deep-into-linux-and-beyond/content/io.html). 

Systems call that we used are as such:

| Layer | Syscall Traced |
|-------|------------------|
| VFS Layer | `vfs_read`, `vfs_write`, `vfs_open`, `vfs_fsync`, `vfs_fsync_range`, `__fput` |
| Block Layer | `block_rq_issue`, `block_rq_complete` |
| Page | `filemap_add_folio`, `folio_mark_accessed` |

