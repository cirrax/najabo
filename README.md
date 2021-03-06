najabod
=======

About
-----

najabod is a Nagios Jabber Bot. najabod connects to a XMPP server as a
XMPP client. It reads the nagios status log and shows an overview of the
current states of the monitored nodes. Further version will allow you
to query detailed informations, acknowledge problems and schedule
downtimes etc.

The current version has no ACL and did not support precense
subscription, yet. You will need to do the presence subscription with
your favorite XMPP client or use a XMPP server with shared roster
support like ejabberd.


Status flags
------------

- `D` - host/service is down
- `C` - host/service is critical
- `W` - host/service is warning
- `F` - host/service state is flapping


Interactive commands
--------------------

User commands:

- `lh [host]`
    list hosts

- `hd <host>`
    host details

- `ls [host] [service]`
    list services

- `sd <host> <service>`
    service details

- `lp`
    list problems

- `help`
    show command list


Admin commands:

- `ack <host[/service]> <comment>`
    acknowledge problem

- `dt <host[/service]> <start> <end> <duration> <comment>`
    schedule downtime


Implemented XEPs
----------------

najabod has the following XEPs implemented:

- XEP-0012: Last Activity
- XEP-0030: Service Discovery
- XEP-0054: vcard-temp
- XEP-0092: Software Version
- XEP-0199: XMPP Ping
- XEP-0202: Entity Time


SRV lookup support in Net::XMPP
-------------------------------

Net::XMPP did not support SRV records to get the XMPP server of the
users JID. XMPP requires the client to lookup the server by SRV records
in the DNS. See also the following bug reports including a fix:

- http://rt.cpan.org/Public/Bug/Display.html?id=18539#txn-249050
- http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=325658

To get SRV lookup work, you must have at least

- Net::XMPP >= 1.02_02
- XML::Stream >= 1.23_04

installed and enable the following lines in your najabo.conf:

```perl
$xmpp_conf{'componentname'} = $xmpp_conf{'hostname'};
$xmpp_conf{'srv'} = 1;
```
