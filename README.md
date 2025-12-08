# libbitcast

## support for

- 16, 24, 32, and 64 bit signed and unsigned integers, 24 bit integers are stored in their 32 bit counterpart
- 32, and 64 bit floats

## usage

```c
#include <stdio.h>
#include "bitcast.h"

void main() {
    // little endian 0xcafe
    const Byte raw_bytes[2] = {0xfe, 0xca}; 

    // contains 0xcafe
    uint16_t u_value = bitcastU16_LE(raw_bytes);

    printf("Deserialized U16: %x\n", u_value); 
}
```
