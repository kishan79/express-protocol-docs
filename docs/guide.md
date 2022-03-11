***

### Create NFT Marketplace using Pandora-express SDK
<!-- CREATE NFT MARKETPLACE USING PANDORA-EXPRESS SDK : -->

 Make your own NFT marketplace for trading NFTs.

## Intro

  In this guide we will make NFT marketplace Dapp using Express Protocol SDK through which anyone can mint, buy and sell tokens.
  We will use Pandora Public ERC721 contract for NFT minting and Pandora Market Contract for Buying/Selling NFTs.
  You also need to connect a wallet, so make sure you have metamask wallet installed.

  Alright without further ado, let's create our marketplace!

## Code

1.Create a Project folder.

Create a Javascript file named main.js in your favourite editor. We will use VScode here.


2.SDK installation 
    
Run in terminal

```bash
npm init 
npm i pandora-express 
``` 

3.Using SDK code.

Now we have to import SDK function in our Dapp and make connection with blockchain using metamask.
Paste code below in main.js file.

```javascript
//Import createPandoraExpressSDK from SDK
const { createPandoraExpressSDK } = require("pandora-express");
const pandoraSDK = createPandoraExpressSDK();

//Connecting with Metamask wallet.
init = async () => {
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
mintNft = async () => {
//get current account address
  const accounts = await web3.eth.getAccounts();
//Get ChainID of current account
  const chainId = await web3.eth.net.getId();
//Mint NFT using SDK erc721 nft mint
  await pandoraSDK.erc721.nft.mint(web3, chainId, accounts[0], itemURI, [
    [accounts[0], 100],
  ]);
};
```

We have minted a NFT using the SDK now, we can sell the NFT in the market using Sell function of the SDK.

```javascript
sellNft = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  await pandoraSDK.erc721.order.sellNFT(
    web3,
    chainId,
    sellItemTokenId
    sellItemPrice
    accounts[0]
  );
};
```

We have put an NFT on sale, anyone else can buy the NFT by providing Price more than the sellItemPrice.

You can also try buying the same NFT using different account in your metamask wallet.
Try pasting the code below for buying NFT.

```javascript
buyNft = async () => {
  const accounts = await web3.eth.getAccounts();
  const chainId = await web3.eth.net.getId();
  await pandoraSDK.erc721.order.buyNFT(
    web3,
    chainId,
    buyItemSaleId,
    accounts[0],
    buyItemAmmount
  );
};
```

That's it!

Congratulations! You have created your own marketplace and minted as well as listed your first Token in the Marketplace ! If you want to use this functionality and numerous others like timed auction, creating collection, bidding, etc today in your app, check out the [Express SDK](sdk/overview.md) section which gives you a plug and play SDK component for front end.

***