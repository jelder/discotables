DiscoTables means control of **&lt;tables&gt;** via multicast **disco**very. With DiscoTables, two common workflows can now be completed on *all* of your load balancers instantly, without logging in.

* Adding a new server to a load balanced pool is automatic. Depending on your environment, it could be as simple as cloning a VM.
* Removing a server from production for maintenance, then adding it back after acceptance testing. 

A typical installation involves a server running on each of your load balancers (because, naturally, you're already running pfsync, carp and maybe even bgpd). Back-end servers such as web servers, message brokers, etc. run agents which announce their presence to the load balancers.

More complicated setups may include multiple `discotables` instances per load balancer, each maintaining a distinct set of tables via distinct encryption keys. This provides great isolation (e.g., production from development) and improved security.

It is assumed that your relayd.conf already knows how to judge the health of your servers. This results in a two-way handshake between the load balancers and your back-end servers.

All communication is encrypted with Blowfish and a relies on a pre-shared key. 

Environment
-----------

The `discotables` server is only intended to work in conjunction with OpenBSD's pfctl, but could in theory be extended to work with other load balancers. The `discotables-announce` client is tested on Ubuntu, Mac OS X, and OpenBSD.

TODO
----

* Directly support ActiveMQ's announcements. Zero security, but could be useful under the right circumstances.
* Need a way to configure 3rd party scripts for updating other load balancers, such as NginX fair-upstream. 
* Need to write some --help text.

Dependencies
------------

Ubuntu, Debian:

`apt-get install libcrypt-cbc-perl libcrypt-blowfish-perl libio-socket-multicast-perl`

Everyone else: 

`cpan install Crypt::CBC Crypt::Blowfish IO::Socket::Multicast`

