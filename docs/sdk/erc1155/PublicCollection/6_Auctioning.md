---

```javascript
const result = await ExpressSDK.erc1155.order.sellNFTByBid(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  tokenId, // Token Id of NFT
  initialPrice, // Initial Bidding Price of NFT
  ownerAddress, // Address of current owner
  amount // Amount of Token
);
```

It emits the same event emitted by [sellNFT](/sdk/erc1155/PublicCollection/4_Selling/) function i.e. **TokenMetaReturn.**

Items on auction sale can be bid by others using saleId.

---
