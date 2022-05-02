# Contract Revision Log Items

Both the renter and the host must agree and sign a contract revision for it to be valid, these occur when the renter and the host have a dispute on one of those revisions. They usually occurs if the renter and host are on different block heights.

## Renter is requesting revision after the revision deadline

The renter has tried to revise a contract after it has expired and during the proof period.

## Rejected for bad revision number

Contracts have a revision number that must always increase, occurs when the renter attempted to revise an old version of the contract.

## Rejected for including too few transaction fees

Occurs when the renter provides a transaction that the host does not feel can actually be confirmed on the blockchain due to transaction fees.

## Rejected for low paying host missed output

Occurs when the renter submitted a revision that has the host posting more collateral than it should.

## Rejected for low paying host valid output

Occurs when the renter submits a revision that does not pay the host enough.

## Rejected for high paying renter valid output

This occurs if the renter submits a revision that did not transfer enough money from the renter's allowance.

## Rejected for low value void output

This occurs if the renter submits a revision that does not burn enough allowance if the host fails

## Rejected for bad file size

Occurs when the renter submits a revision with a data size that does not make sense or the data file size was not updated.

## Rejected for having an unexpected number of outputs

Contracts in most situations should have 2 valid proof outputs and 3 missed proof outputs. There are situations where there are only 2 missed proof outputs on a contract. This occurs if the renter submits a revision that does not contain the expected number of outputs.

## Rejected for small window size

This occurs if the contract's proof window is less than the host's minimum window duration \[144 blocks]

## Rejected for a window that starts too soon

This occurs when a renter attempts to create a contract where the proof window starts too soon. The proof window, by default, must be at least 20 blocks away.

## Rejected for bad file merkle root

The merkle root is used to prove that the host correctly stored the data using merkle proofs. This occurs if the renter changed the contract's merkle root during a download revision or gave a different than expected merkle root during an upload revision.

## Renter proposed a file contract with a too-long duration

This occurs if the file contract's duration is longer than the host's max duration. Increasing `maxduration` may reduce the occurrence, but your host is payed at the end of the file contract so may not be ideal.

## File contract proposal expects the host to pay more than the maximum allowed collateral

This occurs when a renter attempts to lock more collateral into a single contract then the host allows. Adjusting `maxcollateral` may reduce the occurrence, but your host may lock more funds into contracts that aren't necessarily going to be used. About 4TB worth of collateral is a good maximum.
