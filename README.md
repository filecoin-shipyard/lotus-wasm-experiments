lotus-wasm-experiments
======================

Experimenting with re-using Lotus to build WebAssembly modules

# Demos

## ClientQueryAsk

* https://ipfs.io/ipfs/QmbsMbojwFWCVvEoc8e3boxuqrWx3aUwerc7BRog3eCcfU/
* Source: https://github.com/jimpick/wasm-client-query-ask-demo

# Branches

Many Filecoin and libp2p projects have been forked experimentally. This section
of the README consists of pointers to modified branches so they can be more
easily found later. Very little of this work is ready to merge yet.

## Development

* **libp2p-caddy**: https://github.com/jimpick/libp2p-caddy/tree/p2pclient

  This is the branch where the experimentation has been done up until now. It
  consists of some Caddy configurations (for SSL), Parcel (for JS development
  and bundling) + some test daemons and some standalone CLI test programs,
  plus HTML + JS + code for a WASM bundle.

* **lotus**: https://github.com/jimpick/lotus/tree/jim/wasm-client-query-ask

  This is the Lotus source, heavily modified to isolate only the dependencies
  needed for the ClientQueryAsk JSON-RPC API method. In the future, it may
  be possible to use Go build tags to simulaneously support native and WASM
  builds ... but presently native builds are broken on this branch.

* **go-fil-markets**: https://github.com/jimpick/go-fil-markets/tree/jim/wasm-client-query-ask

  This module is also heavily modified to isolate the dependencies for
  ClientQueryAsk and to support using go-libp2p-daemon

* **go-ws-transport**: https://github.com/jimpick/go-ws-transport/tree/jim-feat-wss-dialing-new-go

  Incorporates unmerged WebSockets over SSL support from 0x + updates for
  latest go WASM.

* **go-libp2p**: https://github.com/jimpick/go-libp2p/tree/jim-pruned-for-wss

  Quickly pruned some modules with dependencies that don't work for WASM.

* **go-reuseport-transport**: https://github.com/jimpick/go-reuseport-transport/tree/jim-pruned-for-wss

  Quickly pruned some modules with dependencies that don't work for WASM.

* **go-jsonrpc**: https://github.com/jimpick/go-jsonrpc/tree/jim-wasm

  Implemented a new JS <=> Go bridge (client and server) using a subset of
  the WebSocket implementation.

* **go-libp2p-daemon**: https://github.com/jimpick/go-libp2p-daemon/tree/jim-ws

  Implemented new control stream via websockets - re-used portion of websocket
  implementation in go-ws-transport - uses custom wsdaemon and wssdaemon
  protocols added to go-multiaddr (it would probably be cleaner to implement
  a non-multiaddr based websocket stream handler). The p2pclient library
  now works from WASM in a web browser.

* **go-multiaddr**: https://github.com/jimpick/go-multiaddr/tree/jim-dialer-wss

  Added support for wss (from 0x) plus wsdaemon and wssdaemon for
  go-libp2p-daemon

* **Lotus JS Client**

  Additionally, a new "provider" was written for Lotus JS Client to talk
  to the JS <=> Go bridge in go-jsonrpc. Also, some code was borrowed to
  proxy JSON-RPC requests from WASM to JS to an external JSON-RPC server
  (typically a Lotus Gateway instance). This code currently lives in
  the libp2p-caddy repo above.

# License

Dual-licensed under [MIT](https://github.com/filecoin-project/lotus/blob/master/LICENSE-MIT) + [Apache 2.0](https://github.com/filecoin-project/lotus/blob/master/LICENSE-APACHE)
