Pandora Protocol consists of a variety of Smart Contracts and Libraries for minting, buying, selling, auctioning, and bidding tokens of ERC721 and ERC1155 standard.

---

### Contracts Overview

Tokens can be created either using Pandora’s public contract _PNDC_ERC721_/_PNDC_ERC1155_ or a collection can be deployed using the _TokenFactory_/_TokenFactory1155_ contract and then tokens can be created inside that collection.

_TokenERC721_/_TokenERC1155_ contract contains boilerplate functions for all the collection contracts that will be deployed.

_NFTFactoryContract_/_NFTFactoryContract1155_ contains functions for selling and buying tokens.

_NFTBid_/_NFTBid1155_ contract contains functions for auction sale and bidding.

_NFTStorage_/_NFTStorage1155_ contract is used as a storage contract for all the sale and collection data.

---

### Libraries Overview

Libraries are used by Smart Contracts to hold useful data in an organized way.

_LibShare_ library contains the royalty share structure.

_LibMeta_/_LibMeta1155_ library contains the sales metadata structure.

_LibCollection_/_LibCollection1155_ library contains the collections metadata structure.

_LibBid_/_LibBid1155_ library contains the bid Order structure.

_LibERC721_/_LibERC1155_ library contains a function to deploy a new ERC721 contract(collection).

---
