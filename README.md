Bitcoin Cash regtest
=====================
[![Build Status](https://travis-ci.org/slashrsm/bitcoin-cash-regtest.svg?branch=master)](https://travis-ci.com/slashrsm/bitcoin-cash-regtest)
[![Docker Pulls](https://img.shields.io/docker/pulls/slashrsm/bitcoin-cash-regtest.svg?maxAge=2592000)](https://hub.docker.com/r/slashrsm/bitcoin-cash-regtest)

Docker images for Bitcoin Cash regtest. Let you run the Bitcoin Cash regtest in no time.

| Software | Version | Tags | Dockerfile |
| --- | --- | --- | --- |
| Bitcoin unlimited | 1.5.0.0 | `bu-1.5.0.0, bu-latest, latest` | [Dockerfile](https://github.com/slashrsm/bitcoin-cash-regtest/blob/master/BU/1.5.0.0/Dockerfile) |

## Quick start

```
docker run -it --name bch-regtest slashrsm/bitcoin-cash-regtest:latest
```

To run `bitcoin-cli`

```
docker exec bch-regtest bitcoin-cli -conf=/opt/bitcoin/bitcoin.conf getinfo
```

## Generating blocks

To "mine" 10 blocks and send block reward to the internal wallet:

```
docker exec bch-regtest bitcoin-cli -conf=/opt/bitcoin/bitcoin.conf generate 10
```

To mine 15 blocks and send the block reward to `[some-address]`:

```
docker exec bch-regtest bitcoin-cli -conf=/opt/bitcoin/bitcoin.conf generatetoaddress 15 [some-address]
```

The block reward becomes spendable after 100 blocks which means that 101 blocks need to be generated initially.

## RPC authentication

RPC username and password are set to `regtest`.

## HTTP RPC

Container exposes ports `18332` and `18333`. In order to connect to the endpoint from host machine map the ports when running the container:

```
docker run -it --name bch-regtest -p 18332:18332 slashrsm/bitcoin-cash-regtest:latest
```

And then connect to it:

```
curl --user regtest:regtest --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getinfo" }' -H 'content-type: text/plain;' http://127.0.0.1:18332/
```

## Copyright

Copyright Janez Urevc 2018

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.