# Registry Log Errors

These errors are specific to the Skynet registry.

## Registered data is too large

The data stored in a single registry entry can not be more than 113 bytes

## Marshaled entry has wrong size

This occurs when a renter has submitted a registry entry that is not exactly 256 bytes, usually indicating an invalid format.

## Provided revision number is invalid

This occurs when a renter submits an update to a registry entry with a revision number less than the existing entry.

## Provided revision number is already registered

This occurs when a renter submits an update to a registry entry with the same revision number as the existing entry

## Provided signature is invalid

This occurs when a renter submits an update to the registry entry with an invalid signature, indicating someone is trying to update the entry using the wrong key.
