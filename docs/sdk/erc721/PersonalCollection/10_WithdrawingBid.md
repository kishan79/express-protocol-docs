---

```javascript
const result = await ExpressSDK.erc721.collection.withdrawBid(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  saleId, // Sale Id of the item on auction
  bidId, //Bid Id of the buyer in an auction
  buyerAddress // Address of the bidder
);
```

When the bidder wants to withdraw their bid, they can do so using this function. After successful execution of the function bid will be removed from the auction and the money will be transferred back to the bidder.

---
