---

```javascript
const result = await ExpressSDK.erc721.collection.sellNFT(
  web3, // Web3 instance configured with metamask provider
  chainId, // Network id of blockchain
  collectionAddress, // Address of the collection
  tokenId, // TokenId of the item in that collection
  sellingPrice, // Selling Price of the item
  ownerAddress // Address of the collection owner/minter
);
```

After this function is executed the seller of the collection will be able to put up an item on sale from its collection and an event **TokenMetaReturn** is emitted which contains key-value pairs.

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
