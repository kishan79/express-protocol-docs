---

```javascript
    struct BidOrder {
        uint256 saleId;
        uint256 numberOfTokens;
        address sellerAddress;
        address buyerAddress;
        uint256 price;
        bool withdrawn;
    }
```

**→saleId**: Id of item on sale

**→numberOfTokens**: Amount of Tokens

**→sellerAddress**: address of the current owner

**→buyerAddress**: address of the current bidder

**→price**: current bid price

**→withdrawn**: bid value is withdrawn or not

---
