Intent
------

DiscoTables (&lt;tables&gt; via multicast discovery) presents method for automatic OpenBSD pf table updates. The intent is to be used in conjunction with relayd and to facilitate rapid scale-out without changing firewall configuration.

A DiscoTables server runs on each of your firewalls (because, naturally, you're already running pfsync, carp and maybe even bgpd). Clients such as web servers, message brokers, etc. run clients which announce their presence to the servers. It is assumed that your relayd.conf already knows how to judge the health of your servers. 

Dependencies:
------------

`cpan install Crypt::CBC Crypt::Blowfish IO::Socket::Multicast`



