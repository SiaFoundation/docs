---
description: Monitoring your hosts average bandwidth usage using vnstat
---

# vnstat

## Installing vnstat

```
sudo apt install vnstat
```



## Using vnstat

```
vnstat
```



### Options

```
-5,  --fiveminutes [limit]   show 5 minutes
-h,  --hours [limit]         show hours
-hg, --hoursgraph            show hours graph
-d,  --days [limit]          show days
-m,  --months [limit]        show months
-y,  --years [limit]         show years
-t,  --top [limit]           show top days

-b, --begin <date>           set list begin date
-e, --end <date>             set list end date

--oneline [mode]             show simple parsable format
--json [mode] [limit]        show database in json format
--xml [mode] [limit]         show database in xml format

--alert <output> <exit> <type> <condition> <limit> <unit>
                             alert if limit is exceeded

-tr, --traffic [time]        calculate traffic
-l,  --live [mode]           show transfer rate in real time
-i,  --iface <interface>     select interface
```



### Examples

Display daily bandwidth statistics:

```
vnstat -d
```



Display daily bandwidth statistics on device `eth0`

```
vnstat -i eth0 -d
```



Use `--longhelp` or `man vnstat` for complete list of options.
