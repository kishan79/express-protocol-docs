---

```javascript
const result = await ExpressSDK.erc721.collection.burn(
  web3, // Web3 instance configured with metamask provider
  collectionAddress, // Address of the collection
  ownerAddress, // Address of token owner
  tokenId // Id of token to burn
);
```

Successful execution of this function burns the token associated with the respective token Id inside the collection.

---
