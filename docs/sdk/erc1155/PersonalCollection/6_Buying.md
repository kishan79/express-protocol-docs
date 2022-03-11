---

```javascript
const result = await ExpressSDK.erc721.collection.buyNFT(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  saleId, // Sale Id of the item
  buyerAddress, // Address of the buyer
  buyPrice, // Price at which item is bought
  tokenAmount //Amount of token
);
```

After the successful execution of this function, token ownership and price money is transferred between the new owner and previous owner respectively

---
