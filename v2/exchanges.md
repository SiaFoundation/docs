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

{% hint style="info" %}
The hardfork activates on June 6th, 2025 at a block height of **526,000 at 06:00 UTC**.
{% endhint %}

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

`walletd` can be installed as a standalone binary or as a Docker container. The Docker container is the recommended way to run `walletd` in a production environment. For exchanges, we recommend running `walletd` in "full" index mode. This mode is designed for exchanges and wallet integrators that need to track all addresses and transactions on the Sia network.

It is also possible to disable HTTP authentication on endpoints that are safe to expose to the public using the `--http.public` flag.

```sh
walletd --index.mode=full --http.public
```

```yml
services:
  walletd:
    image: ghcr.io/siafoundation/walletd:latest
    command: --index.mode=full --http.public
    restart: unless-stopped
```

## Wallets

`walletd` supports multiple wallets. Each wallet has its own set of addresses and transactions. Wallets can be created and updated using the `wallets` API. When running in "full" index mode, it is not required to group addresses into wallets. However, it is recommended to do so for easier indexing.

### Creating a wallet

```sh
curl -u :"sia is cool" "http://localhost:9980/api/wallets" -X POST -d '{"name":"exchange"}'
```

```json
{
        "id": "1",
        "name": "exchange",
        "description": "",
        "dateCreated": "2025-02-07T11:02:51-08:00",
        "lastUpdated": "2025-02-07T11:02:51-08:00",
        "metadata": null
}
```

### Adding an address to a wallet

To add an address to a wallet, you can use the `[PUT] /api/wallets/:id/addresses` endpoint. When an address is added in "full" index mode, the wallet is immediately updated without needing to rescan the chain. The spend policy is used to track the address' unlock conditions. It can be ignored for addresses where the unlock conditions are not known. If the address is already in the wallet, its metadata will be updated.

```sh
curl -u :"sia is cool" "http://localhost:9980/api/wallets/1/addresses" -X PUT -d '{"address":"3dbc6e05dfe9db593dd4796a9522b5df435e9fc45ec9b90b6f2ae5d2d18550b6bd8db06bc824","spendPolicy":{"type":"uc","policy":{"timelock":0,"publicKeys":["ed25519:0d49fba38e80a888f847cb9661fd91f97cfba1e355ddeb15de2b8dd9a4b58614"],"signaturesRequired":1}}}'
```

If successful, the body will be empty and a `204` response code will be returned.

### Getting the balance of a wallet

To get the balance of a wallet, you can use the `[GET] /api/wallets/:id/balance` endpoint. This endpoint will return the balance of the specified wallet.

```sh
curl -u :"sia is cool" "http://localhost:9980/api/wallets/1/balance"
```

```json
{
        "siacoins": "0",
        "immatureSiacoins": "0",
        "siafunds": 0
}
```

### Getting the events of a wallet

To get the events of a wallet, you can use the `[GET] /api/wallets/:id/events` endpoint. This endpoint will return a paginated list of events for the specified wallet. You can use this event list to track deposits and other changes from the wallet. The pagination can be controlled with the `offset` and `limit` query parameters. It defaults to `0` and `50`, respectively.

```sh
curl -u :"sia is cool" "http://localhost:9980/api/wallets/1/events
```

```json
[
        {
                "id": "268ef8627241b3eb505cea69b21379c4b91c21dfc4b3f3f58c66316249058cfd",
                "index": {
                        "height": 0,
                        "id": "e23d2ee56fc5c79618ead2f8f36c1b72c6f3ec5e0f751c05e08bd6665a6ec22a"
                },
                "confirmations": 45791,
                "type": "v1Transaction",
                "data": {
                        "transaction": {
                                "id": "268ef8627241b3eb505cea69b21379c4b91c21dfc4b3f3f58c66316249058cfd",
                                "siacoinOutputs": [
                                        {
                                                "value": "1000000000000000000000000000000000000",
                                                "address": "3d7f707d05f2e0ec7ccc9220ed7c8af3bc560fbee84d068c2cc28151d617899e1ee8bc069946"
                                        }
                                ],
                                "siafundOutputs": [
                                        {
                                                "value": 10000,
                                                "address": "053b2def3cbdd078c19d62ce2b4f0b1a3c5e0ffbeeff01280efb1f8969b2f5bb4fdc680f0807"
                                        }
                                ]
                        }
                },
                "maturityHeight": 0,
                "timestamp": "2023-01-13T08:53:20Z",
                "relevant": [
                        "053b2def3cbdd078c19d62ce2b4f0b1a3c5e0ffbeeff01280efb1f8969b2f5bb4fdc680f0807"
                ]
        }
]
```

### Sending Transactions

When using wallets, you can construct transactions using the construct API. This API will return a transaction that must be signed before it can be broadcast to the network. You can sign transactions using a hardware security device, like a YubiKey, Hashicorp Vault, or another offline signing node. This can be more complex than with `siad`, but it provides significantly more flexibility and security.

The example is provided in Go, but the same process can be done in any language that supports ed25519 signing.

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
	resp, err := wc.Construct([]types.SiacoinOutput{
		{Address: recipientAddress, Value: sendAmount},
	}, nil, depositAddress)
	if err != nil {
		panic(err)
	}

	basis := resp.Basis
	txn := resp.Transaction

	for i, sig := range txn.Signatures {
		// calculate the sig hash
		sigHash := cs.WholeSigHash(txn, sig.ParentID, 0, 0, nil)
		// sign the hash
		sig := privateKey.SignHash(sigHash)
		// add the signature to the transaction
		txn.Signatures[i].Signature = sig[:]
	}

	// broadcast the transaction
	if err := client.TxpoolBroadcast(basis, []types.Transaction{txn}, nil); err != nil {
		panic(err)
	}
}
```

## Addresses

In "full" index mode, `walletd` will automatically index all addresses on the Sia network. This means that you can query any address on the Sia network without needing to add it to a wallet. However, it is recommended to add addresses to a wallet for easier management.

### Getting the balance of an address

To get the balance of an address, you can use the `[GET] /api/addresses/:address/balance` endpoint. This endpoint will return the balance of the specified address. When in full index mode, you can use this endpoint to check the balance of any address on the Sia network.

```sh
curl "http://localhost:9980/api/addresses/053b2def3cbdd078c19d62ce2b4f0b1a3c5e0ffbeeff01280efb1f8969b2f5bb4fdc680f0807/balance"
```

```json
{
        "siacoins": "2102400000000000000000000000000000",
        "immatureSiacoins": "0",
        "siafunds": 10000
}
```

### Getting UTXOs of an address

To get the UTXOs of an address, you can use the `[GET] /api/addresses/:address/outputs/siacoin` endpoint. This endpoint will return a paginated list of UTXOs controlled by the address. By default, 50 UTXOs will be returned. When in full index mode, you can use this endpoint to get the UTXOs of any address on the Sia network.

The returned `basis` field should be used when broadcasting a transaction using `[POST] /api/txpool/broadcast`.

```sh
curl http://localhost:9980/api/addresses/053b2def3cbdd078c19d62ce2b4f0b1a3c5e0ffbeeff01280efb1f8969b2f5bb4fdc680f0807/outputs/siacoin
```

```json
{
        "basis": {
                "height": 36160,
                "id": "00000000a23eea639f23280271ee4ca6d0c0d377203836b23f8d71b23f6b2e11"
        },
        "outputs": [
                {
                        "id": "c4ea841fd65d568800f0570f9884b89ce5a32522550567825d9a37586b71ddbf",
                        "stateElement": {
                                "leafIndex": 62,
                                "merkleProof": [
                                        "4a4efb6bcd0c72f9184919d37cf82a3bba8437e839729862f3e950f67dd6abc4",
                                        "7c41069f30e59762a25f50f592b1e055c671e5a491d86dba890d261c50fa882d",
                                        "2394d769cda0c493a9c11ff91575b2b69bde3ff82098b96d0b28fa05879fa15b",
                                        "e44f7f72902cea0a6c0c1502bcdeb8e20b3d096a8483b484f7f1a50b6c4ce172",
                                        "2f19474ba8ced8878c7bad3667dfb360eae2eebdec12e9331ce4949316bbdaf1",
                                        "fb2bb42a2eb46429404181c66ed47d98d3cc14de0277646a3dc97d7b1bbde520",
                                        "c2ec74ea3fbe05b61627c7991ff218618169d291324cb3e94239a75a3f08b8c8",
                                        "d712efa3e01cb26bb3ec7b6695b67d4b6c6d9c4f56d2e5b13e1da5268135db43",
                                        "50fcc5496c329090ff1752d294eb1e5a7627adb932f1a203585ab0c3826cd463",
                                        "504400a021f71285e05ce053ea50fe728cc03536df530a2a7b8edf9bb36623d7",
                                        "49b6d947606ffc9c7ff32ae4ecfd2f8c79243bf6038bd02a3acb8694900a171b",
                                        "83d3a112a3da3227e7249be6cd00bf60109d47a521ee0483b426d937fd22bdbc",
                                        "969707c956e18368593a38995033cb1849e5e2ff7bb1aac7b595b3662b5cac1e",
                                        "3fa743ce013f5e0086d6eb48e089caa02b0ff11bd79e142cc612ae9d018b5863",
                                        "d59fda9e08a521c6db35b6f60cc78b1d304834b781e1bbfb5b7955d5daea75aa",
                                        "42614f598bc8698783f619c5e07ec00b46017015d99a5f94b14c9e38e29adcc8"
                                ]
                        },
                        "siacoinOutput": {
                                "value": "1576800000000000000000000000000000",
                                "address": "053b2def3cbdd078c19d62ce2b4f0b1a3c5e0ffbeeff01280efb1f8969b2f5bb4fdc680f0807"
                        },
                        "maturityHeight": 174
                }
        ]
}
```

### Scanning for deposits

`walletd` has an endpoint designed to make scanning the blockchain for deposits simpler. `[GET] /api/consensus/updates/:index` will return 10 blocks after the specified index. This endpoint is designed to be polled by exchanges that do not use `wallets` to track new deposits. `index` is the chain index of the last block that has been processed. The updates will also handle reverted blocks in the path. When a changeset is processed, `index` should be updated to the last block processed to process the next batch of blocks.

The block data, the spent UTXOs, and the height are all included in the response. This data can be used to update the exchange's internal database with new deposits from relevant addresses.

```sh
curl http://localhost:9980/api/consensus/updates/0::0000000000000000000000000000000000000000000000000000000000000000
```

```json
{
	"applied": [
		{
			"update": {
				"siacoinElements": [
					{
						"siacoinElement": {
							"id": "35b81e41f594d7faeb88bd8eaac2eaa68ce99fe1c8fe5f0cba8fafa65ab3a70e",
							"stateElement": {
								"leafIndex": 0,
								"merkleProof": [
									"88052fa2d1e22e4a5542fed9686cdad3fbeccbc60d15d4fd36a7691d61add1e1"
								]
							},
							"siacoinOutput": {
								"value": "1000000000000000000000000000000000000",
								"address": "3d7f707d05f2e0ec7ccc9220ed7c8af3bc560fbee84d068c2cc28151d617899e1ee8bc069946"
							},
							"maturityHeight": 0
						},
						"created": true,
						"spent": false
					}
				],
				"siafundElementDiffs": [
					{
						"siafundElement": {
							"id": "69ad26a0fbd1a6985d2053246650bb3ba5f3491d818748b6c8562db1ddb2c45b",
							"stateElement": {
								"leafIndex": 1,
								"merkleProof": [
									"837482a39d5bf66f07bae3b89191e4375b82c9f341ce6a17e22e14e0333ab9f6"
								]
							},
							"siafundOutput": {
								"value": 10000,
								"address": "053b2def3cbdd078c19d62ce2b4f0b1a3c5e0ffbeeff01280efb1f8969b2f5bb4fdc680f0807"
							},
							"claimStart": "0"
						},
						"created": true,
						"spent": false
					}
				],
				"fileContractElementDiffs": null,
				"v2FileContractElementDiffs": null,
				"attestationElements": null,
				"chainIndexElement": {
					"id": "e23d2ee56fc5c79618ead2f8f36c1b72c6f3ec5e0f751c05e08bd6665a6ec22a",
					"stateElement": {
						"leafIndex": 2
					},
					"chainIndex": {
						"height": 0,
						"id": "e23d2ee56fc5c79618ead2f8f36c1b72c6f3ec5e0f751c05e08bd6665a6ec22a"
					}
				},
				"updatedLeaves": {},
				"treeGrowth": {},
				"oldNumLeaves": 0,
				"numLeaves": 3
			},
			"state": {
				"index": {
					"height": 0,
					"id": "e23d2ee56fc5c79618ead2f8f36c1b72c6f3ec5e0f751c05e08bd6665a6ec22a"
				},
				"prevTimestamps": [
					"2023-01-13T00:53:20-08:00",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z"
				],
				"depth": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
				"childTarget": "0000000100000000000000000000000000000000000000000000000000000000",
				"siafundTaxRevenue": "0",
				"oakTime": 0,
				"oakTarget": "00000000ffffffff00000000ffffffff00000000ffffffff00000000ffffffff",
				"foundationSubsidyAddress": "053b2def3cbdd078c19d62ce2b4f0b1a3c5e0ffbeeff01280efb1f8969b2f5bb4fdc680f0807",
				"foundationManagementAddress": "000000000000000000000000000000000000000000000000000000000000000089eb0d6a8a69",
				"totalWork": "1",
				"difficulty": "4294967295",
				"oakWork": "4294967297",
				"elements": {
					"numLeaves": 3,
					"trees": [
						"e1c3af98d77463b767d973f8a563947d949d06428ff145db30143a2811d10014",
						"134b1f08aec0c7fbc50203a514277d197947e3da3ab1854749bf093b56402912"
					]
				},
				"attestations": 0
			},
			"block": {
				"parentID": "0000000000000000000000000000000000000000000000000000000000000000",
				"nonce": 0,
				"timestamp": "2023-01-13T00:53:20-08:00",
				"minerPayouts": [],
				"transactions": [
					{
						"id": "268ef8627241b3eb505cea69b21379c4b91c21dfc4b3f3f58c66316249058cfd",
						"siacoinOutputs": [
							{
								"value": "1000000000000000000000000000000000000",
								"address": "3d7f707d05f2e0ec7ccc9220ed7c8af3bc560fbee84d068c2cc28151d617899e1ee8bc069946"
							}
						],
						"siafundOutputs": [
							{
								"value": 10000,
								"address": "053b2def3cbdd078c19d62ce2b4f0b1a3c5e0ffbeeff01280efb1f8969b2f5bb4fdc680f0807"
							}
						]
					}
				]
			}
		},
		{
			"update": {
				"siacoinElements": [
					{
						"siacoinElement": {
							"id": "ca02d6807c92f61af94e626604615fbcdb471f38fcd8f3add6c6e6e0485ce090",
							"stateElement": {
								"leafIndex": 3,
								"merkleProof": [
									"e1c3af98d77463b767d973f8a563947d949d06428ff145db30143a2811d10014",
									"134b1f08aec0c7fbc50203a514277d197947e3da3ab1854749bf093b56402912"
								]
							},
							"siacoinOutput": {
								"value": "300000000000000000000000000000",
								"address": "c5e1ca930f193cfe4c72eaed8d3bbae627f67d6c8e32c406fe692b1c00b554f4731fddf2c752"
							},
							"maturityHeight": 145
						},
						"created": true,
						"spent": false
					}
				],
				"siafundElementDiffs": null,
				"fileContractElementDiffs": null,
				"v2FileContractElementDiffs": null,
				"attestationElements": null,
				"chainIndexElement": {
					"id": "0000000028e731f0bb5d48662283bec83cca9427581b948d1036deb2b42c3006",
					"stateElement": {
						"leafIndex": 4
					},
					"chainIndex": {
						"height": 1,
						"id": "0000000028e731f0bb5d48662283bec83cca9427581b948d1036deb2b42c3006"
					}
				},
				"updatedLeaves": {},
				"treeGrowth": {
					"0": [
						"190d98a7d8ff464e57f89dc916b155455ecf927f4c74b9edf5e80c103f052bfa",
						"134b1f08aec0c7fbc50203a514277d197947e3da3ab1854749bf093b56402912"
					],
					"1": [
						"2b082bec52801c1e61e5b0d0c1f5fc3925bd24e16d2f490afeb70374828586f1"
					]
				},
				"oldNumLeaves": 3,
				"numLeaves": 5
			},
			"state": {
				"index": {
					"height": 1,
					"id": "0000000028e731f0bb5d48662283bec83cca9427581b948d1036deb2b42c3006"
				},
				"prevTimestamps": [
					"2023-01-13T08:18:19-08:00",
					"2023-01-13T00:53:20-08:00",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z",
					"0001-01-01T00:00:00Z"
				],
				"depth": "00000000ffffffff00000000ffffffff00000000ffffffff00000000ffffffff",
				"childTarget": "0000000100000000000000000000000000000000000000000000000000000000",
				"siafundTaxRevenue": "0",
				"oakTime": 26699000000000,
				"oakTarget": "000000008052201448053c59f99803e7a8165929036cd574d91425423191387c",
				"foundationSubsidyAddress": "053b2def3cbdd078c19d62ce2b4f0b1a3c5e0ffbeeff01280efb1f8969b2f5bb4fdc680f0807",
				"foundationManagementAddress": "000000000000000000000000000000000000000000000000000000000000000089eb0d6a8a69",
				"totalWork": "4294967297",
				"difficulty": "4294967295",
				"oakWork": "8568459756",
				"elements": {
					"numLeaves": 5,
					"trees": [
						"589fb425faa23be357492394813dc575505899d42d0b23a7162e1c68f7eeb227",
						"750cc671d80aef6ee5c73344ba4e74eccda77d9f0cf51ed6237952b1d84bc336"
					]
				},
				"attestations": 0
			},
			"block": {
				"parentID": "e23d2ee56fc5c79618ead2f8f36c1b72c6f3ec5e0f751c05e08bd6665a6ec22a",
				"nonce": 10689346,
				"timestamp": "2023-01-13T08:18:19-08:00",
				"minerPayouts": [
					{
						"value": "300000000000000000000000000000",
						"address": "c5e1ca930f193cfe4c72eaed8d3bbae627f67d6c8e32c406fe692b1c00b554f4731fddf2c752"
					}
				],
				"transactions": [
					{
						"id": "1148417ad8fa6546646da6922618358210bc7a668ef7cb25f6a8a3605851bc7b",
						"arbitraryData": [
							"Tm9uU2lhAAAAAAAAAAAAAClvJjNhfcbxtEfP2yfbBM4="
						]
					}
				]
			}
		}
	],
	"reverted": null
}
```

## Sending Transactions

If you do not want to use a wallet to construct a transaction, you can manually select UTXOs and build the transaction yourself. This is more complex than using a wallet, but it provides more control over the transaction construction process. It is required to use this method if you are using multi-sig addresses.

```go
package main

import (
	"go.sia.tech/core/types"
	"go.sia.tech/walletd/api"
)

const (
	walletdAPIAddress  = "http://localhost:9980/api"
	walletdAPIPassword = "change me"
)

func main() {
	const txnSizeBytes = 1200

	privateKey := types.GeneratePrivateKey() // private key is a standard ed25519 private key

	unlockConditions := types.StandardUnlockConditions(privateKey.PublicKey())
	depositAddress := unlockConditions.UnlockHash()
	recipientAddress := types.VoidAddress
	sendAmount := types.Siacoins(10)

	client := api.NewClient(walletdAPIAddress, walletdAPIPassword)

	utxos, basis, err := client.AddressSiacoinOutputs(depositAddress, 0, 10)
	if err != nil {
		panic(err)
	}

	fee, err := client.TxpoolFee()
	if err != nil {
		panic(err)
	}
	minerFee := fee.Mul64(txnSizeBytes)

	txn := types.Transaction{
		MinerFees: []types.Currency{minerFee},
		SiacoinOutputs: []types.SiacoinOutput{
			{Address: recipientAddress, Value: sendAmount},
		},
	}

	// construct a transaction sending 10 SC to the recipient
	outputSum := sendAmount.Add(minerFee)
	var inputSum types.Currency
	for _, utxo := range utxos {
		if inputSum.Cmp(outputSum) >= 0 {
			break
		}

		inputSum = inputSum.Add(utxo.SiacoinOutput.Value)
		txn.SiacoinInputs = append(txn.SiacoinInputs, types.SiacoinInput{
			ParentID:         utxo.ID,
			UnlockConditions: unlockConditions,
		})
		txn.Signatures = append(txn.Signatures, types.TransactionSignature{
			ParentID:       types.Hash256(utxo.ID),
			PublicKeyIndex: 0,
			Timelock:       0,
			CoveredFields:  types.CoveredFields{WholeTransaction: true},
		})
	}

	if inputSum.Cmp(outputSum) < 0 {
		panic("insufficient funds")
	} else if change := inputSum.Sub(outputSum); !change.IsZero() {
		txn.SiacoinOutputs = append(txn.SiacoinOutputs, types.SiacoinOutput{
			Address: depositAddress,
			Value:   change,
		})
	}

	cs, err := client.ConsensusTipState()
	if err != nil {
		panic(err)
	}

	for i, sig := range txn.Signatures {
		// calculate the sig hash
		sigHash := cs.WholeSigHash(txn, sig.ParentID, 0, 0, nil)
		// sign the hash
		sig := privateKey.SignHash(sigHash)
		// add the signature to the transaction
		txn.Signatures[i].Signature = sig[:]
	}

	// broadcast the transaction
	if err := client.TxpoolBroadcast(basis, []types.Transaction{txn}, nil); err != nil {
		panic(err)
	}
}
```

### How to Support V2?

After June 6th, 2025 at block height 526,000 at 06:00 UTC, `siad` will no longer be able to send or receive Siacoins. To continue supporting the Sia network, exchanges must upgrade to `walletd`. In addition to upgrading to `walletd`, exchanges will need to start sending V2 transactions and using the new V2 API endpoints.

### Sending V2 transactions

This example uses our Go SDK, but you can also use the `walletd` API directly. It is not required to create a wallet to send transactions, but it does simplify transaction creation.

#### Changes from V1

* The miner fee is no longer an array of `Currency` but a single `Currency` value.
* There is a slightly different structure to siacoin inputs
* The input signature has moved to the siacoin input instead of in a separate signatures array.
* The sig hash is calculated using the `InputSigHash` method on the consensus state instead of `WholeSigHash` or `PartialSigHash`.

#### With a wallet

When using a wallet, there are two primary changes to make. The first, is to use `[POST] /api/wallets/:id/construct/v2/transaction` instead of `[POST] /api/wallets/:id/construct/transaction`.

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

#### Without a wallet

```go
package main

import (
	"go.sia.tech/core/types"
	"go.sia.tech/walletd/api"
)

const (
	walletdAPIAddress  = "http://localhost:9980/api"
	walletdAPIPassword = "change me"
)

func main() {
	const txnSizeBytes = 1200
	privateKey := types.GeneratePrivateKey() // private key is a standard ed25519 private key

	unlockConditions := types.SpendPolicy{Type: types.PolicyTypeUnlockConditions(types.StandardUnlockConditions(privateKey.PublicKey()))}
	depositAddress := unlockConditions.Address()
	recipientAddress := types.VoidAddress
	sendAmount := types.Siacoins(10)

	client := api.NewClient(walletdAPIAddress, walletdAPIPassword)
	utxos, basis, err := client.AddressSiacoinOutputs(depositAddress, 0, 10)
	if err != nil {
		panic(err)
	}

	fee, err := client.TxpoolFee()
	if err != nil {
		panic(err)
	}
	minerFee := fee.Mul64(txnSizeBytes)

	txn := types.V2Transaction{
		MinerFee: minerFee,
		SiacoinOutputs: []types.SiacoinOutput{
			{Address: recipientAddress, Value: sendAmount},
		},
	}

	// construct a transaction sending 10 SC to the recipient
	outputSum := sendAmount.Add(minerFee)
	var inputSum types.Currency
	for _, utxo := range utxos {
		if inputSum.Cmp(outputSum) >= 0 {
			break
		}

		inputSum = inputSum.Add(utxo.SiacoinOutput.Value)
		txn.SiacoinInputs = append(txn.SiacoinInputs, types.V2SiacoinInput{
			Parent: utxo,
			SatisfiedPolicy: types.SatisfiedPolicy{
				Policy: unlockConditions,
			},
		})
	}

	if inputSum.Cmp(outputSum) < 0 {
		panic("insufficient funds")
	} else if change := inputSum.Sub(outputSum); !change.IsZero() {
		txn.SiacoinOutputs = append(txn.SiacoinOutputs, types.SiacoinOutput{
			Address: depositAddress,
			Value:   change,
		})
	}

	cs, err := client.ConsensusTipState()
	if err != nil {
		panic(err)
	}

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

### How Can I Test?

To test your integration with `walletd` without risking real Siacoin, you can use one of our two testnets.

* To test V2 transactions, you can use the Anagami testnet. Pass the `--network=anagami` CLI flag to `walletd` to connect to the Anagami testnet.
* To test V1 transactions, you can use the Zen testnet. Pass the `--network=zen` CLI flag to `walletd` to connect to the Zen testnet.

## More questions?

Let us know!

* Send us an [email](mailto://hello@sia.tech)
* [Reach out to the community on Discord](https://discord.gg/sia)
* [Open an Issue](https://github.com/SiaFoundation/walletd)
