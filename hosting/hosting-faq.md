# Hosting FAQ

<details>

<summary>Can I run my host on two different computers at the same time?</summary>

It is not recommended to keep the same wallet and installation running in two different computers while hosting, as it could lead to data loss and loss of Siacoins.

</details>

<details>

<summary>What happens if my host computer shuts off?</summary>

Your host will appear as offline. Reference [this article](broken-reference) to reboot it automatically.

</details>

<details>

<summary>Can I change the folder that Sia uses for storage?</summary>

The easiest way to do so is to add the new storage folder in the Host tab, wait for it to show as part of the "Total Storage", and then remove the old storage folder. Sia should move any stored data from the old folder to the new ones once you remove the old one, but this process might take a while depending on the size of the old folder and Sia will be unresponsive during the move.

It may be easier to resize your old storage folders down incrementally after adding the new folder, which will cause Sia to move data from the old folder to the new folder with each resize. If you do this repeatedly in small pieces (e.g. 50 or 100 GB at a time), Sia is less likely to lock up or crash in the process.

</details>

<details>

<summary>Should I backup my Sia host metadata?</summary>

The Sia client maintains additional information on your contracts as a host and your renters' files in an internal location. This information is known as host metadata and is required in order to provide your renters with access to their data on the Sia cloud storage network. Without it, it's like losing renter data - you'd have no way to know which data belongs to who in your host storage folders.

See more about backing up in [Sia-UI hosting guide](broken-reference).

</details>

<details>

<summary>How do I set up port forwarding for TCP ports 9981-9983?</summary>

To set up port forwarding for TCP ports 9981-9983, you'll need to access your firewall or router settings. While we can't provide specific instructions in this guide, you can find tutorials for configuring port forwarding on most routers and firewalls online.

</details>

<details>

<summary>Is the Sia host affected when my public IP address changes, given that it is dynamic?</summary>

You can use a free Dynamic DNS (DDNS) service. DDNS involves registering for and receiving your own address, like "mysiahost.ddns.net", in combination with running a small program or script on your computer. Some routers also have built-in DDNS support for certain providers. When your public IP address changes, the DDNS program detects the change and configures your DDNS address with the new IP. This way, you can announce your Sia host using your DDNS address, and it should stay Online even with public IP changes.

There are a number of free DDNS providers which can be found by searching for DDNS using your favorite search engine. One popular free option is [NoIP.com](https://www.noip.com/).

</details>

<details>

<summary>How do I shut my Sia host down?</summary>

You can stop accepting new contracts by turning off the green slider next to "Announce Host" in the Host tab. However, this only stops new contracts - you still need to finish out current contracts. Default host settings use a \~26-week contract length and renters use a default \~3-month length, so you should switch new contracts off at least 6 months prior to when you'd like to shut down your host. Otherwise, you may still have contracts active which you could lose collateral for if you take your host offline before they complete.

Once you've switched off new contracts, you can track the progress of any current contracts by typing `host` into the Terminal `>` at the top of Sia-UI every week or so. Once all collateral is freed (no collateral shows as locked or risked), you can safely take your host offline. You can also use a tool like the [SiaStats Host Monitor](https://siastats.info/hosts) by searching for your host's IP address or domain name. While this service doesn't show contract details, once your host's used storage drops to zero all contracts should be completed.

</details>

