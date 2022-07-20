---
tags:
  - bitcoin
  - blockchain
  - smart contracts
  - clarity
  - hello world
  - introduction
---

# Clarity

Clarity is for writing smart contracts on the Bitcoin blockchain. It is a *decideable* language, meaning the behaviour of the contract is predictable from the code itself.  This makes it easier to debug and safer for developers. 

> In the world of smart contracts, everything is a blockchain transaction. 

[Website](https://clarity-lang.org/)

[Tutorials](https://docs.hiro.so/tutorials/clarity-hello-world)

## Hello World

```bash
clarinet new project-name
cd project-name
clarinet contract new hello-world
```

### `hello-world.clar` in the `contracts` folder

```c
(define-public (say-hi) 
  (ok "hello world"))

(define-read-only (echo-number (val int))
  (ok val))
```

### Interacting with the contract

Check to see if there are any errors in the code

```bash
clarinet check
```

Then run the following command:

```bash
clarinet console
```

It is possible to get outputs by using the following commands

#### Return a string

```bash
(contract-call? .hello-world say-hi)
```

This should return `(ok "hello world")`

#### Return a integer

```bash
(contract-call? .hello-world echo-number 42)
```

This should return `(ok 42)`

#### Incorrect type

```bash
(contract-call? .hello-world echo-number u42)
```

You should receive the following error `Analysis error: expecting expression of type 'int', found 'uint'`

## Deploying a smart contract

### The test sandbox

Testing is very important in order to make sure the contract is written correctly and behaves as intended.  This is especially important when dealing with real value in large sums.

[Testnet Sandbox](https://explorer.stacks.co/sandbox/deploy?chain=testnet)

You will have to connect your Hiro Wallet to use the sandbox.

Paste the code in the `hello-world.clar` file into the code editor.  This will bring up the wallet window, click `confirm` and wait for it to be confirmed.  Once it's confirmed, you can interact with the contract further and call the functions which will also be written to the blockchain.



