The Portable Operating System Interface (POSIX) is a standardized Application Programming Interface (API) framework designed to maintain source compatibility across distinct operating systems. It standardizes things like [[System Call]] interfaces so that code written against POSIX can be recompiled, rather than rewritten, on a different POSIX-compliant system.

## How It Works

Operating systems relate to the standard in a few different ways:

- **POSIX-certified operating systems**: macOS, Solaris. These have been formally verified against the standard.
- **POSIX-compliant operating systems**: Linux, Android, FreeBSD, Contiki. These follow the standard closely in practice without pursuing formal certification.
- **Compatibility layers**: Cygwin provides a POSIX-compatible emulation environment on Microsoft Windows, which is not itself POSIX-compliant.
