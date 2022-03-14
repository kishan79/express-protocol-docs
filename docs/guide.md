***

### Create NFT Marketplace using Pandora-express SDK
<!-- CREATE NFT MARKETPLACE USING PANDORA-EXPRESS SDK : -->

 Make your own NFT marketplace for trading NFTs.

### Intro

  In this guide we will make NFT marketplace Dapp using Express Protocol SDK through which anyone can mint, buy and sell tokens.
  We will use Pandora Public ERC721 contract for NFT minting and Pandora Market Contract for Buying/Selling NFTs.
  You also need to connect a wallet, so make sure you have metamask wallet installed.

  Alright without further ado, let's create our marketplace!

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
    <div id="createItem">
      <h4>Create Item</h4>
      <input
        type="text"
        id="txtCreateItemURI"
        required
        placeholder="Enter TokenURI"
      />

      <button id="btnCreateItem">Create Item</button>
    </div>


    <div id="sellItem">
      <h4>Sell Item</h4>
      <input
        type="number"
        min="1"
        step="1"
        id="numSellItemTokenId"
        placeholder="Enter TokenId"
        required
      />
      <input
        type="number"
        min="1"
        step="1"
        id="numSellItemPrice"
        placeholder="Enter Price"
        required
      />

      <button id="btnSellItem">Sell Item</button>
    </div>
    

    <div id="buyItem">
      <h4>Buy Item</h4>
      <input
        type="number"
        min="1"
        step="1"
        id="numBuyItem"
        placeholder="Enter SaleId"
        required
      />
      <input
        type="number"
        min="1"
        step="1"
        id="numBuyItemAmmount"
        placeholder="Enter Ammount"
        required
      />

      <button id="btnBuyItem">Buy Item</button>
    </div>
     <script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
    <script src="main.js"></script>
  </body>
</html>
```

As we have pasted the code, now our frontend will look something like this:

![Screenshot](/media/html.png)

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

  Now, we have to define the Mint function, that will mint NFT using the SDK.

  ```javascript
  const mintNft = async () => {
  //get current account address
    const accounts = await web3.eth.getAccounts();
  //Get ChainID of current account
    const chainId = await web3.eth.net.getId();
  //Mint NFT using SDK erc721 nft mint
   await pandoraSDK.erc721.nft.mint(web3, chainId, accounts[0], itemURI.value, [
    [accounts[0], 100],
  ]);
  };
  ```

  We have minted a NFT using the SDK now, we can sell the NFT in the market using Sell function of the SDK.
  Define the Sell NFT function as written below.

  ```javascript
  const sellNft = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.order.sellNFT(
    web3,
    chainId,
    sellItemTokenId.value,
    sellItemPrice.value,
    accounts[0]
   );
  };
  ```

  We have put an NFT on sale, anyone else can buy the NFT by providing Price more than the sellItemPrice.

  You can also try buying the same NFT using different account in your metamask wallet.
  Try pasting the code below for buying NFT.

```javascript
const buyNft = async () => {
const accounts = await web3.eth.getAccounts();
const chainId = await web3.eth.net.getId();
console.log(chainId);
await pandoraSDK.erc721.order.buyNFT(
  web3,
  chainId,
  buyItemSaleId.value,
  accounts[0],
  buyItemAmmount.value
 );
};
```

**5.Getting Data from User from Frontend**

Now as we defined the functions for our NFT marketplace, the last step is to get the function parameters using javascript DOM.

Paste the code written below to main.js.


```javascript
const itemURI = document.getElementById("txtCreateItemURI");

const createItemButton = document.getElementById("btnCreateItem");
createItemButton.onclick = mintNft;

const itemURI1 = document.getElementById("txtCreateItemURI1");
const itemURI2 = document.getElementById("txtCreateItemURI2");

const createItemsButton = document.getElementById("btnCreateItemInBatch");
createItemsButton.onclick = batchMintNft;

const sellItemTokenId = document.getElementById("numSellItemTokenId");
const sellItemPrice = document.getElementById("numSellItemPrice");

const sellItemButton = document.getElementById("btnSellItem");
sellItemButton.onclick = sellNft;

const auctionItemTokenId = document.getElementById("numAuctionItemTokenId");
const auctionItemPrice = document.getElementById("numAuctionItemPrice");
const auctionItemTime = document.getElementById("numAuctionItemTime");

const auctionItemButton = document.getElementById("btnAuctionItem");
auctionItemButton.onclick = auctionNft;

const buyItemSaleId = document.getElementById("numBuyItem");
const buyItemAmmount = document.getElementById("numBuyItemAmmount");
numBuyItemAmmount;

const buyItemButton = document.getElementById("btnBuyItem");
buyItemButton.onclick = buyNft;

init();
```

 **That's it!**

  Congratulations! You have created your own marketplace and minted as well as listed your first Token in the Marketplace ! If you want to use this functionality and numerous others like timed auction, creating collection, bidding, etc today in your app, check out the [Express SDK](sdk/overview.md) section which gives you a plug and play SDK component for front end.

  ***