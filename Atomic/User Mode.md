User mode is a restricted execution environment with limited access to hardware and privileged instructions, designed to protect system stability and security. Every ordinary user program, and every application shown in the layered view of the [[Operating System]], runs here.

## How It Works

In user mode, the set of allowed instructions and accessible hardware resources is deliberately limited, in contrast to **[[Kernel Mode]]**, where the CPU can execute every instruction and use every piece of hardware. To reach a protected resource from user mode, a program has to make a **[[System Call]]**: normal execution is suspended, and the operating system takes control through a **trap**.

### Why User Mode at All?

It is worth asking directly why systems bother with this split, rather than just running everything in kernel mode all the time. Three real benefits justify the cost:

- It **enables the operating system to enforce management policies**, since applications can only reach protected resources by going through the OS, never around it.
- It provides **stability through isolation**: a bug in a user-mode program cannot, by construction, take down the entire system the way a kernel-mode bug can.
- It provides **security in multi-user systems**, preventing one user's [[Process]] from freely reaching into another's.

The cost is real too: transitioning between user mode and kernel mode is genuinely expensive computationally, so systems face a direct trade-off between how much protection they enforce and how efficient they can be. This trade-off is exactly what drives the different designs discussed in [[Operating System Structure]].
