DiscoTables
===========

DiscoTables (&lt;tables&gt; via multicast discovery) presents method for automatic OpenBSD pf table updates.

This simplifies two common usecases for your operations team. Both of these tasks can now be completed on ''all'' of your load balancers instantly, without logging in.

# Adding a new server to a load balanced pool is automatic. Depending on your environment, it could be as simple as cloning a VM.
# Removing a server from production for maintenance. 

A DiscoTables server runs on each of your firewalls (because, naturally, you're already running pfsync, carp and maybe even bgpd). Clients such as web servers, message brokers, etc. run clients which announce their presence to the servers. It is assumed that your relayd.conf already knows how to judge the health of your servers. 

Environment
-----------

The discotables server is only intended to work in conjunction with OpenBSD's pfctl, but could in theory be extended to work with other load balancers. The discotables-announce client is tested on Ubuntu, Mac OS X, and OpenBSD.

TODO
----

* Directly support ActiveMQ's announcements. Zero security, but could be useful under the right circumstances.
* Need a way to configure 3rd party scripts for updating other load balancers, such as NginX fair-upstream. 

Dependencies
------------

Ubuntu, Debian:

`apt-get install libcrypt-cbc-perl libcrypt-blowfish-perl libio-socket-multicast-perl`

Everyone else: 

`cpan install Crypt::CBC Crypt::Blowfish IO::Socket::Multicast`

