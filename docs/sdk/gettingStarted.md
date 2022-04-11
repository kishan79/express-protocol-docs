## Installation

SDK is written in Javascript. To use SDK, install it through [npm](https://www.npmjs.com/package/pandora-express)

`npm install pandora-express`

After installation, SDK can be initialized<br>
![](/media/folder.png){: style="height:300px;width:200px"}


In the main.js file, Paste the following code, this will initialize PandoraExpressSDK
```javascript
import { createPandoraExpressSDK } from "pandora-express";
const ExpressSDK = createPandoraExpressSDK();
```

For further usage of SDK with frontend, you can refer to [SDK-Usecases section](../guide.md)

---

## Usage

With Express Protocol SDK, one can:

- Mint ERC721/ERC1155 Token
- Sell/Buy Tokens
- Put Tokens on Auction
- Create/accept bids for auction
- Deploy personal ERC721/ERC1155 contract(Collection)
- Mint, trade, and auction tokens inside Collection

---
