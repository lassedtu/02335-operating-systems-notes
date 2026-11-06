Unix shells provide operators for redirecting the [[Standard File Descriptors|standard input, output, and error]] of a command, letting programs exchange data without requiring them to implement their own file handling mechanisms.

## How It Works

| Operator | Purpose | Example |
|---|---|---|
| `>` | Redirects standard output to a file | `ls > output.txt` |
| `<` | Redirects standard input from a file | `sort < input.txt` |
| `\|` | Connects the output of one command to another | `ls \| wc -l` |

The `|` operator is implemented underneath using a **[[Pipe]]**, connecting the write end of one process's output to the read end of another process's input.
