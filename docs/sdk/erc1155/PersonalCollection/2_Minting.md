---

```javascript
const result = await ExpressSDK.erc1155.collection.mint(
  web3, // Web3 instance configured with metamask provider
  collectionAddress, // Address of the collection in which item will be minted
  tokenId, //ID of token
  tokenAmount, //Amount of token
  tokenURI, //Token URI String
  minterAddress, // Address of the owner/minter
  royalties // Nested Array of Royalties
);
```

After this function is executed, a tokenId will be generated corresponding to the minted item in that particular collection. This id is emitted in an event **RoyaltiesSetForTokenId** and it can be accessed through:

```javascript
const collectionTokenId =
  result.events.RoyaltiesSetForTokenId.returnValues.tokenId;
```

---
