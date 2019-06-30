# SnaPy
[![Build Status](https://travis-ci.com/justinnbt/SnaPy.svg?branch=master)](https://travis-ci.com/justinnbt/SnaPy)
[![PyPI version](https://badge.fury.io/py/snapy.svg)](https://badge.fury.io/py/snapy)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
<br>
Python library for detecting near duplicate texts in a corpus at scale using Locality Sensitive Hashing.<br>
As described in Mining Massive Datasets http://infolab.stanford.edu/~ullman/mmds/ch3.pdf.

## Installation
Install SnaPy using: `pip install snapy`<br>
Install mmh3 library needed for Minhash using: `pip install mmh3`

## Quickstart Example
``` python
from snapy import MinHash, LSH

content = [
    'Jupiter is primarily composed of hydrogen with a quarter of its mass being helium',
    'Jupiter moving out of the inner Solar System would have allowed the formation of inner planets.',
    'A helium atom has about four times as much mass as a hydrogen atom, so the composition changes '
    'when described as the proportion of mass contributed by different atoms.',
    'Jupiter is primarily composed of hydrogen and a quarter of its mass being helium',
    'A helium atom has about four times as much mass as a hydrogen atom and the composition changes '
    'when described as a proportion of mass contributed by different atoms.',
    'Theoretical models indicate that if Jupiter had much more mass than it does at present, it would shrink.',
    'This process causes Jupiter to shrink by about 2 cm each year.',
    'Jupiter is mostly composed of hydrogen with a quarter of its mass being helium',
    'The Great Red Spot is large enough to accommodate Earth within its boundaries.'
]

labels = [1, 2, 3, 4, 5, 6, 7, 8, 9]

seed = 3

# Create MinHash object.
minhash = MinHash(content, char_n_gram=9, permutations=100, hash_bits=64, method='universal', seed=3)

# Create LSH model.
lsh = LSH(minhash, labels, no_of_bands=50)

# Query to find near duplicates for text 1.
print(lsh.query(1, sensitivity=8))
>>> [8, 4]

```
## MinHash
Generates MinHash object that contains matrix of Minhash Signatures for each text.
### Parameters
<b>text: {list or ndarray}</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;Iterable containing text strings.<br><br>
<b>char_n_gram: int, optional, default: 9</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;Number of characters to be used in each shingle.<br><br>
<b>permutations: int, optional, default: 100</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;Number of hash values in each document signature.<br><br>
<b>vhash_bits: int, optional, default: 64</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;Hash value size, must be 32, 64 or 128 bit.<br><br>
<b>method: str, optional, default: 'universal'</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;Method to be used for minhash function, must be universal or k_smallest_values.<br><br>
<b>seed: int, optional, default: None</b><br>
&nbsp;&nbsp;&nbsp;&nbsp;Seeds from which to generate random hash function.<br><br>

## Contributing
Contributions are very welcome, message us or just submit a pull request!

## Authors
Justin Boylan-Toomey

## License
MIT License
