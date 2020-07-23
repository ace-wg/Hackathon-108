# Resource Directory ACL Testing

## Policy

Current Policy Implemented
Audience: ResourceServer1

1.  Always permit access to /rd/epLookup and /rd/resLookup
2.  If an installer, always permit access to /rd and /rd?ep=*
3.  Allow access to /rd?ep=<name> for the EP name for the key
4.  Change access for /rd to /rd?ep=<name>

## Test Cases

### Client knows its name

1.  Client attempts to register /RD/EP?ep=client1
2.  RD responds with scope and pointer to AS
3.  Client gets token from AS
4.  Client connects to RD with token
5.  Client registers on RD
6.  Client updates on RD
7.  Client deletes on RD

### Client does not know its name

1.  Client attempts to register /RD/EP
2.  RD responds with scope and pointer to AS
3.  Client gets token from AS
4.  Client connects to RD with token
5.  Client registers on RD
6.  Client updates on RD
7.  Client deletes on RD

###  Installer creates

1.  Client attempts to register /RD/EP
2.  RD responds with scope and pointer to AS
3.  Client gets token from AS
4.  Client connects to RD with token
5.  Client registers on RD
6.  Client updates on RD
7.  Client deletes on RD

## Keys and Attributes - Jim's AS

Jim Authorization Server - coap://31.133.177.29:5688  coaps://31.133.177.29:5689
    ipv6 -  2001:67c:1233:176:45b0:2b8c:135b:feb9 - but I cannot ping it currently from outside of the IETF network.

Installer #1 - OSCORE only - Key to AS
~~~
{1: h'97F9808FEC61A369E87AB20F3EA22978', 2: h'8D536B576002C1', 3: h'D88D536B576002', 5: 10, 7: h'415331'}
~~~

Endpoint #1 - OSCORE only - Key to AS ep="ep1"
~~~
{1: h'B89D5952D1CCE8D2D571099FEB58039A', 2: h'66B1C3C4771293', 3: h'661B3CC7472139', 5: 10, 7: h'415331'}
~~~

Endpoint #2 - OCORE only - Key to AS ep="ep2"
~~~
{1: h'52B6554B5FD61B6A7C07E065F232A5CD', 2: h'5F855A1F9C350F', 3: h'8EA735679C41E8B4', 5: 10, 7: h'415331'}
~~~

Endpoint #3 - DTLS - Key to AS ep="ep3"
~~~
{1: 4, -1: h'95348A200F835861FECE77C0E21792A879D1D4AFBDB1CF83E5A7CBFBDE61B64E', 2: h'B9C18BEEDFCA543D'}
~~~


Resource Directory #1 - CWT Encryption Key
* Audience: ResourceDirectory1

~~~
AS Key - For introspection
{1: h'3C5E9E361E698CDEBAF2705A7622E5B1', 2: h'23D07B50D50582', 3: h'32D705B05D50', 5: 10, 7: h'415331'}

Token Key
{1: 4, -1: h'401681BA2E9D2F0ACDEF73D4336E1E2C', 4: h'EA60AC02CFFB6A68', 3: 10}
~~~

