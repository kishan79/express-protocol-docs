***

### Create NFT Drop Dapp using Pandora-express SDK

### Intro

  In this guide we will build a Dapp using Express Protocol SDK through which NFT makers/celebs can mint and Transfer their NFT directly on Ethereum.<br>
  Basically celebs and NFT creators can mint their own NFTs and can drop NFTs, whenever they want. 
  These NFT can later be traded using Express SDK.
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
  npm install -g parcel 
  ``` 
  ![Screenshot](/media/pandora-install.png)

  **3.Building the UI**

   Make a index.html file and paste the following code. <br>
   We have made two section here, first is for creating NFT in which any user can mint NFT by giving TokenURI as an argument.<br>
   Now their is NFT drop/transfer section, the Owner can transfer the NFT in the market, so their is a transfer NFT function which takes TokenID and receiver's address <br>


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
    <div id="createItem">
      <h4>Mint NFT</h4>
      <input
        type="text"
        id="txtCreateItemURI"
        required
        placeholder="Enter TokenURI"
      />

      <button id="btnCreateItem">Mint NFT</button>
    </div>

    <div id="dropItem">
      <h4>Drop NFT</h4>
      <input
        type="number"
        min="1"
        step="1"
        id="numDropItemTokenId"
        placeholder="Enter TokenId"
        required
      />
      <input
        type="text"
        id="txtDropItemToAddress"
        placeholder="Enter receiver's address"
        required
      />

      <button id="btnDropItem">Drop NFT</button>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
    <script type="module" src="main.js"></script>
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

Now, The creators can Mint their NFT using pandoraSDK.erc721.nft.mint() function.<br>
Let's define a function for the same.

```javascript
mintNft = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.nft.mint(web3, chainId, accounts[0], itemURI.value, [
    [accounts[0], 100],
  ]);
};
```

After Minting NFTs, Owners/Creators can Drop/Transfer their NFTs using pandoraSDK.erc721.order.transferNFT() function

```javascript
dropNft = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.order.transferNFT(
    web3,
    chainId,
    accounts[0],
    dropItemToAddress.value,
    dropItemTokenId.value
  );
};
```

**5.Getting Data from User from Frontend**

Now as we defined the functions for our Dapp, the last step is to get the function parameters using javascript DOM.

Paste the code written below to main.js.


```javascript
const itemURI = document.getElementById("txtCreateItemURI");

const createItemButton = document.getElementById("btnCreateItem");
createItemButton.onclick = mintNft;

const dropItemToAddress = document.getElementById("txtDropItemToAddress");
const dropItemTokenId = document.getElementById("numDropItemTokenId");

const dropItemButton = document.getElementById("btnDropItem");
dropItemButton.onclick = dropNft;

init();
```

Now run in terminal
```bash
parcel index.html
```

 **That's it!**

  Congratulations! You have created your first NFT Drop and minted as well as transfer your first Token from  our Marketplace ! If you want to use this functionality and numerous others like timed auction, bidding, etc today in your app, check out the [Express SDK](sdk/overview.md) section which gives you a plug and play SDK component for front end.

***