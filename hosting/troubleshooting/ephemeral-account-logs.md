# Ephemeral Account Logs

Ephemeral accounts are used for quicker interactions between a renter and host. The renter funds an ephemeral account using a file contract, after funding the ephemeral account can be used to transact with the host without needing to update or lock the file contract allowing for high parallelism and better performance.

## Ephemeral account maximum balance exceeded

The renter tried to deposit more money than the host allows, this is normally not a problem as ephemeral accounts can be refilled quickly and easily. There is a `maxephemeralaccountbalance` setting, but the current guidance from the core team is to leave it at the default \[1SC].

## Ephemeral account withdrawals are inactive because the host is not synced

Ephemeral account withdrawals are not available until the consensus and host module are both synced. Usually just need to wait until everything is ready, but may be good to check that you have peers.

## Unknown payment method

The renter tried to use an invalid payment method to fund the ephemeral account, currently ephemeral accounts can only be funded through contracts.

## Ephemeral account withdrawal message expired

Withdrawal requests must be signed and timestamped with an expiration block height. Occurs when the renter has tried to send a withdrawal request after it has expired.

## Ephemeral account deposit cancelled due to a shutdown

Occurs when the host was shutdown in the middle of an ephemeral deposit request

## Ephemeral account withdrawal cancelled due to a shutdown

Occurs when the host was shutdown in the middle of an ephemeral deposit request

## Ephemeral account withdrawal message expires too far into the future

Occurs when the expiration of a withdrawal request is too far into the future \[20 blocks]
