---

```javascript
    struct TokenMeta {
        uint256 saleId;
        address collectionAddress;
        uint256 tokenId;
        uint256 price;
        bool directSale;
        bool bidSale;
        uint256 bidStartTime;
        uint256 bidEndTime;
        address mintedBy;
        address currentOwner;
    }
```

**→saleId**: Id of item on sale

**→collectionAddress**: collection address

**→tokenId**: Id of token

**→price**: selling price/base bidding price

**→directSale**: item on direct sale or not

**→bidSale**: item on bid sale or not

**→bidStartTime**: auction start time

**→bidEndTime**: auction end time

**→mintedBy**: address of minter

**→currentOwner**: address of current owner

---
