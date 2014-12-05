#lsf-stats
*lsf-stats* displays resource utilization statistics for clusers using IBM's Platform Load Sharing Facility (LSF)  with real-time scattergraphs and historiograms.

These live graphs are viewable in a web-browser. 

This application was built using [plot.ly](https://plot.ly), [node.js](http://nodejs.org/), [python](https://python.org), and the [LSF](https://github.com/PlatformLSF/platform-python-lsf-api) api.

### Install

1) ```make```


2) Open ```web/config.json``` and  replace all the tokens and api keys with your own values.
You will need to create 16 new tokens. 

You can get keys and create tokens here: https://plot.ly/settings/api

### Run

```
./start_server <path_to_static_directory>
```

The html file generated by the above command can be placed on an http server anywhere on the internet. 
You do not need to place it on the same server as lsf-stats or even on the same cluster or subnet.

Data is pushed out to plot.ly's servers.

When a client accesses the webpage, they pull from plot.ly's servers - not yours.

### Prerequisites

*  python 2.6 or 2.7
*  node.js >= 0.10.2x
*  an HPC cluster running lsf
*  cputime "ulimit" of "unlimited" on the node you run this daemon on (otherwise it will die after your time expires...)

### Special Requirements

This needs to be run on a webfacing node.

Errors on startup may be the result of your system not giving you enough resources. 

If you notice you're having trouble forking after running lsf-stats, please run ask your system admin for additional resources on the node you chose to run this service on.

```ulimit -a``` will help you see what your resource limits are.

### Known Issues
*  Graphs randomly fail to render in the web-browser (and produce different types of errors)
*  Initialization connections with the plot.ly api randomly fail (ussually returning a 200 error).

We are working with the plot.ly team to resolve these issues. 
