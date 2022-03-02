---

```javascript
const result = await ExpressSDK.erc721.order.sellNFTByBid(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  tokenId, // Token Id of NFT
  initialPrice, // Initial Bidding Price of NFT
  ownerAddress, // Address of current owner
  auctionTime // Auction Time Period in seconds
);
```

It emits the same event emitted by [sellNFT](/sdk/erc721/PublicCollection/5_Selling/) function i.e. **TokenMetaReturn.**

Items on auction sale can be bid by others using saleId.

---
