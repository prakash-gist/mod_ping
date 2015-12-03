Description

This module implements support for XMPP Ping (XEP-0199) and periodic keepalives. When
this module is enabled ejabberd responds correctly to ping requests, as defined in the protocol.

Configuration options:

send pings: true|false If this option is set to true, the server sends pings to connected
clients that are not active in a given interval ping interval. This is useful to keep client
connections alive or checking availability. By default this option is disabled.

ping interval: Seconds How often to send pings to connected clients, if the previous option
is enabled. If a client connection does not send or receive any stanza in this interval, a ping
request is sent to the client. The default value is 60 seconds.

timeout action: none|kill What to do when a client does not answer to a server ping request
in less than 32 seconds. The default is to do nothing.

This example enables Ping responses, configures the module to send pings to client connections
that are inactive for 4 minutes, and if a client does not answer to the ping in less than 32 seconds,
its connection is closed:

This module implements XMPP Ping support (XEP-0199).

Supports
ejabberd 2.1.x

Installation
Make sure that ejabberd is already installed. The build script assumes it lives at /usr/lib/ejabberd

$ git clone https://github.com/prakash-gist/mod_ping.git
$ cd mod_ping
$ ./build.sh
$ sudo cp ebin/*.beam /usr/lib/ejabberd/ebin
Update the configuration in /etc/ejabberd/ejabberd.cfg and restart ejabberd

Example Configuration
%%%   =======
%%%   MODULES

{modules,
 [
  ....
  {mod_ping,     [
                  {send_pings, true},
                  {ping_interval, 10},
                  {timeout_action, kill}
                 ]},