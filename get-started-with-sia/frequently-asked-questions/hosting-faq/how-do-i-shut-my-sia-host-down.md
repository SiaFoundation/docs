# How do I shut my Sia host down?

To shutdown your host you must first stop accepting contracts. However, this will only stop new contracts from forming - you will still need to complete your current contracts. So if your host is still set to the default contract length of \~26 weeks, that should stop accepting contracts at least 6 months prior to shutting down. Otherwise, you may still have contracts active which you could lose collateral for if you take your host offline before they complete.

To find out how to stop accepting contracts for your host, select your installation type from below:

* [Sia-UI](../../../hosting/hosting-guides/siaui.md#step-6-retire)
* [Linux CLI](../../../hosting/linux-cli.md#step-11-retire)
* [Raspberry Pi](../../../hosting/raspberry-pi.md#step-15-retire-your-host)

Once you've switched off new contracts, you can track the progress of any current contracts by typing `host` into the Terminal `>` at the top of Sia-UI every week or so. Once all collateral is freed (no collateral shows as locked or risked), you can safely take your host offline. You can also use a tool like the [SiaStats Host Monitor](https://siastats.info/hosts) by searching for your host's IP address or domain name. While this service doesn't show contract details, once your host's used storage drops to zero all contracts should be completed.
