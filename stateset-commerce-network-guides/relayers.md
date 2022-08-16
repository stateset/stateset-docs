# Relayers

**Stateset Network is currently partnering with relayers for our stateset-1-testnet. If you are interested in becoming a Stateset packet relayer please get in touch.**

Relayers relay transaction packets on the Stateset Network and other IBC-enabled blockchains.

Stateset is able to communicate with other smart contracts via IBC.

**IBC**

The inter-blockchain communication protocol is a catalyst for the polycentric interchain.

Different application specific blockchain networks are going in to be used in different use cases.

The Problem: Before IBC, blockchains cannot talk to each other, transfer packets, between blockchains such as token transfers, signatures, votes and other types of transactions. Currently all of the assets on different chains are siloed.

The Solution: IBC is a messaging protocol for the interchain. Authenticated, Ordered and Route topology between networks. IBC enables chain innovation and continuous innovation across multiple state machines.

IBC represent's application-layer packet semantics Application layer protocols sit on top of IBC. Cross-Chain account abstraction: delegate control to another chain. What state machine interacts. Interchain code relocation: transport contracts in packets.

IBC/TAO: Transport, authencation ordering.

Transport data, assets, tokens from one zone to another another.

Authenticating that the data came from this Blockchain and is going to a different blockchain network or state machine. Authenticating that data came from another Blockchain network is interacting with a contract on another Blockchain.

The Ordering abstraction allows to reason about the ordering of the transactions.

IBC Protocol Stack consist of clients, connections, channels, packets, and modules:

* Client: verifying consensus transcripts
* Connections: associating two chains. Created with a handshake. Paired set of identifiers.
* Channels: data pipe between two modules. Channels handle Ordering Semantics and routing Semantics.
* Packets: Where the action happens. The core messages, can contain different types of data. Token transfers, votes, etc. analogous to the core.

![](../.gitbook/assets/channel-state-machine.png)

_**Documentation on running a relayer for Stateset will be coming soon.**_
