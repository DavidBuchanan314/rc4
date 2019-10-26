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

cipher = RC4(b"secret", streaming=False)
msg = b"Not very secret message"

ciphertext = cipher.crypt(msg)
print(ciphertext) #=> b'\xa3Y\xa6<\xf4\xc1\xa4\xdf\x12\xb8\xde\xbf\x81\x83\x81\x17\xc0R\x01\x91\xe2\x94\xa1'

plaintext = cipher.crypt(ciphertext)
print(plaintext) #=> b'Not very secret message'

assert(plaintext == msg)
```
