Every [[Process]] typically starts with three predefined [[File Descriptor|file descriptors]] already open.

## How It Works

| File Descriptor | Name | Purpose |
|---|---|---|
| `0` | STDIN | Standard input |
| `1` | STDOUT | Standard output |
| `2` | STDERR | Standard error |

These descriptors can be redirected to different files or I/O resources, see [[Shell Redirection]] for how a shell does this, and [[Pipe]] for how `dup2()` is used to redirect one of them into a pipe.
