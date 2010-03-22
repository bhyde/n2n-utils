# n2n-utils

A few bash scripts for managing a n2n based VPN.

# Getting started

1. Get you own copy of this by doing:
 git clone git://github.com/bhyde/n2n-utils.git 
2. Get reeady to configure things:
 cp n2n.config-example n2n.config
3. Edit n2n.config, setting the variables toward the top.
4. Start a supernode, and an edge
 ./n2n-supernode-start
 ./n2n-join
5. On each edge node:
  - clone the utils,
  - install your n2n.config file, and
  - start an edge
    ./n2n-join

## Introduction

I run n2n for a community of Macintoshes.  These are the scripts I'm using.  They aren't quite right yet, but they may provide some helpful insights.

Note that you have to set up n2n.config, basing it on n2n.config-example

+ n2n.config
    a file you create from n2n.config-example

+ n2n.config-example
    sketch for the config file.

+ n2n-join -- script to join the community
    Joining the community leads to a new interface appearing on this machine, e.g. tap0,
    with a MAC address that is stable looks like 01:00:00:xx:xx:xx where xx:xx:xx is taken
    from some other MAC address on this machine.  The new interface participates in a
    virtual ethernet implemented by N2N.  Your IP adress on that network is as specified
    in your config file.  Only the most minimal routing is established.  Behind the interface
    a process, known as an edge, is running.

+ n2n-kill-edge
    Shuts down the edge process running on your machine.

+ n2n-manage [<cmd>]
    Sends <cmd> to the UDP port of your edge.  Note that if your running both an
    edge and a super node it's a race who get's this cmd.

+ n2n-status
    Displays various status information about your participation in the community.

+ n2n-all-traffic
    Changes your routing so that the default route for packets is to the gateway
    mentioned in your config file, presumably an IP address in the VPN.  Before
    setting that it creates a specific rule to the supernode, which means, in due
    course all the encrypted packets that support the VPN will flow via the supernode.

+ n2n-no-traffic
    Undoes the routing rules setup by n2n-all-traffic.

+ n2n-supernode-start
    Starts up a supernode.