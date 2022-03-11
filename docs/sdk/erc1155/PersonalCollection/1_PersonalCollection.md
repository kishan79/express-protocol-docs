---

A personal collection can be deployed using SDK and inside a collection, user can furthur mint and trade tokens.

```javascript
const result = await ExpressSDK.erc1155.collection.createCollection(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  ownerAddress, // Address of the collection creator
  uri, // URL of Token
  description, //description of token
  collectionRoyalties // Royalties received by the owner
);
```

When this function is executed an event is emitted **ERC1155Deployed** which contains the address of the collection.

```javascript
const collectionContractAddress =
  result.events.ERC1155Deployed.returnValues._tokenAddress;
```

This variable will contain the required contract address of the collection.

---
