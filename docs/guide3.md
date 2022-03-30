***

### Build a NFT-Ticketing Dapp using Pandora-express SDK

### Intro

  In this guide we will build a Dapp using Express Protocol SDK through which Event organizers or Movie makers can mint and sell their NFT Tickets directly on Ethereum .<br>
  Tickets are basically a ERC1155 token that the owner want to distribute in the market and owners can also save some tickets for some particular address.
  Owners can then Sell these tickets in the market using Pandora Marketplace SDK.

  Alright without further ado, let's build our Dapp!

### Prerequisites
#### Some Prequisites required before building the project:
    NodeJS version > 16.0.0
    NPM version > 6.0.0
    Metamask Browser Extension

### Code

  **1.Creating Project:**

  Create an empty folder in your favourite editor. We will use VScode here.
  We will use Parcel for bundling the javascript code.

  **2.SDK installation** 
      
  Run in terminal

  ```bash
  npm init 
  npm i pandora-express parcel
  ``` 
  ![Screenshot](/media/pandora-install.png)

  **3.Building the UI**

   Make a index.html file and paste the following code.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>SDK</title>
  </head>
  <body>
    <h1>NFT Ticket Booking</h1>
    <div id="Collection1155">
      <h4>Create Event(Collection)</h4>
      <input
        type="text"
        id="collection1155Uri"
        required
        placeholder="Enter Collection URI"
      />
      <input
        type="text"
        id="collection1155Description"
        required
        placeholder="Enter collection Description"
      />
      <input
        type="number"
        id="collection1155Royalties"
        required
        placeholder="Enter collection Royalties"
      />

      <button id="btnCreateCollection1155">Create Collection</button>
    </div>

    <div id="mintInCollection1155">
      <h4>Mint Tickets(Tokens)</h4>
      <input
        type="text"
        id="collection1155Address"
        required
        placeholder="Enter collection Address"
      />
      <input
        type="text"
        id="token1155Id"
        required
        placeholder="Enter TokenId"
      />
      <input
        type="text"
        id="token1155URI"
        required
        placeholder="Enter TokenURI"
      />
      <input
        type="number"
        id="numMintInCol1155Amount"
        required
        placeholder="Enter Amount of Tokens"
      />

      <button id="btnMintInCollection1155">Mint in collection</button>
    </div>

    <div id="sellInCollection1155">
      <h4>Sell Tickets(Tokens)</h4>
      <input
        type="text"
        id="sellCollection1155Address"
        required
        placeholder="Enter collection Address"
      />
      <input
        type="number"
        id="sell1155TokenId"
        required
        placeholder="Enter TokenId"
      />
      <input
        type="number"
        id="sell1155Price"
        required
        placeholder="Enter Price"
      />
      <input
        type="number"
        id="numSellInCol1155Amount"
        required
        placeholder="Enter Amount of Tokens"
      />

      <button id="btnSellInCollection1155">Sell in collection</button>
    </div>


    <script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
    <script src="main.js"></script>
  </body>
</html>

```
Now run in terminal
```bash
parcel index.html
```
Our HTML page will look something like this.
![Screenshot](/media/html3.png)

**5.Getting Data from User from Frontend**

Now as we defined the functions for our Dapp, the last step is to get the function parameters using javascript DOM.

Paste the code written below to main.js.


```javascript
const { createPandoraExpressSDK } = require("pandora-express");

init = async () => {
  if (window.ethereum) {
    window.web3 = new Web3(window.ethereum);
    await window.ethereum.enable();
    console.log("Connected");
  } else {
    alert("Metamask not found");
  }
};

createCollection = async () => {
  let ExpressSDK = createPandoraExpressSDK();
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
 const result = await ExpressSDK.erc1155.collection.createCollection(
    web3,
    chainId,
    accounts[0],
    collectionURI.value,
    collectionDescription.value,
    [[accounts[0], collectionRoyalties.value]]
  );

  console.log(result);
};

mintInCollection = async () => {
  let ExpressSDK = createPandoraExpressSDK();
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
 const result = await ExpressSDK.erc1155.collection.mint(
    web3,
    collectionAddress.value,
    tokenID.value,
    itemColNumber.value,
    tokenURI.value,
    accounts[0]
  );
  console.log(result)
};

sellInCollection = async () => {
  let ExpressSDK = createPandoraExpressSDK();
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  const result = await ExpressSDK.erc1155.collection.sellNFT(
    web3,
    chainId,
    sellCollectionAddress.value,
    sellTokenId.value,
    sellPrice.value,
    accounts[0],
    itemSellNumber.value
  );
  console.log(result)
};

const collectionURI = document.getElementById("collection1155Uri");
const collectionDescription = document.getElementById("collection1155Description");
const collectionRoyalties = document.getElementById("collection1155Royalties");
const CollectionButton = document.getElementById("btnCreateCollection1155");
CollectionButton.onclick = createCollection;

const collectionAddress = document.getElementById("collection1155Address");
const tokenURI = document.getElementById("token1155URI");
const tokenID = document.getElementById("token1155Id");
const itemColNumber = document.getElementById("numMintInCol1155Amount");
const btnMintInCollection = document.getElementById("btnMintInCollection1155");
btnMintInCollection.onclick = mintInCollection;

const sellCollectionAddress = document.getElementById("sellCollection1155Address");
const sellTokenId = document.getElementById("sell1155TokenId");
const sellPrice = document.getElementById("sell1155Price");
const itemSellNumber = document.getElementById("numSellInCol1155Amount");
const btnSellInCollection = document.getElementById("btnSellInCollection1155");
btnSellInCollection.onclick = sellInCollection;

init();
```

**That's it!**

  Congratulations! You have created your NFT Ticket Booking Dapp, minted as well as listed your Event Tickets for sale in the Marketplace ! If you want to use this functionality and numerous others like timed auction, bidding, etc today in your app, check out the [Express SDK](sdk/overview.md) section which gives you a plug and play SDK component for front end.

***
