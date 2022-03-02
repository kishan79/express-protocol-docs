---

```javascript
    struct BidOrder {
        uint256 bidId;
        uint256 saleId;
        address sellerAddress;
        address buyerAddress;
        uint256 price;
        bool withdrawn;
    }
```

**→bidId**: bid Id of item

**→saleId**: Id of item on sale

**→sellerAddress**: address of the current owner

**→buyerAddress**: address of the current bidder

**→price**: current bid price

**→withdrawn**: bid value is withdrawn or not

---
