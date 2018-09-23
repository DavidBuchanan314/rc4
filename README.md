# rc4
A python3 RC4 implementation that doesn't suck. (i.e. it's actually binary-safe...)

Literally every other implementation I could find relied on chr/ord to decode bytes,
which would fail on any invalid unicode sequences.

This implementation uses bytes/bytearray objects to work with binary data, and
has been tested against [RFC6229](https://tools.ietf.org/rfc/rfc6229.txt).

Supports python 3.4+.

## Example usage:

```python
from rc4 import RC4

ciphertext = RC4(b"secret").crypt(b"Not very secret message")
print(ciphertext)

plaintext = RC4(b"secret").crypt(ciphertext)
print(plaintext)
```
