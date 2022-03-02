---

## Upload NFTs to Pinata Cloud Service:

```javascript
const result = await PandoraSDK.pinata.upload(
  nftImageFile, //File to be uploaded to Pinata
  nftDescription, // Description of the NFT
  pinataApiKey, // Pinata API Key
  pinataSecretApiKey // Pinata Secret API Key
);
```

After uploading the NFT Image successfully, we can get the IPFS link of the image from the response by getting the IPFS Hash.

```javascript
const hash = result.data.IpfsHash;
```

And appending that hash to the following link

```
"<https://gateway.pinata.cloud/ipfs/{hash}>"
```

---

## Upload JSON data to Pinata Cloud Service:

```javascript
const result = await PandoraSDK.pinata.pinJSON(
  pinataAPIKeyJSON, // Pinata API Key
  pinataSecretApiKeyJSON, // Pinata Secret API Key
  pinataJSONData // JSON data to upload
);
```

---
