# Why GeCo?

This library brings several key advantages over the one from the original publication.

## Support for Python 3.9 and above

A few years have passed since the original publication.
Since then, Python 2, which is the version of Python which the original library relied on, has reached end-of-life.


## Performance under the hood

Wherever possible, [NumPy](https://numpy.org/) and [Pandas](https://pandas.pydata.org/) are used to accelerate computations.
This makes the generation and corruption of synthetic data much more performant.

## Reliable, reproducible results

Random data requires random number generators (RNGs).
The original library rests entirely on Python's `random` module.
However, it utilizes Python's global RNG for all of its operations.
Applications that require the `random` module and seek to use the original library might run into issues from having to deal with shared state.

In this revision, all functions support the use of [NumPy's RNGs](https://numpy.org/doc/stable/reference/random/generator.html).
This means you can create an RNG instance with its own seed and use it for data generation and corruption.
You can also create multiple instances and assign an RNG to each generator and corruptor that you intend to use.
Dealing with shared RNG states is no issue unless, of course, you prefer it that way.