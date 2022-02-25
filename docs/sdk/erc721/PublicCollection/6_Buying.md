---

```javascript
const result = await ExpressSDK.erc721.order.buyNFT(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  saleId, // Sale Id of NFT
  buyerAddress, // Address of buyer
  price // Price of item
);
```

After the successful execution of this function, token ownership and price money are transferred between the new owner and previous owner respectively.

---
