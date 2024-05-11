# MoString 🔥

This repository explores string concatenation in Mojo and strategies for performance optimization. We introduced `MoString`, a simple wrapper around the standard Mojo `String` struct that features a custom in-place addition operator (`__iadd__`). It primarily enhances performance by employing a pre-allocation memory strategy, akin to what is used in `StringBuilder` implementations.

We invite everyone interested to contribute different implementations of efficient string concatenation to this repository. Our aim is to build this repository into a valuable resource that could lead to a proposal for the Mojo standard library. Ideally, this repo will eventually render itself obsolete 🔥.

## Demo

This demo aims to highlight the memory management of MoString:

- The capacity (allocated memory) increases only when necessary.
- The current size is displayed as `X+1`, where "+1" represents the trailing null terminator each String in Mojo contains.
- Use the `optimize_memory` method to minimize the allocated memory to what's needed (`capacity=size`).
Access the underlying String variable through `mostring_var.string` for standard String operations, including the use of `+=`.

```python
from mostring import MoString

fn main():
    
    var text = MoString("Alice:")
    print(text.info())

    text+="\nIf I had"
    print(text.info())

    text+=" a world on my own"
    print(text.info())

    text.optimize_memory()
    print(text.info())

    text+=",\neverything"
    print(text.info())

    text+=" would be nonsense."
    print(text.info())

    text.string+="\nNothing would be what it is\nbecause everything would be what it isn't."
    print(text.info())

```

Output with additional comments:

```bash
# Init
Alice:
(Size: 6+1, Capacity: 7)

# Capcacity doubled twice
Alice:
If I had
(Size: 15+1, Capacity: 28)

# Capacity doubled
Alice:
If I had a world on my own
(Size: 33+1, Capacity: 56)

# optimize_memory call, memory/capacity is reduced to size
Alice:
If I had a world on my own
(Size: 33+1, Capacity: 34)

#  Capacity doubled
Alice:
If I had a world on my own,
everything
(Size: 45+1, Capacity: 68)

# Enough capacity available 
Alice:
If I had a world on my own,
everything would be nonsense.
(Size: 64+1, Capacity: 68)

# Direct String operation, capacity = size 
Alice:
If I had a world on my own,
everything would be nonsense.
Nothing would be what it is
because everything would be what it isn't.
(Size: 135+1, Capacity: 136)
```
