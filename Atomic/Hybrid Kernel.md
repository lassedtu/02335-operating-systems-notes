In practice, many modern operating systems do not strictly follow either the pure [[Monolithic Kernel]] or the pure [[Microkernel]] model, blending ideas from both. This hybrid approach is one of the main answers to the design question behind [[Operating System Structure]].

## How It Works

A hybrid kernel borrows efficiency from the monolithic side, running most core services in [[Kernel Mode]] for speed, and modularity from the microkernel side, keeping some services more isolated, where it makes sense for the system.

## Examples

- The **NT kernel**, used in Windows since the early 2000s (including on phones and the Xbox).
- The **XNU kernel**, used across macOS, iOS, and watchOS.

Both are real-world examples of this hybrid approach.
