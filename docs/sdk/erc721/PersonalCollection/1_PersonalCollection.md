---
A personal collection can be deployed using SDK and inside a collection, user can furthur mint and trade tokens.

```javascript
const result = await ExpressSDK.erc721.collection.createCollection(
web3, // Web3 instance configured with metamask provider
chainId, // Network id of blockchain
ownerAddress, // Address of the collection creator
name, // Name of the collection
symbol, // Symbol of the collection
description, // Description of the collection
collectionRoyalties // Royalties received by the owner
);
```

When this function is executed an event is emitted **ERC721Deployed** which contains the address of the collection.

```javascript
const collectionContractAddress =
result.events.ERC721Deployed.returnValues._tokenAddress;
```

This variable will contain the required contract address of the collection.
---
