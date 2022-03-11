---

```javascript
const result = await ExpressSDK.erc1155.order.sellNFT(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  tokenId, // Token Id of NFT
  tokenPrice, // Selling Price of NFT
  ownerAddress, // Address of current owner
  tokenAmount // Amount of token to sell
);
```

An event is emitted in this function call:

**TokenMetaReturn**: It can be retrieved from the returned transaction receipt.

```javascript
const tokenMetaEvent = result.events.TokenMetaReturn.returnValues.data;
```

_tokenMetaEvent_ variable is an object with following key-value pair:

```
{
     collectionAddress:  "0x9095Ee504caeADfdA6EA81Ee8EC625a5827a6BF2"; //Address of Collection
     tokenId: "2"; //ID of token
     numberOfTokens: "10"; //Amount of token to mint
     price: "100"; //Base Selling price
     directSale: true; //Direct sale or not
     bidSale: false; //Bid Sale or not
     status: true; //Status of token
     currentOwner: "0xbEc53EBdf7833B9d8747522287d5781d265A3e87"; //Current owner of token
}
```

---
