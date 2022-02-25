---

```javascript
const result = await ExpressSDK.erc721.order.sellNFT(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  tokenId, // Token Id of NFT
  tokenPrice, // Selling Price of NFT
  ownerAddress // Address of current owner
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
  bidEndTime: "0"; // Ending time of bid if item on auction
  bidSale: false; // Item on auction sale or not
  bidStartTime: "0"; // staring time of bid if item on auction
  collectionAddress: "0x9095Ee504caeADfdA6EA81Ee8EC625a5827a6BF2"; // collection address
  currentOwner: "0xbEc53EBdf7833B9d8747522287d5781d265A3e87"; // current owner address
  directSale: true; // item on direct sale or not
  mintedBy: "0x675056CeEBE35C6c6aB46d7a099CAfEADe153De1"; // minter address
  price: "1000"; // selling or initial bidding price of item
  saleId: "8"; // sale id of item
  status: true; // status of item
  tokenId: "11"; // token id of item
}
```

---
