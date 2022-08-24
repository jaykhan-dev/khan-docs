---
tags:
  - python
  - hash function
  - hash
  - crypto
  - cryptography
---

# Hash Functions

In a nutshell, hash functions take a string and return a fixed length value that cannot be reversed.

```python
import hashlib

message = "This is a string!"
strings = [
    "hello",
    "sha256",
    "bitcoin rails"
]

hash_obj = hashlib.sha256(message.encode())
hash_val = hash_obj.hexdigest()

print(hash_val)
print(len(hash_val))

for string in strings:
    string_hash = hashlib.sha256(string.encode())
    string_hash_val = string_hash.hexdigest()
    print(f"Hash #{strings.index(string) +1}: {hash_val})
```
