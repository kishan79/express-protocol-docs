---

```javascript
const result = await ExpressSDK.erc721.collection.batchMint(
  web3, // Web3 instance configured with metamask provider
  collectionAddress, // Address of the collection
  minterAddress, // Address of Minter
  totalNFT, // Number of tokens to mint
  arraytokenURI, // array of TokenURI String for each token
  royalties // array of royalties for each token
);
```

The token Ids for minted tokens can be retrieved through the respective emitted events. (Transfer and RoyaltiesSetForTokenId events are emitted for each token minted through batchMint.)

---
