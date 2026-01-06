monetarium-ctl
==============

[![Build Status](https://github.com/monetarium/dcrctl/workflows/Build%20and%20Test/badge.svg)](https://github.com/monetarium/dcrctl/actions)
[![ISC License](https://img.shields.io/badge/license-ISC-blue.svg)](http://copyfree.org)

Monetarium-ctl is a command-line client for interacting with the JSON-RPC servers of
[monetarium](https://github.com/monetarium/monetarium-node) and
[monetarium-wallet](https://github.com/monetarium/monetarium-wallet).

## Usage

In its default configuration, monetarium-ctl connects to monetarium's mainnet RPC port on
localhost.  The `--wallet` and `--testnet` flags change these defaults to the
monetarium-wallet RPC port and/or testnet ports.  The `--rpcserver/-s` flag can be used
to specify other hostnames or IP addresses of the server, and can also be used
to override the port defaults.

Monetarium-ctl will attempt to read monetarium and monetarium-wallet config files for the
user/password authentication.  If these fields cannot be read, monetarium-ctl must be
manually configured with the correct authentication.  Permanent configuration
changes may be written to a config file in a platform-specific location:

* macOS: `~/Library/Application Support/Monetarium-ctl/monetarium-ctl.conf`
* Windows: `%LOCALAPPDATA%\Monetarium-ctl\monetarium-ctl.conf`
* Linux and other Unix: `~/.monetarium-ctl/monetarium-ctl.conf`

## Build and installation

- **Install Go 1.23 or higher version**

  Installation instructions can be found here: https://golang.org/doc/install.
  Ensure Go was installed properly and is a supported version:
  ```sh
  $ go version
  $ go env GOROOT GOPATH
  ```
  NOTE: if `GOROOT` and `GOPATH` are initialized they must not be on the same path.
  It is recommended to add `$GOPATH/bin` to your `PATH` according to the Golang.org
  instructions.

- **Build or Update monetarium-ctl**

  The latest release of monetarium-ctl may be built in a single command without cloning
  this repository:

  ```sh
  $ go install github.com/monetarium/monetarium-ctl@latest
  ```

  Alternatively, a development build can be performed by running `go install` in
  a locally checked-out repository.

  If you want to easily access `monetarium-ctl` from the command-line without having to
  type the full path to the binary every time, ensure the bin directory rooted
  at the path reported by `go env GOPATH` is added to your system path:

  * macOS: [how to add binary to your PATH](https://gist.github.com/nex3/c395b2f8fd4b02068be37c961301caa7#mac-os-x)
  * Windows: [how to add binary to your PATH](https://gist.github.com/nex3/c395b2f8fd4b02068be37c961301caa7#windows)
  * Linux and other Unix: [how to add binary to your PATH](https://gist.github.com/nex3/c395b2f8fd4b02068be37c961301caa7#linux)

## Developing

When developing either the `monetarium` or `monetarium-wallet` RPC servers and making
modifications to the RPC methods, you may want to build a development version of
`monetarium-ctl` supporting these changes.  Due to `monetarium-ctl` being built around
package-global method registrations and reflection, supporting these changes
only requires building with the updated packages.

This can be easily achieved by making use of a local Go workspace that uses the
development versions of `monetarium` and `monetarium-wallet` as follows:

```
$ go work init .
$ go work use ../node/rpc/jsonrpc/types ../wallet
```

## License

monetarium-ctl is licensed under the [copyfree](http://copyfree.org) ISC License.
