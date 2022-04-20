***

### Create NFT Auctions using Pandora-express SDK

### Intro

  In this guide we will make NFT marketplace Dapp using Express Protocol SDK through which anyone can Mint NFTs, Auction them and buyers can Bid on tokens.
  We will use Pandora Public ERC721 contract for NFT minting and Pandora Market Contract for Auctioning/Bidding of NFTs.
  You also need to connect a wallet, so make sure you have metamask wallet installed.

  Alright without further ado, let's create our marketplace!

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
  ``` 
  ![Screenshot](/media/pandora-install.png)

  **3.Building the UI**

   Make a index.html file and paste the following code.<br>
   Here we have made five sections for the frontend, first one we have the create item section, in which any user can mint NFT. Then we have auction section in which user can put their NFT on auction, it has three fields, one for token ID, one for setting Base price of NFT and next for time span in which the auction will end.
   <br>
   Then we have next section for user who want to Bid on the auctioned NFT, user have to enter the sale ID and the Bid offer he want to make for the NFT. Next we have execute Bid section through which the NFT owner can accept the bid made by the bidders, we have two fields for the Sale ID and Bid ID.<br>
   Next their is withdraw bid section, by which bidders can withdraw the bid they have made, bidders have to pass the sale ID and Bid ID in the fields present.<br>
   At last their is the cancel sale section, NFT owner can cancel the auction of their NFT. User have to enter only the Sale ID.

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


    <div id="auctionItem">
      <h4>Auction Item</h4>
      <input
        type="number"
        min="1"
        step="1"
        id="numAuctionItemTokenId"
        placeholder="Enter TokenId"
        required
      />
      <input
        type="number"
        min="1"
        step="1"
        id="numAuctionItemPrice"
        placeholder="Enter Auction Price"
        required
      />
      <input
        type="number"
        min="1"
        step="1"
        id="numAuctionItemTime"
        placeholder="Enter Auction Time"
        required
      />

      <button id="btnAuctionItem">Auction Item</button>
    </div>

    <div id="Bid">
      <h4>Bid</h4>
      <input
        type="number"
        id="numBidItemSaleId"
        required
        placeholder="Enter SaleId"
      />
      <input
        type="number"
        id="numBidItemPrice"
        required
        placeholder="Enter Bid Price"
      />

      <button id="btnBidItem">Bid</button>
    </div>

    <div id="executeBid">
      <h4>Execute Bid</h4>
      <input
        type="number"
        id="numExecuteSaleId"
        required
        placeholder="Enter SaleId"
      />
      <input
        type="number"
        id="numExecuteBidId"
        required
        placeholder="Enter BidId"
      />

      <button id="btnExecuteBidItem">Execute Bid</button>
    </div>

    <div id="withdrawBid">
      <h4>Withdraw Bid Money</h4>
      <input
        type="number"
        id="numWithdrawSaleId"
        required
        placeholder="Enter SaleId"
      />
      <input
        type="number"
        id="numWithdrawBidId"
        required
        placeholder="Enter BidId"
      />

      <button id="btnWithdrawBidItem">Withdraw Bid</button>
    </div>

    <div id="withdrawBid">
      <h4>Cancel Item Sale</h4>
      <input
        type="number"
        id="numCancelSaleId"
        required
        placeholder="Enter SaleId"
      />

      <button id="btnCancelItemSale">Cancel Sale</button>
    </div>
     <script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
    <script src="main.js"></script>
  </body>
</html>

```

Now run the app with live server<br>
As we have pasted the code, Now our frontend will look something like this:

![Screenshot](/media/html1.png)


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
  }
 ```

 We have minted a NFT using the SDK now, we can put the NFT in auction using sellNFTByBid function of the SDK.<br>
 Define the auction NFT function that will call the PandoraSDK.erc721.order.sellNFTByBid function.

```javascript
const auctionNft = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.order.sellNFTByBid(
    web3,
    chainId,
    auctionItemTokenId.value,//Token ID
    auctionItemPrice.value,// Base Price of Token
    accounts[0],
    auctionItemTime.value// Time of Auction
  );
}
```

After putting the item on Auction, anyone can Bid on the Token by providing price more than the base price of the Token or price more than the previous highest Bid.<br>
We can implement the Bid function in our App using the PandoraSDK.erc721.order.bid function.

```javascript
const bid = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.order.bid(
    web3,
    chainId,
    BidItemSaleId.value, //Sale ID of Token
    accounts[0],
    BidItemPrice.value // Price offered by the Bidder
  );
};
```

The owner of the Token can accept the Bid that he likes using the PandoraSDK.erc721.order.acceptBid function.<br>
Lets define a function that owner of Token will use to accept the offer.

```javascript
const executeBid = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.order.acceptBid(
    web3,
    chainId,
    ExecuteSaleId.value, //Sale ID of the token on Auction
    ExecuteBidId.value, //Bid ID of the Bid offering
    accounts[0]
  );
};
```

After Auction is over and if the Bidder's bid is not accepted then they can withdraw their bids.<br>
We will use pandoraSDK.erc721.order.withdrawBid() function to implement this.

```javascript
const withdrawBidMoney = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.order.withdrawBid(
    web3,
    chainId,
    WithdrawSaleId.value,
    WithdrawBidId.value,
    accounts[0]
  );
}
```

The Owner of the token can cancel the auction using the pandoraSDK.erc721.order.cancelSale() function.
Lets define the function for our app.

```javascript
const cancelSale = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  console.log(chainId);
  await pandoraSDK.erc721.order.cancelSale(
    web3,
    chainId,
    accounts[0],
    CancelSaleId.value
  );
}
```

**5.Getting Data from User from Frontend**

Now as we defined the functions for our Dapp, the last step is to get the function parameters using javascript DOM.

Paste the code written below to main.js.

```javascript
const itemURI = document.getElementById("txtCreateItemURI");

const createItemButton = document.getElementById("btnCreateItem");
createItemButton.onclick = mintNft;

const itemURI1 = document.getElementById("txtCreateItemURI1");
const itemURI2 = document.getElementById("txtCreateItemURI2");

const auctionItemTokenId = document.getElementById("numAuctionItemTokenId");
const auctionItemPrice = document.getElementById("numAuctionItemPrice");
const auctionItemTime = document.getElementById("numAuctionItemTime");

const auctionItemButton = document.getElementById("btnAuctionItem");
auctionItemButton.onclick = auctionNft;

const BidItemSaleId = document.getElementById("numBidItemSaleId");
const BidItemPrice = document.getElementById("numBidItemPrice");

const BidItemButton = document.getElementById("btnBidItem");
BidItemButton.onclick = bid;

const ExecuteSaleId = document.getElementById("numExecuteSaleId");
const ExecuteBidId = document.getElementById("numExecuteBidId");

const ExecuteBidItemButton = document.getElementById("btnExecuteBidItem");
ExecuteBidItemButton.onclick = executeBid;

const WithdrawSaleId = document.getElementById("numWithdrawSaleId");
const WithdrawBidId = document.getElementById("numWithdrawBidId");

const WithdrawBidItemButton = document.getElementById("btnWithdrawBidItem");
WithdrawBidItemButton.onclick = withdrawBidMoney;

const CancelSaleId = document.getElementById("numCancelSaleId");

const CancelItemSaleButton = document.getElementById("btnCancelItemSale");
CancelItemSaleButton.onclick = cancelSale;

init();

```

Now run in terminal
```bash
npx parcel index.html
```

**All Set!**

  Congratulations! You have created your own NFT trading marketplace and minted as well as listed your first Token in the Marketplace ! If you want to use this functionality and numerous others things like timed auction, creating collection, bidding, etc today in your app, check out the [Express SDK](sdk/overview.md) section which gives you a plug and play SDK component for front end.
***