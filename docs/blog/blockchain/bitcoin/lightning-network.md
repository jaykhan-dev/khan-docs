---
tags:
  - blockchain
  - bitcoin
  - lightning network
  - lnurl
  - layer 2
  - scaling
  - payments
  - borderless
  - fast
---

# Lightning Network
The Lightning Network is a layer 2 implementation on top of the Bitcoin blockchain to help it scale.  Without this solution, Bitcoin could never really become a world currency since billions of people have mobile phones and the potential to connect to the internet. 

From the [whitepaper](https://lightning.network/lightning-network-paper.pdf)

>A decentralized system is proposed whereby transactions are sent over
a network of micropayment channels (a.k.a. payment channels or
transaction channels) whose transfer of value occurs off-blockchain.

Mobile wallets will be the main medium of interacting and transacting with the Bitcoin blockchain.  My plans for lightning is to use the LNURL-AUTH for authenticating users without a web2 loging such as Google, Facebook, or Linkedin. In my opinion, for a web3 project, there should be a stronger focus on the newer system so that adoption is greater and there is less friction.  If the underlying protocol *just works* then it is better for our financial and psychological health. 

## LNURL

[See article](https://telegra.ph/lnurl-a-protocol-for-seamless-interaction-between-services-and-Lightning-wallets-08-19)

>lnurl is a protocol for communication between Lightning wallets and third-party services. It simplifies complicated common flows into standard subprotocols carried on between the user wallet and the service over simple HTTP JSON calls, leveraging the fact that the third-party services have the luxury of offering an https:// endpoint the user wallet can freely call.

### LNURL-AUTH

### How it works

> 1. The wallet reads a QR code;
> 2. If it has the lnurl prefix it is decoded and the the resulting URL is called;
> 3. From the server response for that URL the wallet knows what subprotocol it should proceed with;
> 4. In the case of lnurl-withdraw, for example, the server response will contain some parameters (min/max, default description) for the invoice that will be generated in the user wallet;
> 5. The wallet proceeds with the subprotocol. In the case of lnurl-withdraw, for example, it will display an invoice generation window prefilled with the parameters returned by the server, and, upon confirmation by the user, send the invoice back to the server, which will pay it.

## Resources
- [Whitepaper](https://lightning.network/lightning-network-paper.pdf)
- [Lightning Labs](https://lightning.engineering/)
- [Jameson Lopp](https://www.lopp.net/lightning-information.html)
- [Umbrel](https://getumbrel.com/)
- [Arcane](https://arcane.no/research)


## Wallets
- [Phoenix](https://phoenix.acinq.co/)
- [Munn](https://muun.com/)
- [Strike](https://strike.me/en/)
- [Blue Wallet](https://bluewallet.io/)
- [Zeus](https://zeusln.app/)
- [Wallet of Satoshi]()