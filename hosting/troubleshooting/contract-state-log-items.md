# Contract State Log Items

These log items indicate life-cycle events for contracts. A storage contract has 3 life-cycle events: creation, revision, and finalization. Creation occurs when the renter and host agree to create a storage contract and lock allowance and collateral into it. Revision occurs when the renter and host agree to revise the contract through upload, download, or funding an ephemeral account. Finalization occurs when the renter or host submits the final revision to the blockchain, indicating the contract will no longer be updated. After finalization, during the contract's proof window, a host can determine whether a storage proof needs to be submitted. If the host submits a valid storage proof the contract's valid proof outputs are created, otherwise the missed outputs are created. There are situations where it is not in the host's best interest to submit a storage proof, so not submitting a proof does not necessarily indicate failure.

* file contract complete, id
* No need to submit a storage proof for the contract. Revenue is
* Successfully submitted a storage proof. Revenue is
* No need to submit a storage proof the contract. Revenue is
* Missed storage proof. Revenue would have been

## File Contract Log Items

The log lines below can occur when renters and hosts revise the file contract. In most cases these do not indicate an issue with your host.

## The requested file contract is currently locked

To revise a contract it has to be locked, a renter attempted to use a file contract that was already locked. This could indicate failure to unlock a contract after disconnect, but it's more likely an issue from the renter.

## Renter has provided an incorrectly sized sector

The renter tried to upload a sector that did not match the host's sector size \[4MiB]

## Transaction has a file contract with an outdated revision number

Usually, the host submits the last contract revision to the block chain in order to get payed, however the renter can also submit the last revision to ensure the host is penalized if it does not meet its obligation. This occurs if the renter has already submitted the same revision the host is attempting to submit or that the host has an older revision, which under normal circumstances should not be possible. The host may still attempt to submit a proof if they are able.

## Could not find the desired sector

Occurs when a renter requests data that is not available on the host. This has started occurring a lot more since Skynet portals attempt to download data from every host if it does not know which hosts are storing the Skylink. Usually not an issue.

## Storage obligation not found in database

Occurs if the renter tried to use a file contract that the host does not know about.

## Download request has invalid sector bounds

Occurs if the renter tried to request a section of a sector that is greater than the host's sector size \[4MiB]
