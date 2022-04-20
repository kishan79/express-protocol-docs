***

### Create NFT Drop Dapp using Pandora-express SDK

### Intro

  In this guide we will build a Dapp using Express Protocol SDK through which NFT makers/celebs can mint and sell their NFT collection directly on Ethereum.<br>
  Basically celebs and NFT creators can make their own collection and can drop NFTs, whenever they want. 
  These NFT collection can later be traded using Express SDK.
  You need to connect a wallet, so make sure you have metamask wallet installed.

  Alright without further ado, let's create our Dapp!

### Prerequisites
#### Some Prequisites required before building the project:
    NodeJS version > 16.0.0
    NPM version > 6.0.0
    Metamask Browser Extension
    Parcel Bundler(For bundling Javascript)

### Code

  **1.Creating Project:**

  Create an empty folder in your favourite editor. We will use VScode here.


  **2.SDK installation** 
      
  Run in terminal

  ```bash
  npm init 
  npm i pandora-express
  npm install -g parcel-bundler 
  ``` 
  ![Screenshot](/media/pandora-install.png)

  **3.Building the UI**

   Make a index.html file and paste the following code. <br>
   We have made three section here, first is for creating the collection ie.. creating the smart contract for the NFT collection, user will have to fill the input fields for Collection's Name, Symbol, Description and royalities.<br>
   Now their is NFT ticket minting section, in technical terms Collection owner can mint ERC1155 token in the smart contract they have made earlier, For this we have three input fields in which owner should enter the Collection address, Token's URI and the royalities that has to be shared with other people. <br>
   Now the Owner have to sell the NFT Tickets in the market, so their is a sell ticket function which takes Collection address, TokenID and Price of the token as input.

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
    <h1>NFT Drop</h1>
    <div id="Collection">
      <h4>Create Collection</h4>
      <input
        type="text"
        id="collectionName"
        required
        placeholder="Enter Collection Name"
      />
      <input
        type="text"
        id="collectionSymbol"
        required
        placeholder="Enter collection Symbol"
      />
      <input
        type="text"
        id="collectionDescription"
        required
        placeholder="Enter collection Description"
      />
      <input
        type="number"
        id="collectionRoyalties"
        required
        placeholder="Enter collection Royalties"
      />

      <button id="btnCreateCollection">Create Collection</button>
    </div>

    <div id="mintInCollection">
      <h4>Mint in collection</h4>
      <input
        type="text"
        id="collectionAddress"
        required
        placeholder="Enter collection Address"
      />
      <input type="text" id="tokenURI" required placeholder="Enter TokenURI" />
      <input
        type="number"
        id="royalties"
        required
        placeholder="Enter Royalties"
      />

      <button id="btnMintInCollection">Mint in collection</button>
    </div>

    <div id="sellInCollection">
      <h4>Sell in collection</h4>
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
      <input type="number" id="sellPrice" required placeholder="Enter Price" />

      <button id="btnSellInCollection">Sell in collection</button>
    </div>

     <script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
    <script src="main.js"></script>
  </body>
</html>
```

Now run the app with live server<br>
As we have pasted the code, now our frontend will look something like this:

![Screenshot](/media/html2.png)

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

Now, we have to define the Create collection function, that will create a ERC721 smart Contract, through which the owner can mint any number of NFT they want. 

```javascript
const createCollection = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.collection.createCollection(
    web3,
    chainId,
    accounts[0],
    collectionName.value, //Name of Collection
    collectionSymbol.value, // Symbol of Collection
    collectionDescription.value, // Description of Collection
    [[accounts[0], collectionRoyalties.value]] // Royalities
  );
};
```

After creating collection, creators can Mint their NFT using pandoraSDK.erc721.collection.mint() function.<br>
Let's define a function for the same.

```javascript
const mintInCollection = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.collection.mint(
    web3,
    collectionAddress.value, //Address of collection Contract
    tokenURI.value, // URI of token
    accounts[0], // Account to mint NFT
    [[accounts[0], collectionRoyalties.value]] // Royalities
  );
}
```

After Minting NFTs, Owners/Creators can put their NFTs on sale using pandoraSDK.erc721.collection.sellNFT() function

```javascript
const sellInCollection = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.collection.sellNFT(
    web3,
    chainId,
    sellCollectionAddress.value, // Collection Address
    sellTokenId.value, // Token ID
    sellPrice.value, // Base price to sell
    accounts[0]
  );
};
```

**5.Getting Data from User from Frontend**

Now as we defined the functions for our Dapp, the last step is to get the function parameters using javascript DOM.

Paste the code written below to main.js.


```javascript
const collectionName = document.getElementById("collectionName");
const collectionSymbol = document.getElementById("collectionSymbol");
const collectionDescription = document.getElementById("collectionDescription");
const collectionRoyalties = document.getElementById("collectionRoyalties");

const CollectionButton = document.getElementById("btnCreateCollection");
CollectionButton.onclick = createCollection;

const collectionAddress = document.getElementById("collectionAddress");
const tokenURI = document.getElementById("tokenURI");
const royalties = document.getElementById("royalties");

const btnMintInCollection = document.getElementById("btnMintInCollection");
btnMintInCollection.onclick = mintInCollection;

const sellCollectionAddress = document.getElementById("sellCollectionAddress");
const sellTokenId = document.getElementById("sellTokenId");
const sellPrice = document.getElementById("sellPrice");

const btnSellInCollection = document.getElementById("btnSellInCollection");
btnSellInCollection.onclick = sellInCollection;

init();
```

Now run in terminal
```bash
parcel index.html
```

 **That's it!**

  Congratulations! You have created your first NFT Drop and minted as well as listed your first Token for sale in the Marketplace ! If you want to use this functionality and numerous others like timed auction, bidding, etc today in your app, check out the [Express SDK](sdk/overview.md) section which gives you a plug and play SDK component for front end.

***