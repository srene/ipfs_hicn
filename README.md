# IPFS Interoperability with hICN

## hICN vs IPFS
* Both adopt Data-centric Networking.
* Both propose content addressing and named-based networking.
* (h)ICN is a network layer solution while IPFS works at the application layer.
* Security based on crypthographic addressing for IPFS vs third-party trust chain.

## Benefits of combining IPFS with hICN
* Use IPFS at the application layer combined with hICN for in-network caching at network level. 
  - Not only caching in the end-points but also in-network cachin in hICN routers.
* Improved performance in IPFS
  - Using in-network caching can improve network performance.
  - Better retrieval times.
  - Less bandwidth required. Traffic reduction in ISPs
* hICN and IPFS content compatibility
  - Availability of many IPFS application-level tools (js-ipfs, browser extensions) compatible with hICN
  - Possibility of using IPLD and IPNS in hICN
  
[<p align="center"><img src="https://user-images.githubusercontent.com/5974002/190433230-84114b78-5147-48b7-a50b-82b16a9cf4ba.png" width="500"/></p>](image.png)

## Solution 

<ol>  
    <li>IPFS name resolution  mapping IPFS Content Identifiers (CIDs) to hICN routable names (IPv6 addresses) so that it can take advantage of in-network caching.
          <ol>
              <li>IPFS content providers publishes PeerIds Linked to hICN addresses for each CID in the IPFS (Kademlia) DHT.</li>
              <li>IPFS can resolve to hICN addresses using the DHT.</li>
          </ol>
    </li>
    <li>hICN as a new libp2p protocol, integrable into IPFS.
       <ol>
          <li>Integration of hICN library into IPFS to request and receive content using hICN interests/content.</li>
      </ol>
    </li>
    <li>Integration of hICN in BitSwap mechanism
      <ol>
          <li>Integrate hICN interests with existing Bitswap messages for content retrieval.</li>
      </ol>
    </li>
</ol>

[<p align="center"><img src="https://user-images.githubusercontent.com/5974002/190439317-a8a1e849-a39f-4449-b406-f14b7909101b.png" width="250"/><p align="center"><img src="https://user-images.githubusercontent.com/5974002/190439494-3729aac3-e081-48c8-b878-741b1423eb27.png" width="250"/></p></p>](image.png)


# Software

* IPFS client

  We have modified IPFS client to include IPFS content publication in the DHT using hICN addresses and being able to request content using hICN protocol. 

  [go-ipfs](https://github.com/srene/go-ipfs)
  
* Bitswap

  Bitswap is the data trading module for ipfs. It manages requesting and sending blocks to and from other peers in the network. 
  Bitswap has two main jobs: to acquire blocks requested by the client from the network and to judiciously send blocks in its possession to other peers who want them
  We have modified bitswap to not only requesting content by connecting directly to other peers but also being able to request it from the network using protocol when a matching hICN address is found after querying the DHT.

  [go-bitswap](https://github.com/srene/go-bitswap)
  
* Libp2p hICN Protocol

  TBC

* Testing and evaluation.
  
  TBC
    

This project has been funded by Cisco grant xx(TBC)
