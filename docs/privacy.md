# Privacy Protection Measures

## Anonymization Efforts

IO Tracer provides an option for users to anonymize their data. This means that certain [fields](fields.md) are anonymized through hashing. Fields that may contain sensitive information, such as `filename` / `filepath` and `command`, are locally hashed using the `SHA-256` algorithm, making it impossible for us to view their original content.

### Filepath

For **file paths**, our hashing method preserves the directory structure while anonymizing specific segments. Specifically, we hash the directory and file names beyond the first two levels, while keeping the top-level directories and the file extension intact.

However, if there is only one level traced in the file path, the program will hash the whole structure.

For example:

- `/usr/bin/baz.txt` → `/usr/bin/baa5a0964d3320fb.txt`
- `/note.txt` → `/baa5a0964d3320fb.txt`

In contrast, command strings are fully hashed to ensure complete privacy.

For instance:

- `"C:\WINDOWS\system32\svchost.exe -k RPCSS -p"` → `314b08c9fe3a404f`

### Network

In terms of **network collection**, we'll hash the ip sent and received that has been traced.

Such as,

- `127.0.0.1` → `4c232a5821`
- `::1` → `7c102d5320`


## Excluded Information
- File contents or personal user data
- Network packet payloads
- User credentials or passwords
- Environment variables
