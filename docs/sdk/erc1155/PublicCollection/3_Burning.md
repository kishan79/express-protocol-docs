---

```javascript
const result = await ExpressSDK.erc1155.nft.burn(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  ownerAddress, // Address of token owner
  tokenId // Id of token to burn
  tokenAmount //Amount of token to burn
);
```

Successful execution of this function will burn token associated to respective tokenId.

---
