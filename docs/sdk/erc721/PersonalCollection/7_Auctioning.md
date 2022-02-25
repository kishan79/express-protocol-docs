---

```javascript
const result = await ExpressSDK.erc721.collection.sellNFTByBid(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  collectionAddress, // Address of the collection
  tokenId, // Token Id of the item
  initialPrice, // Initial Price to be set for an item
  ownerAddress, // Address of the item owner
  auctionTime // Auction Time Period in seconds, i.e 120 is equal to 120s.
);
```

It emits the same event emitted by _sellNFT_ function i.e. **TokenMetaReturn** which can be accessed through

```javascript
const tokenMetaEvent = result.events.TokenMetaReturn.returnValues.data;
```

Items on auction sale can be bid by others using saleId which can be retrieved through _tokenMetaEvent_.

---
