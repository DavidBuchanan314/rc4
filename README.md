# rc4
A python3 RC4 implementation that doesn't suck. (i.e. it's actually binary-safe...)

> [!WARNING]
> RC4 is cryptographically broken. Treat it as if it were rot13, base64, or other trivial encoding. Only use this if you know precisely why you're using it.

Literally every other implementation I could find relied on chr/ord to decode bytes,
which would fail on any invalid unicode sequences.

Update: [PyCrypto's implementation](https://pycryptodome.readthedocs.io/en/latest/src/cipher/arc4.html) Isn't that bad, and you should probably use that instead, if you can. However, it places arbitrary restrictions on key size, which is a dealbreaker for some applications (i.e. legacy hardware/software backwards-compatibility).

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
