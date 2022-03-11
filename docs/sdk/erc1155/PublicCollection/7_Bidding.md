---

```javascript
const result = await ExpressSDK.erc1155.order.bid(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  saleId, // Sale Id of NFT
  buyerAddress, // Address of bidder/buyer
  bidPrice // Bid Price placed on item
  amount // Amount of token
);
```

An event is emitted in this function call:

**BidOrderReturn**: It can be retrieved from the returned transaction receipt.

```javascript
const bidOrderReturn = result.events.BidOrderReturn.returnValues.bid;
```

_bidOrderReturn_ variable is an object with following key-value pairs:

```
{
  saleId: "97"; // Sale Id of the item
  tokenAmount: "10" //Amount of token
  sellerAddress: "0xe18B1dFb94BB3CEC3B47663F997D824D9cD0f4D2"; // Address of seller
  buyerAddress: "0x3A0b38AAC59429e628f3064bb0332061d0602883"; //Address of the buyer
  price: "60000"; // Buyer's bid on the item
  withdrawn: false; // Current status of the bid
}
```

---
