# endian-type

[![crates.io](https://img.shields.io/crates/v/endian-type?label=latest)](https://crates.io/crates/endian-type)
[![Documentation](https://docs.rs/endian-type/badge.svg)](https://docs.rs/endian-type/)
[![License](https://img.shields.io/crates/l/endian-type.svg)]()

Type safe wrappers for types with a defined byte order.

### Example

```rust
use endian_type::{types, BigEndian, LittleEndian, NetworkOrder};

// the endianness reflects the type-safety of the declaration
let foo = 0xbeef_u32;
let foo_be = BigEndian::from(foo);
assert_eq!(foo_be.as_bytes(), &foo.to_be_bytes());

// the deref implementations will allow you to operate the wrapped types as if they are regular
// numbers
let foo = u128::MAX;
let foo_le = LittleEndian::from(foo);
assert_eq!(foo_le.wrapping_add(1), 0);

// we also have a couple of aliases to be used as helper
//
// this will assert our `NetworkOrder` type is in accordance with the IETF RFC1700
let foo = -0xdead_i32;
let foo_no = NetworkOrder::from(foo);
let foo_be = types::i32_be::from(foo);
assert_eq!(foo.to_be_bytes(), foo_no.as_bytes());
assert_eq!(foo.to_be_bytes(), foo_be.as_bytes());
```
