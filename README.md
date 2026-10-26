# Downstream CI for Rust's `libc` on OpenBSD

Daily CI that runs the [`libc`](https://github.com/rust-lang/libc) test suite
on OpenBSD, which `libc`'s own CI only builds and does not test. It is based on
<https://github.com/tgross35/libc-downstream-ci>.

This does the following:

* Launch CI once per day (or manually, for `main` or `libc-0.2`)
* Check out both this repo and rust-lang/libc
* Apply all patches in the `patches` directory to `libc`
* Boot an OpenBSD VM with [vmactions/openbsd-vm](https://github.com/vmactions/openbsd-vm)
* Install the release's `rust` package and run `libc`'s `ci/run.sh`

Targets:

| Target | OpenBSD | Rust |
|--------|---------|------|
| `x86_64-unknown-openbsd` | 8.0 | 1.98.1 (from packages) |
| `x86_64-unknown-openbsd` | 7.9 | 1.94.1 (from packages) |

See <https://github.com/rust-lang/libc/issues/5209> for more details.

## Patches

Patches in `patches/` are applied with `git am` before testing. Fixes found
here should be submitted upstream to rust-lang/libc.

## Licensing

This is derived from `libc`'s CI so available under the same licenses (MIT
or Apache-2.0).
