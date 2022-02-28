### Procedure to deploy contracts on local as well as public blockchains.

→Clone the Repository [Modular-Contract]("https://github.com/Pandora-Finance/Modular-contract")

→Install the dependencies by running -

```bash
    npm install
```

---

### For deployment on the local network:

→Start truffle development console by running following command in terminal -

```bash
    truffle develop
```

→For compiling and deploying on the local blockchain, run -

```bash
    compile --all
```

```bash
    migrate --reset
```

---

### For deployment on the public test network:

→Create a ‘.env’ file in the root directory and add a private key :

```
    PK = <PRIVATE_KEY>
```

→For compiling and deploying on the public test blockchain, run -

```bash
    truffle compile --all
```

```bash
    truffle migrate --reset --network testnet
```

---
