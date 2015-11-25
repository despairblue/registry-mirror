registry-mirror
===============

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://ipn.io) [![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs) [![Dependency Status](https://david-dm.org/diasdavid/registry-mirror.svg?style=flat-square)](https://david-dm.org/diasdavid/registry-mirror) [![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/feross/standard) [![Build Status](https://img.shields.io/travis/diasdavid/registry-mirror/master.svg?style=flat-square)](https://travis-ci.org/diasdavid/registry-mirror)

> Set up a NPM registry mirror, using your favourite storage, including IPFS! :D

# Quick setup (probably all that you need)

## Install IPFS dev0.4.0

```bash
$ go get -u github.com/ipfs/go-ipfs
$ cd $GOPATH/src/github.com/ipfs/go-ipfs
$ git checkout dev0.4.0
$ go install ./cmd/ipfs
$ ipfs version
ipfs version 0.4.0-dev
```

## Run IPFS daemon

```bash
$ ipfs daemon
Initializing daemon...
Swarm listening on /ip4/127.0.0.1/tcp/4001
Swarm listening on /ip4/192.168.1.64/tcp/4001
Swarm listening on /ip4/192.168.10.172/tcp/4001
Swarm listening on /ip6/2001:8a0:7ac5:4201:4816:fd56:bea7:eaf3/tcp/4001
Swarm listening on /ip6/2001:8a0:7ac5:4201:ae87:a3ff:fe19:def1/tcp/4001
Swarm listening on /ip6/::1/tcp/4001
API server listening on /ip4/127.0.0.1/tcp/5001
Gateway (readonly) server listening on /ip4/127.0.0.1/tcp/8080
Daemon is ready
```

## Install registry-mirror

```bash
$ npm i registry-mirror -g
```

## Run registry-mirror

Wait for the `Updated directory listing` log.

```bash
$ registry-mirror daemon --ipfs
IPFS mode ON
registry-mirror [info] using output directory /npm-registry/
registry-mirror [info] listening on 127.0.0.1:50321
registry-mirror [info] Cloning NPM OFF
registry-mirror [info] Updated directory listing, good to go :)
```

Port `50321` is default and can be set with `--port`.

## Configure npm

Set up your npm to use `registry-mirror` with the default port through:

```bash
$ npm config set registry http://localhost:50321
```

If you picked another `--port` you need to adjust accordingly.

Good to npm install away! :)

# Usage

## CLI

```bash
$ registry-mirror
Usage: registry-mirror COMMAND [OPTIONS]

Available commands:

daemon  Mirror npm registry
```

## Commands

### daemon

`$ registry-mirror daemon`

Options:
- `--folder` - Name of the directory where the registry gets downloaded to
- `--blob-store` - Custom blob-store support (must follow [abstract-blob-store]() interface)
- `--clone` - Download the entire npm (Otherwise it just tries to read)
- `--ipfs` - Use local IPFS Node (must support the files/mfs API, available from version 0.4.0 onwards)
- `--port` Listen on the specified port
- `--host` Listen on the specified port

## Important

If you are on Mac OS X, make sure to increase the limit of files open (with `ulimit -Sn 4096`), otherwise the ipfs daemon will be sad and throw 502 replies.

# Acknowledgements

This module takes a lot of inspiration from [reginabox](https://www.npmjs.com/package/reginabox). Big thank you to everyone that contributed with code or to the [discussion](https://github.com/ipfs/notes/issues/2) to make this happen.
