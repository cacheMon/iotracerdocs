# Privacy Protection Measures

## Anonymization Efforts

IO Tracer provides an option for users to anonymize their data. This means that certain [fields](fields.md) are anonymized through hashing. Fields that may contain sensitive information, such as `filename` / `filepath` and `command`, are locally hashed using the `SHA-256` algorithm, making it impossible for us to view their original content.

For file paths, our hashing method preserves the directory structure while anonymizing specific segments. Specifically, we hash the directory and file names beyond the first two levels, while keeping the top-level directories and the file extension intact.

For example:
`foo/bar/baz.txt` → `foo/bar/baa5a0964d3320fb.txt`

In contrast, command strings are fully hashed to ensure complete privacy.

For instance:
`"C:\WINDOWS\system32\svchost.exe -k RPCSS -p"` → `314b08c9fe3a404f`

## Automatic Filtering
The tool systematically excludes virtual filesystems such as `/proc`, `/sys`, `/dev`, and `tmpfs`, which contain system-generated information rather than hardware information. To prevent recursive loops and maintain system performance, the tracer implements self-tracing prevention by automatically excluding its own input/output operations from the collection. Additionally, the system filters out special files including pipes, sockets, and device files.

## Data Minimization Techniques
The tool features configurable cache event sampling, allowing researchers to capture representative information patterns by recording only a specified ratio of events, such as one in every ten operations. To prevent excessive storage consumption, the tool implements time-based log rotation with a default 24-hour cycle, automatically archiving older data while maintaining recent activity logs. Process-specific filtering capabilities enable users to focus data collection on particular applications or exclude unnecessary system processes from monitoring. Finally, the tool incorporates automatic compression and cleanup routines that optimize storage space and remove outdated information.

## Excluded Information
- File contents or personal user data
- Network packet payloads
- User credentials or passwords
- Environment variables
