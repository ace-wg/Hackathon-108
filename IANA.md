# IANA Non-Registrations

There are a number of places where we do not yet have numbers for various parameters.
In order to have common values we will be using the following for testing.

## Media Types

* application/ace+cbor ==> 65000
* application/ace-groupcomm+cbor ==> 66000
* application/CoRAL ==> 65087
* text/CoRAL ==>  65343 

## for application/ace+cbor (OAuth Creation Hints)

* Nonce1 ==> 65  (ace-oscore-profile)
* Nonce2 ==> 66  (ace-oscore-profile)

## for CoRAL

* Dictionary References CBOR Tag ==> 99999


## ACE Oauth Profile Registry

* coap_oscore ==> 2
* coap_dtls ==> 4
* coap_mqtt => 6

## CWT Confirmation Methods

* osc ==> 99

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
