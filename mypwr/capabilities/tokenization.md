# Tokenization

The system creates digital twins of energy sources as well as of their produced energy. This enables use cases for aggregation and disaggregation of energy sources as well as use cases based on the utility of an energy source.

With this release the use case of multi-ownership is implemented, where the ownership of energy sources is represented by a number of tokens. Those tokens are then distributed to the members of a community. Based on the energy production of an energy source, as well as on the number of tokens a member owns, the members receive utility tokens to their wallets which represents the proportionally energy production of a member.

All the machines and users in the system are associated with cryptographic keys with which they are represented on the blockchain.​

**Dual Token Design**

The concept of this dual token design is to represent the energy (KWH) with one token, and fractional ownership of a specific energy source with another token. Both tokens rely on an Ethereum based blockchain

**KWH Token**

The KWH token was implemented as a smart contract that follows the ERC20 standard. Every time a measurement of an energy source is captured by the system, the energy source mints the number of KWH tokens based on the the energy difference to the previous measurement.

**Ownership Token**

The PV token(s) are implemented as a smart contract that follows the ERC1155 standard. Every energy source is represented as own token type, where as tokens from the same energy source are fungible. For every energy sources added to the system, a new token type will be created with a fixed supply of token. The tokens are added to the contract owner in the beginning from where they can be transferred to the members.

**Layered Blockchains**

The dual token design described above can be deployed on two different blockchain technologies. For this release only the Polygon chain is used, but the contracts are ready to be used on both chains.

**Layer 1 - Ethereum**

The smart contracts can be deployed on Ethereum where the advantage is that it is a large and fairly distributed network. It has as well a high number of market places and variety of applications where the tokens could be used. Downside are the higher transaction fees.

**Layer 2 - Polygon**

The smart contracts deployed on Polygon lead to lower operation costs and higher transaction speed. One could argue that the network is smaller as Ethereum and therefore be less secure.

**Bridging Layer 1 and 2**

In order to transfer tokens between two blockchain technologies so called _bridges_ are used. They are smart contracts by themselves which verify confirmed transactions across blockchains and handle the minting and burning of tokens depending where tokens are transferred too. With this we can use the best of both worlds: Frequent smart contract calls can be executed on Polygon. If necessary tokens can be transferred to Ethereum.To be flexible with the deployment of smart contracts for bridging, smart contracts are built by keeping abstraction of concepts in mind: Methods and attributes used by smart contracts on the Ethereum (root chain) are often shared with the smart contracts deployed on Polygon (child chain). To enable this following smart contract hierarchy was implemented:

1. Contract: Move ERC20 logic (PV and KWH) to an ERC11550 BaseContract (Stand-alone contract that can be deployed without the use of a second layer technology)
2. Contract: Inherit from first contract an extend it with withdraw functions (This contract will be deployed on polygon)
3. Contract: Inherit from second contract and add mint functions (Will be deployed on the first level technology)
