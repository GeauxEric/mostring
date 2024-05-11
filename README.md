# MoString 🔥

variations over StringBuilder ideas in Mojo

## Demo

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

Output:

```bash
Alice:
(Size: 6+1, Capacity: 7)

Alice:
If I had
(Size: 15+1, Capacity: 28)

Alice:
If I had a world on my own
(Size: 33+1, Capacity: 56)

Alice:
If I had a world on my own
(Size: 33+1, Capacity: 34)

Alice:
If I had a world on my own,
everything
(Size: 45+1, Capacity: 68)

Alice:
If I had a world on my own,
everything would be nonsense.
(Size: 64+1, Capacity: 68)

Alice:
If I had a world on my own,
everything would be nonsense.
Nothing would be what it is
because everything would be what it isn't.
(Size: 135+1, Capacity: 136)
```
