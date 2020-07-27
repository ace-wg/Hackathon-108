# Group Servers

## Rikard Servers

2 servers running on the IETF network at 31.133.178.1 and multicast address 224.0.1.187, port 5699. Supports CoAP, OSCORE and Group OSCORE.

### Group OSCORE
**Sender contexts:**  
- Rikard Test 1 Entity 1
  - Server 1
- Rikard Test 1 Entity 2
  - Server 2

**Recipient context:**  
- Rikard Test 1 Entity 3
  - Server 1 & 2

### OSCORE
Server context from OSCORE RFC section C.2.2:  
https://tools.ietf.org/html/rfc8613#appendix-C.2.2

### Resources
- /test
  - Testing resource which responds with some status information
- /oscore/hello/1
  - (Group) OSCORE protected Hello-World Resource
- /oscore/hello/bw2
  - Block-Wise Resource
- /oscore/hello/coap
  - CoAP unprotected Hello-World Resource
- /oscore/hello/observe
  - Observable resource
