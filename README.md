`ord`
=====

`ord` is an index, block explorer, and command-line wallet. It is experimental
software with no warranty. See [LICENSE](LICENSE) for more details.

Ordinal theory imbues litoshis with numismatic value, allowing them to
collected and traded as curios.

Ordinal numbers are serial numbers for litoshis, assigned in the order in which
they are mined, and preserved across transactions.

See [the docs](https://docs.ordinals.com) for documentation and guides.

See [the BIP](bip.mediawiki) for a technical description of the assignment and
transfer algorithm.

See [the project board](https://github.com/users/casey/projects/3/) for
currently prioritized issues.

See [milestones](https://github.com/casey/ord/milestones) to get a sense of
where the project is and where it's going.

Join [the Discord server](https://discord.gg/87cjuz4FYg) to chat with fellow
ordinal degenerates.

Donate
------
BTC - `bc1qqt2hz97ys62gg3gaq2cuxgqx5hw4rnyxnvpqkv`

LTC - `ltc1qfmvk898k6jgfgp98dhsc5gvr9hpxl2ggd25ygk`

Wallet
------

`ord` relies on litecoin Core for private key management and transaction signing.
This has a number of implications that you must understand in order to use
`ord` wallet commands safely:

- Litecoin Core is not aware of inscriptions and does not perform sat
  control. Using `litecoin-cli` commands and RPC calls with `ord` wallets may
  lead to loss of inscriptions.

- `ord wallet` commands automatically load the `ord` wallet given by the
  `--wallet` option, which defaults to 'ord'. Keep in mind that after running
  an `ord wallet` command, an `ord` wallet may be loaded.

- Because `ord` has access to your litecoin Core wallets, `ord` should not be
  used with wallets that contain a material amount of funds. Keep ordinal and
  cardinal wallets segregated.

### Pre-alpha wallet migration

Alpha `ord` wallets are not compatible with wallets created by previous
versions of `ord`. To migrate, use `ord wallet send` from the old wallet to
send sats and inscriptions to addresses generated by the new wallet with `ord
wallet receive`.

Installation
------------

`ord` is written in Rust and can be built from
[source](https://github.com/casey/ord). Pre-built binaries are available on the
[releases page](https://github.com/casey/ord/releases).

You can install the latest pre-built binary from the command line with:

```sh
curl --proto '=https' --tlsv1.2 -fsLS https://ordinals.com/install.sh | bash -s
```

Once `ord` is installed, you should be able to run `ord --version` on the
command line.

Building
--------

On Debian and Ubuntu, `ord` requires `libssl-dev` when building from source:

```
sudo apt-get install libssl-dev
```

You'll also need Rust:

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

To build `ord` from source:

```
git clone https://github.com/casey/ord.git
cd ord
cargo build --release
```

`ord` requires `rustc` version 1.67.0 or later. Run `rustc --version` to ensure you have this version. Run `rustup update` to get the latest stable release.

Syncing
-------

`ord` requires a synced `litecoind` node with `-txindex` to build the index of
satoshi locations. `ord` communicates with `litecoind` via RPC.

If `litecoind` is run locally by the same user, without additional
configuration, `ord` should find it automatically by reading the `.cookie` file
from `litecoind`'s datadir, and connecting using the default RPC port.

If `litecoind` is not on mainnet, is not run by the same user, has a non-default
datadir, or a non-default port, you'll need to pass additional flags to `ord`.
See `ord --help` for details.

Logging
--------

`ord` uses [env_logger](https://docs.rs/env_logger/latest/env_logger/). Set the
`RUST_LOG` environment variable in order to turn on logging. For example, run
the server and show `info`-level log messages and above:

```
$ RUST_LOG=info cargo run server
```

New Releases
------------

Release commit messages use the following template:

```
Release x.y.z

- Bump version: x.y.z → x.y.z
- Update changelog
- Update dependencies
- Update database schema version
```
