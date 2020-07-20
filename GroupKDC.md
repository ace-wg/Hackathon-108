# Group KDC

## Test cases

### C <-> AS

1. Test CoapToken using PSK, for asking access to an OSCORE group with a single role, using a REF token.

    1.1 The requested role is allowed in the specified group

    1.2 The requested role is allowed in the specified group

    1.3 Access to the specified group is not allowed

    1.4 The requested role is not allowed in the specified group

    1.5 The requested role is not allowed in the specified group


2. Test CoapToken using PSK, for asking access to an OSCORE group with multiple roles, using a REF token.

    2.1 Both requested roles are allowed in the specified group

    2.2 Access to the specified group is not allowed

    2.3 Only one role out of the two requested ones is allowed in the specified group


3. Test CoapToken using PSK, for asking access to an OSCORE group with multiple roles, using a REF token. (Alternative version with different client)

    3.1 The requested role is not allowed in the specified group

    3.2 Only one role out of the two requested ones is allowed in the specified group

### C <-> Group Manager (DTLS profile)

1. Test post to authz-info, then RPK handshake, then join the group with a single role.

2.  Test post to authz-info, then RPK handshake, then join the group with multiple roles.

3. Test post to authz-info, then PSK handshake, then join the group with a single role.

4. Test post to authz-info, then PSK handshake, then join the group with multiple roles.

### C <-> Group Manager (OSCORE profile)

1. Test post to Authz-Info, then join the group with a single role.

2. Test post to Authz-Info, then join the group with multiple roles.

---

## General Configuration and Parameter Values

### Token protection

- Use `Encrypt0` and `AES_CCM_16_64_128`

### C <-> AS

Use DTLS in PSK mode

(More key material is already hardcoded, to possibly test in RPK mode too)

### C <-> Group Manager

Possible to test:

- DTLS profile in PSK mode (w/ latest updates regarding "psk_identity")
- DTLS profile in RPK mode
- OSCORE profile

### Content-Formats

application/ace+cbor ............. `65000`
application/ace-groupcomm+cbor ... `66000`

### Profile identifiers

coap_oscore ... `2`
coap_dtls ..... `4`

### Group OSCORE role identifiers

Requester ... `1`
Responder ... `2`
Monitor ..... `3`
Verifier .... `4`

### Labels in the POST request to /authz-info

sign_info ... `203`
nonce1 (OSCORE profile) ....... `65`

### Labels in response from /authz-info

kdcchallence ... `205`
nonce2 (OSCORE profile) .......... `66`

### Labels in the Joining Request

scope ...... `9`
get_pub_keys ......... `101`
client_cred .......... `102`
client_cred_verify ... `103`

### Labels in the Joining Response

gkty ..................... `1`
key ...................... `2`
pub_keys ................. `3`
exp ...................... `4`
ace_groupcomm_profile ... `38`
sign_info .............. `203`
pub_key_enc ............ `204`
num .................... `206`
group_policies ......... `207`


#### Values for 'gkty' in the Joining Response

"Group OSCORE Security Context Object" ... `1`


#### Values for 'ace_groupcomm_profile'

"coap_group_oscore_app" ... `1`

#### Labels for 'group_policies' entries

"Sequence Number Synchronization Method" ... `1`
"Key Update Check Interval" ................ `2`
"Expiration delta" ......................... `3`
"Group OSCORE Pairwise Mode" ............... `4`

#### Values for "Sequence Number Synchronization Method"

"Best effort" ............... `1`
"Baseline" .................. `2`
"Echo challenge-response" ... `3`

---

## AS configuration

### Registered Group Managers

Three Group Managers are registered:

- `"rs2"`
- `"rs3"`
- `"rs4"`

For each Group Manager, Tokens can be released to access one OSCORE Group with name: `"feedca570000"`

### Registered clients

Two clients are registered:

1) `"ClientF"`
    - Can request to access the group `"feedca570000"` at rs2, with any role
    - Can request to access the group `"feedca570000"` at rs3, as `"requester"` or `"monitor"`

2) `"ClientG"`, with less rights
    - Can request to access the group `"feedca570000"` at rs2, only as `"requester"`

Both clients are registered as supporting the DTLS profile.

### Keys

#### PSK between ClientF and the AS

Key identity: `"clientF"`
Key Octet: `{0x61, 0x62, 0x63, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x11}`

### PSK between ClientG and the AS
Key identity: `"clientG"`
Key Octet: `{0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x12}`


### PSK between rs2 and the AS
Key identity: `"rs2"`
Key Octet: `{0x51, 0x52, 0x53, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x11}`

### PSK between rs3 and the AS
Key identity: `"rs3"`
Key Octet: `{0x51, 0x52, 0x53, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x12}`

#### PSK between rs4 and the AS
Key identity: `"rs4"`
Key Octet: `{0x51, 0x52, 0x53, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x13}`

#### Key to encrypt the Token for rs2
`{(byte)0xb1, (byte)0xa2, (byte)0xa3, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x10}`

#### Key to encrypt the Token for rs3
`{(byte)0xb1, (byte)0xb2, (byte)0xb3, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x11}`

#### Key to encrypt the Token for rs4
`{(byte)0xb1, (byte)0xb2, (byte)0xb3, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x12}`

#### Asymmetric key pair of the AS
```
X = "058F35F3C0D34D3DF50DEBC82208CDA9BE373AF7B8F7AAC381577B144D5FA781"
Y = "364269649744067D4600A529AE12076750D90C5EFCD9835137DB1AE2B4BACCB8"
D = "0089A92D07B34F1D806FABFF444AF6507C5F18F47BB2CCFAA7FBEC447303790D53"
```
#### Public key of a RS (same for all the RSs)
```
X = "73B7D755827D5D59D73FD4015D47B445762F7CDB59799CD966714AB2727F1BA5"
Y = "1A84F5C82797643D33F7E6E6AFCF016522238CE430E1BF21A218E6B4DEEAC37A"
```
#### Public key of a Client
```
X = "12D6E8C4D28F83110A57D253373CAD52F01BC447E4093541F643B385E179C110"
Y = "283B3D8D28FFA59FE5CB540412A750FA8DFA34F6DA69BCDA68400D679C1347E8"
```
---

## Group Manager configuration

### Group configuration

One OSCORE Group exists, with name: `"feedca570000"`

The joining uri-path is: `group-oscore/feedca570000`

#### Master Secret
```
{ (byte) 0x01, (byte) 0x02, (byte) 0x03, (byte) 0x04,
  (byte) 0x05, (byte) 0x06, (byte) 0x07, (byte) 0x08,
  (byte) 0x09, (byte) 0x0A, (byte) 0x0B, (byte) 0x0C,
  (byte) 0x0D, (byte) 0x0E, (byte) 0x0F, (byte) 0x10 }
```
#### Master Salt
```
{ (byte) 0x9e, (byte) 0x7c, (byte) 0xa9, (byte) 0x22,
  (byte) 0x23, (byte) 0x78, (byte) 0x63, (byte) 0x40 }
```
#### Group ID
```
{ (byte) 0xfe, (byte) 0xed, (byte) 0xca, (byte) 0x57,
  (byte) 0xf0, (byte) 0x5c }
```
#### AEAD algorithm
`AES_CCM_16_64_128`

#### HKDF algorithm
`HKDF_HMAC_SHA_256`
  
#### Signature algorithm
Can be configured either as ECDSA_256 or Ed25519

####  Group policies values (all with default values)
"Sequence Number Synchronization Method" = `1` ("Best effort")
"Key Update Check Interval"              = `3600`
"Expiration delta"                       = `0`
"Group OSCORE Pairwise Mode"             = `False`

### To also include in the Joining Response

#### Location-Path option
`"group-oscore/feedca570000/nodes/25"`

#### Keying material version ('num')
`0`

#### Keying material expiration ('exp')
`1000000`

### Group membership

The Sender ID `0x25` will be assigned to the joining node

The node name `"25"` will be assigned to the joining node

Two nodes are already in the group, with Sender ID:

1. `0x52`
2. `0x77`

### Keys

#### Key used to protect the Tokens
`{ (byte)0xa1, (byte)0xa2, (byte)0xa3, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x10 }`


#### Asymmetric key pair for the DTLS profile in RPK mode (same for all audiences)
```
X = "73B7D755827D5D59D73FD4015D47B445762F7CDB59799CD966714AB2727F1BA5"
Y = "1A84F5C82797643D33F7E6E6AFCF016522238CE430E1BF21A218E6B4DEEAC37A"
D = "00EA086573C683477D74EB7A0C63A6D031D5DEB10F3CC2876FDA6D3400CAA4E507"
```

#### ECDSA_256 public keys of already present group members:

// For Sender ID `0x52`
```
X = "35F3656092E1269AAAEE6262CD1C0D9D38ED78820803305BC8EA41702A50B3AF"
Y = "5D31247C2959E7B7D3F62F79622A7082FF01325FC9549E61BB878C2264DF4C4F"
```

// For Sender ID `0x77`
```
X = "9DFA6D63FD1515761460B7B02D54F8D7345819D2E5576C160D3148CC7886D5F1"
Y = "76C81A0C1A872F1730C10317AB4F3616238FB23A08719E8B982B2D9321A2EF7D"
```

#### Ed25519 public keys of already present group members:

// For Sender ID `0x52`
`X = "77EC358C1D344E41EE0E87B8383D23A2099ACD39BDF989CE45B52E887463389B"`

// For Sender ID `0x77`
`X = "105B8C6A8C88019BF0C354592934130BAA8007399CC2AC3BE845884613D5BA2E"`

---

## Client configuration

### Group joining

The joining node considers the audience `"rs2"` as Group Manager.

The Sender ID `0x25` will be assigned to the joining node

### Keys

#### ClientF <--> AS symmetric key
Key identity: `"clientF"`
Key Octet: `{0x61, 0x62, 0x63, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x11}`


#### ClientF <--> AS symmetric key
Key identity: `"clientG"`
Key Octet: `{0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x12}`


#### Key used to protect the Tokens
`{(byte)0xa1, (byte)0xa2, (byte)0xa3, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x10}`


#### Public key of the Group Manager for the DTLS profile in RPK mode (same for all audiences)
```
X = "73B7D755827D5D59D73FD4015D47B445762F7CDB59799CD966714AB2727F1BA5"
Y = "1A84F5C82797643D33F7E6E6AFCF016522238CE430E1BF21A218E6B4DEEAC37A"
```
#### Symmetric PoP key for ClientF
KeyID: `{(byte)0x91, (byte)0xEC, (byte)0xB5, (byte)0xCB, 0x5D, (byte)0xAA}`
Key Octet: `{0x61, 0x62, 0x63, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x11}`

#### Symmetric PoP key for ClientG
KeyID:  `{(byte)0x91, (byte)0xEC, (byte)0xB5, (byte)0xCB, 0x5D, (byte)0xAB}`
Key Octet: `{0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f, 0x12}`

#### ECDSA_256 key pair of the joining node:
```
X = "E8F9A8D5850A533CDA24B9FA8A1EE293F6A0E1E81E1E560A64FF134D65F7ECEC"
Y = "164A6D5D4B97F56D1F60A12811D55DE7A055EBAC6164C9EF9302CBCBFF1F0ABE"
D = "3BE0047599B42AA44B8F8A0FA88D4DA11697B58D9FCC4E39443E9843BF230586"
```
#### Ed25519 key pair of the joining node:
```
X = "069E912B83963ACC5941B63546867DEC106E5B9051F2EE14F3BC5CC961ACD43A"
D = "64714D41A240B61D8D823502717AB088C9F4AF6FC9844553E4AD4C42CC735239"
```