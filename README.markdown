DiscoTables means control of **&lt;tables&gt;** via multicast **disco**very. With DiscoTables, two common workflows can now be completed on *all* of your load balancers instantly, without logging in.

* Adding a new server to a load balanced pool is automatic. Depending on your environment, it could be as simple as cloning a VM.
* Removing a server from production for maintenance, then adding it back after acceptance testing. 

A typical installation involves a server running on each of your load balancers (because, naturally, you're already running pfsync, carp and maybe even bgpd). Back-end servers such as web servers, message brokers, etc. run agents which announce their presence to the load balancers.

More complicated setups may include multiple `discotables` instances per load balancer, each maintaining a distinct set of tables via distinct encryption keys. This provides great isolation (e.g., production from development) and improved security.

It is assumed that your relayd.conf already knows how to judge the health of your servers. This results in a two-way handshake between the load balancers and your back-end servers.

All communication is encrypted with Blowfish and a relies on a pre-shared key. 

Environment
-----------

Developed and tested on Ubuntu, Mac OS X, and OpenBSD. Needs a modern Perl and not much else.

Roadmap
------

Before release:

* Current design only works against pfctl tables, not relayd. Final version will work against nginx, relayd, or any thingthing with an include statement in the configuration syntax and a graceful reload method. 

Nice to have:

* Directly support ActiveMQ's announcements. Zero security, but could be useful under the right circumstances.
* Need to write some --help text.

Dependencies
------------

Ubuntu, Debian:

`apt-get install libcrypt-cbc-perl libcrypt-blowfish-perl libio-socket-multicast-perl`

Everyone else: 

`cpan install Crypt::CBC Crypt::Blowfish IO::Socket::Multicast`

