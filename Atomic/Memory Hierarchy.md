There is an old constraint in computer architecture: you want memory to be fast, large, and cheap, but you can only ever pick two of the three. No single memory technology satisfies all three at once.

## How It Works

This is exactly why real systems use **layered memory** instead of one uniform pool: small, extremely fast (and expensive) memory close to the [[CPU]], backed by progressively larger, slower, and cheaper memory further away. The fast layer closest to the CPU is the **cache**, discussed in detail in [[Cache Memory]].

This layered approach only helps if there is a reliable way to guess which data should live in the fast, expensive layer at any given moment. The system does not actually know, it has to guess, but it can make very good guesses by relying on the **[[Principle of Locality]]**.
