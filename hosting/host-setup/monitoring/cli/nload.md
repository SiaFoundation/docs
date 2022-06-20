---
description: Monitoring real time bandwidth usage using nload
---

# nload

## Installing nload

```
sudo apt install nload
```



## Using nload

```
nload [options] [devices]
```



### Options

```
-a period       Sets the length in seconds of the time window for average
                calculation.
                Default is 300.
                
-i max_scaling  Specifies the 100% mark in kBit/s of the graph indicating the
                incoming bandwidth usage. Ignored if max_scaling is 0 or the
                switch -m is given.
                Default is 10240.
                
-m              Show multiple devices at a time; no traffic graphs.

-o max_scaling  Same as -i but for the graph indicating the outgoing bandwidth
                usage.
                Default is 10240.
                
-t interval     Determines the refresh interval of the display in milliseconds.
                Default is 500.
                
-u h|b|k|m|g    Sets the type of unit used for the display of traffic numbers.
   H|B|K|M|G    h: auto, b: Bit/s, k: kBit/s, m: MBit/s etc.
                H: auto, B: Byte/s, K: kByte/s, M: MByte/s etc.
                Default is h.
                
-U h|b|k|m|g    Same as -u, but for a total amount of data (without "/s").
   H|B|K|M|G    Default is H.
   
devices         Network devices to use.
                Default is to use all auto-detected devices.
                
--help

-h              Print this help.
```

{% hint style="info" %}
_The options above can also be changed at run time by pressing the 'F2' key._
{% endhint %}



### Examples&#x20;

Monitor bandwidth on device `eth0`:

```
nload eth0
```



Monitor bandwidth on device `eth0`:

* The refresh rate `-t` set to 200 milliseconds,
* max scaling `-i` of incoming bandwidth set to 1024 kBit/s
* Max scaling of outgoing bandwidth `-o` set to 128 kBit/s
* Display size of units `-U` set to MBits/s&#x20;

```
nload -t 200 -i 1024 -o 128 -U M eth0
```



Use `man nload` for complete list of options.
