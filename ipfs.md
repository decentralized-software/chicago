IPFS
==

Links
--

* [Project site][site]
* [go-ipfs][go-ipfs] (on GitHub)

[site]: https://ipfs.io
[go-ipfs]: https://github.com/ipfs/go-ipfs

Problem area
--

IPFS tackles the problem of addressing, versioning, and distributing binary blobs 
efficiently in a large, permissionless p2p network.


Resource allocation
--

Every organization in the network independently makes decisions about how to 
deploy their processor cycles, storage, and bandwidth.  This means that we have 
to pay some attention to incentives.

### Allocation factors

As requests for blobs and routing information stream in off the network, node 
operators have to (tacitly) decide whether to serve these requests, and how to 
prioritize requests that are served.

* Profit motive.  Node operators are always willing to serve data in exchange 
  for a high enough price.
* Politics.  The price for service the data depends on content.  Some node 
  operators may be willing to incur a cost to serve (even arbitrary) blobs when 
  they believe these blobs ought to be highly available.

### Default policy

The default policy (according to the whitepaper) is to maintain a share ratio 
for each peer and to serve a peer's requests with probability given by a 
function of this share ratio.  In this regime a node can try to balance its 
share ratio against other peers by the following heuristic.  If peer A requests 
a blob which the node operator doesn't have, the node operator can request the 
same blob from one or more peers for whom the share ratio is _higher_ than the 
share ration against peer A.  If the request succeeds, the node operator serves 
peer A's request.  Optimizing share ratios seems

### Filecoin
