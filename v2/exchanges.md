---
cover: https://sia.tech/assets/previews/nate-snow.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# How to Upgrade: Exchanges

This guide is for exchanges that are currently using `siad` to track and manage Siacoin deposits. Exchanges should upgrade to `walletd` before the V2 hardfork to continue supporting the Sia network.

`walletd` is the new reference wallet for exchanges. It is designed to be more secure, reliable, and scalable than `siad`. `walletd` also has a more robust API, supports multiple wallets simultaneously, and provides easier support for secure key management setups.

### Differences from `siad`

The most important difference between `siad` and `walletd` is that `walletd` is a watch-only server. That means that it does not store any private keys. This makes `walletd` more secure, but also means that transactions must be signed by an external service with access to the private keys. Either a hardware security device, like a YubiKey, Hashicorp Vault, or an offline signing node. This can be more complex than with `siad`, but it provides significantly more flexibility and security.

Another difference is that `walletd` does not need to rescan the blockchain when adding new addresses to a wallet. This makes managing deposit addresses significantly easier than with `siad`.

`walletd` supports significantly more addresses than `siad` and can handle a much larger number of transactions. This makes it a better choice for exchanges that need to manage a large number of deposit addresses.

`walletd` does not require addresses to be added to wallets before they can be used for addresses. However, there are a few benefits to using addresses that have been added to a wallet.

* The balance of a wallet is the sum of all addresses that have been added to a wallet
* The wallet event list contains transactions for all of its addresses
* `walletd` can construct transactions using UTXOs controlled by all of the addresses in a wallet

### How to run `walletd`

`walletd` can be installed as a standalone binary or as a Docker container. The Docker container is the recommended way to run `walletd` in a production environment. For exchanges, running `wallted` in "Full" index mode. This mode is designed for exchanges and wallet integrators that need to track all addresses and transactions on the Sia network.

```sh
walletd --index.mode=full
```

```yml
services:
  walletd:
    image: ghcr.io/siafoundation/walletd:latest
    command: --index.mode=full
    restart: unless-stopped
```

This will index all transactions on the Sia network, allowing you to track all deposits and withdrawals.

* `[GET] /api/addresses/:address/balance` - Get the balance of the specified address. When running in full index mode, you can use this endpoint to check the balance of any address on the Sia network.
* `[GET] /api/addresses/:address/events` - Get the transactions for the specified address. When running in full index mode, you can use this endpoint to check the balance of any address on the Sia network.

### How to Support V2?

After June 6th, 2025 at block height 526,000 at 06:00 UTC, `siad` will no longer be able to send or receive Siacoins. To continue supporting the Sia network, exchanges must upgrade to `walletd`. In addition to upgrading to `walletd`, exchanges will need to start sending V2 transactions and using the new V2 API endpoints.

#### How to send a V2 transaction

This example uses our Go SDK, but you can also use the `walletd` API directly.

```go
package main

import (
	"go.sia.tech/core/types"
	"go.sia.tech/walletd/api"
	"go.sia.tech/walletd/wallet"
)

const (
	walletdAPIAddress  = "http://localhost:9980/api"
	walletdAPIPassword = "change me"
)

func main() {
	privateKey := types.GeneratePrivateKey() // private key is a standard ed25519 private key

	unlockConditions := types.StandardUnlockConditions(privateKey.PublicKey())
	depositAddress := unlockConditions.UnlockHash()
	recipientAddress := types.VoidAddress
	sendAmount := types.Siacoins(10)

	client := api.NewClient(walletdAPIAddress, walletdAPIPassword)

	w, err := client.AddWallet(api.WalletUpdateRequest{
		Name: "test wallet",
	})
	if err != nil {
		panic(err)
	}

	// create a wallet and add an address
	wc := client.Wallet(w.ID)
	err = wc.AddAddress(wallet.Address{
		Address: depositAddress,
		SpendPolicy: &types.SpendPolicy{
			Type: types.PolicyTypeUnlockConditions(unlockConditions),
		},
	})
	if err != nil {
		panic(err)
	}

	cs, err := client.ConsensusTipState()
	if err != nil {
		panic(err)
	}

	// construct a transaction sending 10 SC to the void address
	resp, err := wc.ConstructV2([]types.SiacoinOutput{
		{Address: recipientAddress, Value: sendAmount},
	}, nil, depositAddress)
	if err != nil {
		panic(err)
	}
	basis := resp.Basis
	txn := resp.Transaction

	// calculate the hash to sign
	sigHash := cs.InputSigHash(txn)

	// sign the transaction
	for i := range txn.SiacoinInputs {
		txn.SiacoinInputs[i].SatisfiedPolicy.Signatures = []types.Signature{privateKey.SignHash(sigHash)}
	}

	// broadcast the transaction
	if err := client.TxpoolBroadcast(basis, nil, []types.V2Transaction{txn}); err != nil {
		panic(err)
	}
}
```

#### How Can I Test?

To test your integration with `walletd`, without risking real Siacoin, you can use one of our two testnets.

* To test V2 transactions, you can use the Anagami testnet. Pass the `--network=anagami` CLI flag to `walletd` to connect to the Anagami testnet.
* To test V1 transactions, you can use the Zen testnet. Pass the `--network=zen` CLI flag to `walletd` to connect to the Zen testnet.

## More questions?

Let us know! Send us an [email](mailto://hello@sia.tech), or [reach out to the community on Discord](https://discord.gg/sia).
