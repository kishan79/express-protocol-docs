---

```javascript
const result = await ExpressSDK.erc1155.nft.mint(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  minterAddress, // Address of Minter
  tokenAmount, //Amount of token
  tokenURI, // TokenURI String
  royalties // Nested array of royalties
);
```

```
royalties for a token is of the form: [ [recipientAddress1, royaltyFraction1],
                                        [recipientAddress2, royaltyFraction2],
                                         .
                                         .
                                        [recipientAddressN, royaltyFractionN] ]

```
***Note:*** N can be atmost 10

It returns the receipt of the on-chain transaction. Information from Emitted Events can be retrieved by looking at the transaction receipt.
Two events are emitted in this function call:

**-> TransferSingle**: It can be retrieved from the returned transaction receipt.

```javascript
const transferEvent = result.events.TransferSingle.returnValues;
```

_transferEvent_ variable is an object with following key-value pair:


```
{
  operator: "0x0000000000000000000000000000000000000000", //zero address
  from: "0x0000000000000000000000000000000000000000", // zero address
  to: "0xbEc53EBdf7833B9d8747522287d5781d265A3e87", // minter address
  tokenId: "11" // token id of minted token,
  value: 5, //token Amount
}
```

**-> RoyaltiesSetForTokenId**: It can also be retrieved in a similar manner

```javascript
const royaltiesEvent = result.events.RoyaltiesSetForTokenId.returnValues;
```

_royaltiesEvent_ variable is an object with following key-value pair:

```
{
  royalties: [["0xbEc53EBdf7833B9d8747522287d5781d265A3e87", "100"]] // array of royalties
  tokenId: "11" // token id of minted token
}
```

Token Minted on a specific network can be put on Sale or Auction further on the same Network.

---
