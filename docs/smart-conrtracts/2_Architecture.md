---

Contracts are built using openzeppelin’s upgradeable smart contracts library. So the smart contract code can be updated to support new features, fix bugs, etc.

Functionalities are divided into different parts and some contracts are inherited by other contracts as well as by openzeppelin’s contracts.

The _TokenFactory_ contract inherits the _NFTBid_ contract which inherits _NFTFactoryContract_ which again inherits the _NFTStorage_ contract.

Similarly in ERC1155 part, The _TokenFactory1155_ contract inherits the _NFTBid1155_ contract which inherits _NFTFactoryContract115_ which again inherits the _NFTStorage1155_ contract.

---
