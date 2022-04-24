---
description: Monitoring your host system using glances.
---

# glances

## Installing glances

```
sudo apt install glances
```



## Using glances

```
glances [options]
```



### Options

```
  -h, --help            show this help message and exit
  
  -V, --version         show program's version number and exit
  
  -d, --debug           enable debug mode
  
  -C CONF_FILE, --config CONF_FILE
                        path to the configuration file
  
  --modules-list, --module-list
                        display modules (plugins & exports) list and exit
  
  --disable-plugin DISABLE_PLUGIN, --disable-plugins DISABLE_PLUGIN
                        disable plugin (comma separed list)
  
  --enable-plugin ENABLE_PLUGIN, --enable-plugins ENABLE_PLUGIN
                        enable plugin (comma separed list)
  
  --disable-process     disable process module
  
  --disable-webui       disable the Web Interface
  
  --light, --enable-light
                        light mode for Curses UI (disable all but top menu)
  
  -0, --disable-irix    task's cpu usage will be divided by the total number
                        of CPUs
  
  -1, --percpu          start Glances in per CPU mode
  
  -2, --disable-left-sidebar
                        disable network, disk I/O, FS and sensors modules
  -3, --disable-quicklook
                        disable quick look module
  
  -4, --full-quicklook  disable all but quick look and load
  
  -5, --disable-top     disable top menu (QL, CPU, MEM, SWAP and LOAD)
  
  -6, --meangpu         start Glances in mean GPU mode
  
  --disable-history     disable stats history
  
  --disable-bold        disable bold mode in the terminal
  
  --disable-bg          disable background colors in the terminal
  
  --enable-irq          enable IRQ module
  
  --enable-process-extended
                        enable extended stats on top process
  
  --sort-processes {cpu_percent,memory_percent,username,cpu_times,io_counters,name}
                        Sort processes by: cpu_percent, memory_percent, 
                                           username, cpu_times, io_counters,
                                           name
  
  --export EXPORT       enable export module (comma separed list)
  
  --export-csv-file EXPORT_CSV_FILE
                        file path for CSV exporter
  
  --export-csv-overwrite
                        overwrite existing CSV file
  
  --export-json-file EXPORT_JSON_FILE
                        file path for JSON exporter
  
  --export-graph-path EXPORT_GRAPH_PATH
                        Folder for Graph exporter
  
  -c CLIENT, --client CLIENT
                        connect to a Glances server by IPv4/IPv6 address or
                        hostname
  
  -s, --server          run Glances in server mode
  
  --browser             start the client browser (list of servers)
  
  --disable-autodiscover
                        disable autodiscover feature
  
  -p PORT, --port PORT  define the client/server TCP port [default: 61209]
  
  -B BIND_ADDRESS, --bind BIND_ADDRESS
                        bind server to the given IPv4/IPv6 address or hostname
  
  --username            define a client/server username
  
  --password            define a client/server password
  
  -u USERNAME_USED      use the given client/server username
  
  --snmp-community SNMP_COMMUNITY
                        SNMP community
  
  --snmp-port SNMP_PORT
                        SNMP port
  
  --snmp-version SNMP_VERSION
                        SNMP version (1, 2c or 3)
  
  --snmp-user SNMP_USER
                        SNMP username (only for SNMPv3)
  
  --snmp-auth SNMP_AUTH
                        SNMP authentication key (only for SNMPv3)
  
  --snmp-force          force SNMP mode
  
  -t TIME, --time TIME  set minumum refresh rate in seconds [default: 2 sec]
  
  -w, --webserver       run Glances in web server mode 
                        (python3-bottle needed, static files not included)
  
  --cached-time CACHED_TIME
                        set the server cache time [default: 1 sec]
  
  --open-web-browser    try to open the Web UI in the default Web browser
  
  -q, --quiet           do not display the curses interface
  
  -f PROCESS_FILTER, --process-filter PROCESS_FILTER
                        set the process filter pattern (regular expression)
  
  --process-short-name  force short name for processes name
  
  --process-long-name   force long name for processes name
  
  --stdout STDOUT       display stats to stdout, one stat per line
                        (comma separated list of plugins/plugins.attribute)
  
  --stdout-csv STDOUT_CSV
                        display stats to stdout, csv format
                        (comma separated list of plugins/plugins.attribute)
  
  --issue               test all plugins and exit
                        (please copy/paste the output if you open an issue)
  
  --api-doc             display fields descriptions
  
  --hide-kernel-threads
                        hide kernel threads in process list
                        (not available on Windows)
  
  -b, --byte            display network rate in byte per second
  
  --diskio-show-ramfs   show RAM Fs in the DiskIO plugin
  
  --diskio-iops         show IO per second in the DiskIO plugin
  
  --fahrenheit          display temperature in Fahrenheit 
                        (default is Celsius)
  
  --fs-free-space       display FS free space instead of used
  
  --sparkline           display sparklines instead of bar in the curses interface
  
  --theme-white         optimize display colors for white background
  
  --disable-check-update
                        disable online Glances version ckeck
  
  --strftime STRFTIME_FORMAT
                        strftime format string for displaying current date
                        in standalone mode
```



### Examples

Monitor local machine (standalone mode):

```
glances
```



Display all Glances modules (plugins and exporters) and exit:

```
glances --module-list
```



Monitor local machine with the Web interface and start RESTful server:

```
glances -w
```



Use `glances --help` or `man glances` for complete list of options.
