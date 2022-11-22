# Feature Utils
This crate implements a collection of helpful feature-related macros. These macros
serve to make it easy to have helpful compiler messages when dealing with sets of
related, sometimes mutually exclusive features.


## Stability
We are pre-0.1, so we make no stability guarantees currently. Cargo consideres 0.0.* to
mean that all new versions are possibly breaking changes.


## Example

Inside `build.rs`:
```rust
// Each of these embedded microcontrollers are mutually exclusive and at least one
// must be provided.
feature_utils::mandatory_and_unique!("esp32c3", "esp8266", "nrf52840");
fn main() {}
```

This results in one message if you don't pass any features:

```text
error: You must provide one of the mandatory features!
 --> src/lib.rs:18:1
  |
5 | feature_utils::mandatory_and_unique!("esp32c3", "esp8266", "nrf52840");
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: this error originates in the macro `$crate::at_least_one_provided` which comes
from the expansion of the macro `feature_utils::mandatory_and_unique` (in Nightly
builds, run with -Z macro-backtrace for more info)
```

And another message if you pass multiple mutually exclusive features:

```text
error: features "esp32c3" and "nrf52840" cannot be used together!
 --> src/lib.rs:18:1
  |
5 | feature_utils::mandatory_and_unique!("esp32c3", "esp8266", "nrf52840");
  | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  |
  = note: this error originates in the macro `$crate::unique` which comes from the
expansion of the macro `feature_utils::mandatory_and_unique` (in Nightly builds, run
with -Z macro-backtrace for more info)
```

## License
All code in this repository is dual-licensed under either:

- MIT License ([LICENSE-MIT](LICENSE-MIT))
- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE))

at your option. This means you can select the license you prefer!

Unless you explicitly state otherwise, any contribution intentionally submitted for
inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual
licensed as above, without any additional terms or conditions.
