---

```javascript
const result = await ExpressSDK.erc1155.collection.acceptBid(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  SaleId, // Sale Id of the token
  BidId, // Bid Id of the buyer the seller wants to accept
  sellerAddress // Address of the seller
);
```

When the seller executes/accepts a bid before the auction’s end then a new event is emitted **BidExecuted** which can be retrieved through the following.

```javascript
const bidExecutedReturnValue = result.events.BidExecuted.returnValues.price;
```

_bidExecutedReturnValue_ will give the amount at which the bid was accepted.

---
