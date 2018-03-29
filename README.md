# Eclair Wallet
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Gitter chat](https://img.shields.io/badge/chat-on%20gitter-rose.svg)](https://gitter.im/ACINQ/eclair)

The Eclair Wallet is a next generation, Lightning-ready Bitcoin wallet. It can be used as a regular Bitcoin wallet, and can also connect to the Lightning Network for cheap and instant payments.

This software is based upon [Eclair](https://github.com/ACINQ/eclair), and follows the Lightning Network standard.

## Installation

The wallet is available on [Google Play](https://play.google.com/store/apps/details?id=fr.acinq.eclair.wallet).

## Wallet Limitations

- The wallet is still experimental. Bugs, crashes and backward incompatibilities should be expected.

- Lightning channels are outbound only: you can pay with LN but you can not receive or forward payments with this wallet. For the complete LN experience, run a full [Eclair Node](https://github.com/ACINQ/eclair).

## Usage with Lightning

### Opening a LN channel

1. Make sur you have funds (swipe to the left from the home screen to display your address and receive funds).

   You can get Testnet bitcoins from [this faucet](https://testnet.manu.backend.hamburg/faucet).

2. Swipe to the right from the home screen, and click on the green `+` button
3. You can now choose to scan/paste the adress of a Lightning Node.

   Alternatively, choose `Autoconnect` to initiate a connection with one of our nodes.

4. Enter the capacity of the channel and click `Open`.

   A transaction will be sent to fund the channel. You can find it in the transactions list as an outbound Bitcoin transaction, with an amount corresponding to the channel's desired capacity.
   At this point the channel will have a `WAIT_FOR_CONFIRMED` state and can not be used yet.

5. Once the channel reaches the `NORMAL` state (the funding transaction has 2+ confirmations) you can send payments!

### Sending a LN payment

1. Make sure you have at least one channel in a `NORMAL` state with enough balance.
2. In the Transaction view, click the Send button.

   You can now scan or paste a Lightning Payment request. This is an invoice generated by a node in the network, and which contains the necessary informations required to execute a LN payment.
   We have set up [Starblocks](https://starblocks.acinq.co), a virtual coffee shop for testers. You can use it to generate LN payment requests.

3. A window will open to display the informations about the payments. Click `Send Payment`.

   The wallet will now find a route from your node to the destination node. Depending on the topology of the network and the amount of hops needed to reach the destination node, you will pays fees. For now, this wallet does not enable you to limit the fees.
   Once a valid route is found, the balance of one of your channels will be updated.

   If no route can be found, the payment fails and your channels are unchanged. The reasons can be multiple:
   - the destination node is not online;
   - none of your channels has enough funds;
   - the nodes between you and the destination node do not have channels with sufficient capacity to relay your payment;
   - ...

### Closing a channel

1. In the LN channels list, click on the channel you want to close.
2. Click on the `Close channel` button

   If the channel is not in a `NORMAL` state, the closing will be uncooperative. It means that you will have to wait for 144 blocks to receive your funds. This is a Lightning Network specification to prevent theft.

3. You will receive a Bitcoin transaction with the leftover balance of the channel.

## Developers

1. clone this project
2. clone [Eclair](https://github.com/ACINQ/eclair) and checkout the `wip-android` branch.

   Follow the steps [here](https://github.com/ACINQ/eclair/blob/wip-android/BUILD.md) to build the project. This is a required dependency for the wallet.

3. Open the Eclair Wallet project with Android studio. You should now be able to install it on your phone/on an emulator.
