# btls

[![CI](https://github.com/0x676e67/btls/actions/workflows/ci.yml/badge.svg)](https://github.com/0x676e67/btls/actions/workflows/ci.yml)
![Crates.io License](https://img.shields.io/crates/l/btls)
[![crates.io](https://img.shields.io/crates/v/btls.svg)](https://crates.io/crates/btls)

BoringSSL bindings for the Rust programming language and TLS adapters for [tokio](https://github.com/tokio-rs/tokio).

## This fork

This is [Netweir](https://github.com/netweir/netweir)'s fork of btls, on
the `netweir` branch, at upstream's `12988758`, the revision wreq pins.
Netweir uses it to send Firefox's Encrypted Client Hello over TCP. It
changes nothing a connection sends unless it's asked for, except where
noted:

- `SslContextBuilder::set_ech_inner_like_nss(enabled)`
  (`SSL_CTX_set_ech_inner_like_nss`, patch 0011): write the
  ClientHelloInner as NSS writes it, with the encrypted_client_hello
  marker first and the ClientHelloOuter's cipher suites.
- delegated_credentials and record_size_limit, which only the patches
  here send, are compressed into ech_outer_extensions like BoringSSL's
  own extensions, since they're the same in both ClientHellos.

## Documentation
 - BoringSSL API: <https://docs.rs/btls>
 - BoringSSL FFI bindings: <https://docs.rs/btls-sys>
 - tokio BoringSSL adapters: <https://docs.rs/tokio-btls>
 - compio BoringSSL adapters: <https://docs.rs/compio-btls>

## Usage

To use `btls`, first add this to your `Cargo.toml`:

```toml
[dependencies]
btls = "0.5"
```

Next, add this to your crate:

```rust
use btls::ssl::{{Ssl, SslConnector};

fn main() {
    // ...
}
```

## License

Licensed under either of Apache License, Version 2.0 ([LICENSE](LICENSE) or
http://www.apache.org/licenses/LICENSE-2.0).

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the [Apache-2.0](LICENSE) license,
shall be licensed as above, without any additional terms or conditions.

## Accolades

The project is based on a fork of [boring](https://github.com/cloudflare/boring).
