OpenFaaS Rust Hasura Action function
=============================================

An OpenFaaS Hasura Action written in Rust actix-web.

## Installation

```sh
faas template pull https://github.com/austinrivas/rust-hasura-action-template
```

## Create Function

```sh
faas new <name> --lang rust-hasura-action
```

## Testing

```sh
cargo test --manifest-path ./function/Cargo.toml
```

### Format

```sh
cargo fmt --manifest-path ./function/Cargo.toml
```

### Linting

```sh
cargo clippy --manifest-path ./function/Cargo.toml
```

## Deployment

```sh
faas up -f function.yml --gateway $GATEWAY_URL
```

## Remote Dev

This function includes an [`okteto.yml`](function/okteto.yml) function to facilitate remote dev and debugging.

```bash
cd function
okteto up
 ✓  Development environment activated
 ✓  Files synchronized
    Namespace: austinrivas
    Name:      rust-hasura-action-hello
    Forward:   8080 -> 8080
               9229 -> 9229
okteto> fwatchdog
```

This will compile the function in the remote dev environment. Rust is fast code that compiles slow, so patience is a virtue here. Okteto will cache the build so that later compilations will be much faster.

Okteto will syncronize local changes with the remote environment.

Currently remote debugging is not implemented, however it is a future goal of this project.

## [Template](https://github.com/austinrivas/rust-hasura-action-template)

This function is based on the OpenFaaS [rust-hasura-action-template](https://github.com/austinrivas/rust-hasura-action-template).

This template provides a thin wrapper around the [actix-web Server](https://actix.rs/).

## [Function Handler](function/src/lib.rs)

## Extras

This repo also contains an [Okteto Remote Development Configuration](function/okteto.yml) for use on the [Okteto Platform](https://okteto.com/).

A [github action](.github/workflows/check-lint-test-format.yml) is included that will trigger on pull request. This action runs the rust tests / lint / check / format.
