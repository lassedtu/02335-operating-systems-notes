A layered operating system organizes the OS as a hierarchy of layers, where inner layers are more privileged than outer ones. It is one of the main approaches to [[Operating System Structure]], sitting conceptually between a [[Monolithic Kernel]] and a [[Microkernel]].

## How It Works

This buys high flexibility: it is easy to extend the system as long as a new layer respects its interface with the layer immediately above and below it. The cost is lower efficiency, since a procedure in an outer layer may need the equivalent of multiple [[System Call]]s just to reach an inner resource, and in practice, deciding exactly where to draw the boundaries between layers is genuinely difficult to get right.
