# Syncing Log Items

Sync issues can happen in distributed networks, usually just waiting for the next block resolves the issue.

## Wallet has coins spent in incomplete transactions - not enough remaining coins

Occurs when the wallet has spent all of its confirmed outputs, waiting one block for confirmations should resolve the issue.

## Consensus conflict on the origin transaction set, id

Most likely occurs if the host is not fully synced, check your peers and your sync height

## Transaction spends a nonexisting siacoin output

This occurs when the payment for a contract formation or revision has a non-existing siacoin output. Usually a syncing issue, and most likely an issue on the renter side. Should resolve itself in a few blocks if the host is synced to the correct blockchain.

## Siacoin inputs do not equal siacoin outputs for transaction

A valid transaction must spend all of its input value, either through returning change to the wallet or using it for the file contract. This occurs when the payment for a contract formation or revision has more input money then it outputs. Most likely on the renter side, this has started happening more often as people experiment with custom Sia implementations.

## Transaction set is too large for this transaction pool

Occurs when a transaction set is too large to be confirmed on the Sia blockchain. A transaction set must be less than 25000 bytes. This usually occurs when a wallet is extremely fragmented and needs to be defragmented.

## Transaction set contains only duplicate transactions

Occurs when a transaction set has already been broadcast, in full, to the network.
