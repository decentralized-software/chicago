# IPFS

## Links

- [Project site][site]
- [go-ipfs][go-ipfs] (on GitHub)
- [whitepaper][wp] (on IPFS)

[site]: https://ipfs.io
[go-ipfs]: https://github.com/ipfs/go-ipfs
[wp]: /ipfs/QmR7GSQM93Cx5eAg6a6yRzNde1FQv7uL6X1o4k7zrJa3LX/ipfs.draft3.pdf

## TODO

- [ ] describe Filecoin though the resource allocation lens

## Problem area

IPFS tackles the problem of addressing, versioning, and distributing binary blobs
efficiently in a large, permissionless p2p network.

## Resource allocation

Every organization in the network independently makes decisions about how to
deploy their processor cycles, storage, and bandwidth. This means that we have
to pay some attention to incentives.

### Allocation factors

As requests for blobs and routing information stream in off the network, node
operators have to (tacitly) decide whether to serve these requests, and how to
prioritize requests that are served. Here are some reasonable assumptions:

- Profit motive. Node operators are always willing to serve data in exchange
  for a high enough price.
- Politics. The price for service the data depends on content. Some node
  operators may be willing to incur a cost to serve (even arbitrary) blobs when
  they believe these blobs ought to be highly available.

### Default policy

The default policy (according to the ipfs whitepaper) is to maintain a share ratio
for each peer and to serve a peer's requests with probability given by a
function of this share ratio. In this regime a node can try to balance its
share ratio against other peers by the following heuristic. If peer A requests
a blob which the node operator doesn't have, the node operator can request the
same blob from one or more peers for whom the share ratio is _higher_ than the
share ratio against peer A. If the request succeeds, the node operator serves
peer A's request.

## Use cases

### Content distribution

IPFS should help lower the cost of content distribution, especially when users
who wish to get content are also willing to serve the same content to new
generations of users. If a set of blobs is distributed across a large network
with high total bandwidth, it is harder to exhaust the bandwidth to DoS this
set of blobs. However, the nodes presently don't have a way to detect a DoS
attack, and coordinate around ignoring requests from the attack network.

### Censorship resistance

IPFS should make it more costly to censor content. Some relevant threat vectors:

1. Identify and filter all IPFS traffic. This is even more difficult when IPFS
   is paired with network obfuscation tools like VPNs or Tor. Connections in
   IPFS are encrypted, so packet inspection is not available to a passive
   adversary.
2. Poison the network with nodes who connect and allow requests for content to
   time out.
