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


  **2.SDK installation** 
      
  Run in terminal

  ```bash
  npm init 
  npm i pandora-express 
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
    <h1>NFT Ticket</h1>
    <div id="createItem">
      <h4>Create Event</h4>
      <input
        type="text"
        id="txtCreateItemURI"
        required
        placeholder="Enter BaseURI"
      />
      <input 
        type="text"
        id="desc"
        required
        placeholder="Enter Description of Ticket"
      />
      <input
        type="number"
        id="collectionRoyalties"
        required
        placeholder="Enter collection Royalties"
      />

      <button id="btnCreateItem">Create Event</button>
    </div>

    <div id="mintTickets">
      <h4>Mint Event Tickets</h4>
      <input
        type="text"
        id="collectionAddress"
        required
        placeholder="Enter collection Address"
      />
      <input type="number" id="tokenId" required placeholder="Enter TicketID" />
      <input type="number" id="tokenAmount" required placeholder="Enter Ticket Amount" />
      <input type="text" id="tokenURI" required placeholder="Enter TicketURI" />
      <input type="text" id="minterAddress" required placeholder="Enter Your Address" />

      <button id="btnMintInCollection">Mint Tickets</button>
    </div>

    <div id="sellInCollection">
      <h4>Sell Events Tickets</h4>
      <input
        type="text"
        id="sellCollectionAddress"
        required
        placeholder="Enter collection Address"
      />
      <input
        type="number"
        id="sellTokenId"
        required
        placeholder="Enter TokenId"
      />
      <input type="number" id="price" required placeholder="Enter Price" />
      <input type="text" id="seller" required placeholder="Enter Your Address" />
      <input type="number" id="sellAmount" required placeholder="Enter Ticket Amount to sell" />
      <button id="btnSellInCollection">Sell Tickets</button>
    </div>

     <script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
    <script src="main.js"></script>
  </body>
</html>
```

Now run the app with live server<br>
As we have pasted the code, now our frontend will look something like this:

![Screenshot](/media/html3.png)

**4.Using SDK code with our javascript Logic**

  Make a Javascript file, name it main.js, 
  Now we have to import SDK function in our Dapp and make connection with blockchain using metamask.
  Paste the code below in main.js file.

```javascript
  //Import createPandoraExpressSDK from SDK
  const { createPandoraExpressSDK } = require("pandora-express");
  const pandoraSDK = createPandoraExpressSDK();

  //Connecting with Metamask wallet.
  const init = async () => {
  //check if metamask is present
    if (window.ethereum) {
      window.web3 = new Web3(window.ethereum);
      await window.ethereum.enable();
      console.log("Connected");
    } else {
      alert("Metamask not found");
    }
  };

```

Now we can start with our createCollection function which will create a new contract ie.. event, in which we can later mint tickets.
We will use pandoraSDK.erc1155.collection.createCollection() for implememting the above functionality.
```javascript
const createCollection = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  await pandoraSDK.erc1155.collection.createCollection(
      web3,
      chainId, 
      accounts[0], 
      itemURI, //Base URI of Event Data
      description, //Description of Event
      royalties //Royalities of Ticket
    )
}
```

After creating the Event, the owner can mint any amount of Ticket he/she want using pandoraSDK.erc1155.collection.mint() function
```javascript
const batchMint1155Nft = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  await pandoraSDK.erc1155.collection.mint(
      web3, 
      collectionAddress, 
      tokenId, //ID of Ticket
      tokenAmount, //Amount of Ticket to be minted
      tokenURI, //URI of Event data
      minter //Event Owner Address
      );
}
```
Event Owner can sell their Tickets in the marketplace using the pandoraSDK.erc1155.collection.sellNFT function.
```javascript
const sell1155Nft = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  await pandoraSDK.erc1155.collection.sellNFT(
    web3, 
    chainId,
    sellCollectionAddress, //Collection Address
    sellTokenId, //TokenID
    price, // Base Price of Ticket
    sellerAddress, // Seller Address
    sellAmount //Amount of Ticket to sell
  );
}
```

**5.Getting Data from User from Frontend**

Now as we defined the functions for our Dapp, the last step is to get the function parameters using javascript DOM.

Paste the code written below to main.js.


```javascript
const itemURI = document.getElementById("txtCreateItemURI");
const description = document.getElementById("desc");
const royalties = document.getElementById("collectionRoyalties");
const createBtn = document.getElementById("btnCreateItem");
createBtn.onclick = createCollection

const collectionAddress = document.getElementById("collectionAddress")
const tokenId = document.getElementById("tokenId");
const tokenAmount = document.getElementById("tokenAmount");
const tokenURI = document.getElementById("tokenURI");
const minter = document.getElementById("minterAddress");
const mintBtn = document.getElementById("btnMintInCollection");
mintBtn.onclick = batchMint1155Nft;

const sellTokenId = document.getElementById("sellTokenId");
const sellCollectionAddress = document.getElementById("sellCollectionAddress");
const price = document.getElementById("price");
const sellerAddress = document.getElementById("seller");
const sellAmount = document.getElementById("sellAmount");
const sellBtn = document.getElementById("btnSellInCollection");
sellBtn.onclick = sell1155Nft;

init();
```

**That's it!**

  Congratulations! You have created your NFT Ticket Booking Dapp, minted as well as listed your Event Tickets for sale in the Marketplace ! If you want to use this functionality and numerous others like timed auction, bidding, etc today in your app, check out the [Express SDK](sdk/overview.md) section which gives you a plug and play SDK component for front end.

***
