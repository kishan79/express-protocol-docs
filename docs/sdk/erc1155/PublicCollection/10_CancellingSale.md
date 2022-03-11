---

```javascript
const result = await ExpressSDK.erc721.order.cancelSale(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  sellerAddress, // Address of the seller
  saleId // Sale Id of the item
);
```

After the successful execution of this function, an Item that was on direct sale or auction sale will be removed from sale

---
