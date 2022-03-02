---

```javascript
const result = await ExpressSDK.erc721.nft.batchMint(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  minterAddress, // Address of Minter
  totalNFT, // Number of tokens to mint
  arraytokenURI, // array of TokenURI String for each token
  royalties // array of royalties for each token
);
```

```
    royalties are of the form: [ royaltyArrayForToken1,
                                 royaltyArrayForToken2,
                                 .
                                 .
                                 royaltyArrayForTokenN ]
```

It emits the same events as by [Mint](/sdk/erc721/PublicCollection/2_Minting/) for all N tokens where N is the total number of tokens minted through ***batchMint***.

---
