#  Test Vectors for Group Keying

## Jim Test 1

Inputs:

* Master Secret:  0x0102030405060708090a0b0c0d0e0f10 (16 bytes)
* Master Salt: 0x9e7ca92223786340 (8 bytes)
* Group Id: 0x09EDDA (2 bytes)
* Countersign Algorithm: -7 (EDDSA w/ SHA-256)
* Countersign Algorithm Parameters: [[2], [2, 1]]
* Countersign Key Parameters: [2, 1]

* Entity #1 Id: 0x0001 (2 bytes)
* Entity #1 Key:
~~~
  {
    / kty / 1:2, 
    / kid / 2:h'E1', 
    / crv / -1:1, 
    / x / -2:h'bac5b11cad8f99f9c72b05cf4b9e26d244dc189f745228255a219
a86d6a09eff', 
    / y / -3:h'20138bf82dc1b6d562be0fa54ab7804a3a64b6d72ccfed6b6fb6e
d28bbfc117e', 
    / d / -4:h'57c92077664146e876760c9520d054aa93c3afb04e306705db609
0308507b4d3'
  }
~~~

* Entity #2 Id: 0x0200 (2 bytes)
* Entity #2 Key:
~~~
  {
    / kty / 1:2, 
    / kid / 2:h'E2', 
    / crv / -1:1, 
    / x / -2:h'65eda5a12577c2bae829437fe338701a10aaa375e1bb5b5de108d
e439c08551d', 
    / y / -3:h'1e52ed75701163f7f9e40ddf9f341b3dc9ba860af7e0ca7ca7e9e
ecd0084d19c', 
    / d / -4:h'aff907c99f9ad3aae6c4cdf21122bce2bd68b5283e6907154ad91
1840fa208cf'
  }
~~~

* Entity #3 Id: 0x0203 (2 bytes)
* Entity #3 Key:
~~~
  {
    / kty / 1:2, 
    / crv / -1:1, 
    / kid / 2:h'E3', 
    / x / -2:h'98f50a4ff6c05861c8860d13a638ea56c3f5ad7590bbfbf054e1c
7b4d91d6280', 
    / y / -3:h'f01400b089867804b8e9fc96c3932161f1934f4223069170d924b
7e03bf822bb', 
    / d / -4:h'02d1f7e6f26c43d4868d87ceb2353161740aacf1f7163647984b5
22a848df1c3'
  }
~~~


## Jim Test 2

* Master Secret:  0x0102030405060708090a0b0c0d0e0f10 (16 bytes)
* Master Salt: 0x9e7ca92223786340 (8 bytes)
* Group Id: 0xABCD (2 bytes)
* Countersign Algorithm: -8 (EdDSA)
* Countersign Algorithm Parameters: [[1], [1, 6]]
* Countersign Key Parameters: [1, 6]

* Entity #1 Id: 0x0001 (2 bytes)
* Entity #1 Public Key:

* Entity #2 Id: 0x0200 (2 bytes)
* Entity #2 Public Key:

* Entity #3 Id: 0x0203 (2 bytes)
* Entity #3 Public Key:


## Rikard Test 1

Inputs:

* Master Secret: 0x0102030405060708090a0b0c0d0e0f10 (16 bytes)
* Master Salt: 0x9e7ca92223786340 (8 bytes)
* Group Id: 0x37cbf3210017a2d3 (8 bytes)
* Countersign Algorithm: -7 (ECDSA w/ SHA-256)
* Countersign Algorithm Parameters: [[2], [2, 1]]
* Countersign Key Parameters: [2, 1]

* Entity #1 Id: 0x01 (1 bytes)
* Entity #1 Key:
~~~
  {
    / kty / 1: 2,
    / kid / 2: h'01',
    / d / -4: h'FEA2190084748436543C5EC8E329D2AFBD7068054F595CA1F987B9E43E2205E6',
    / y / -3: h'64CE3DD128CC4EFA6DE209BE8ABD111C7272F612C2DB654057B6EC00FBFB0684',
    / x / -2: h'1ADB2AB6AF48F17C9877CF77DB4FA39DC0923FBE215E576FE6F790B1FF2CBC96',
    / crv / -1: 1
  }
~~~

* Entity #2 Id: 0x (0 bytes)
* Entity #2 Key:
~~~
  {
    / kty / 1: 2,
    / kid / 2: h'',
    / d / -4: h'DA2593A6E0BCC81A5941069CB76303487816A2F4E6C0F21737B56A7C90381597',
    / y / -3: h'1897A28666FE1CC4FACEF79CC7BDECDC271F2A619A00844FCD553A12DD679A4F',
    / x / -2: h'0EB313B4D314A1001244776D321F2DD88A5A31DF06A6EEAE0A79832D39408BC1',
    / crv / -1: 1
  }
~~~

* Entity #3 Id: 0xAA (1 bytes)
* Entity #3 Key:
~~~
  {
    / kty / 1: 2,
    / kid / 2: h'AA',
    / d / -4: h'BF31D3F9670A7D1342259E700F48DD9983A5F9DF80D58994C667B6EBFD23270E',
    / y / -3: h'5694315AD17A4DA5E3F69CA02F83E9C3D594712137ED8AFB748A70491598F9CD',
    / x / -2: h'FAD4312A45F45A3212810905B223800F6CED4BC8D5BACBC8D33BB60C45FC98DD',
    / crv / -1: 1
  }
~~~


## Rikard Test 2

