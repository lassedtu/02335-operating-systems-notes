A file is a data container in the file system, typically stored on a disk, but files are not limited to physical storage devices, see [[Everything Is a File]].

## How It Works

Directories group files together, providing an organisational structure for the file system. Files and directories are organised in hierarchical trees, starting from a root directory.

A running [[Process]] accesses an open file through a **[[File Descriptor]]**, a handle returned by the operating system rather than the raw file itself. Access to a file's contents is restricted through **[[File Permissions]]**.
