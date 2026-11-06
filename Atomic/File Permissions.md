Access to [[File|files]] is restricted through file permissions, which determine which users can read, write, or execute a file.

## How It Works

File permissions are represented as a bitmap consisting of nine permission bits, divided into three groups:

- **Owner**: permissions assigned to the file's owner.
- **Group**: permissions assigned to users belonging to the file's group.
- **Others**: permissions assigned to all remaining users.

Each group contains three permission bits:

| Permission | Symbol | Octal Value |
|---|---|---|
| Read | `r` | 4 |
| Write | `w` | 2 |
| Execute | `x` | 1 |

The permissions can be inspected using:

```bash
ls -al
```

Example output:

```text
-rwxr-xr-- 1 lasse users 1024 Nov 6 example
```

The permission string `-rwxr-xr--` indicates that the owner has read, write, and execute permissions, the group has read and execute permissions, and others have read permissions.

### Changing Permissions

```c
int chmod(const char *path, mode_t mode);
```

This syscall changes the permissions of a file specified by its path.

## Examples

```bash
chmod 754 example
```

The octal value `754` represents the following permissions:

- Owner: `7` = read, write, execute.
- Group: `5` = read, execute.
- Others: `4` = read.
