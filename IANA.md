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
* sign_info ... `203`
* kdcchallence ... `205`

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

### Labels application/ace-groupcomm+cbor

* scope ...... `9`
* get_pub_keys ......... `101`
* client_cred .......... `102`
* client_cred_verify ... `103`
* cnonce ............... `39`
* pub_key_repos
* control_path
* gkty ..................... `1`
* key ...................... `2`
* pub_keys ................. `3`
* exp ...................... `4`
* ace_groupcomm_profile ... `38`
* num .................... `206`
* group_policies ......... `207`
* mgt_key_material

> JLS - Need to get a value for cnonce.  Probably don't care about the other items that do not have a value.

> MT - For 'cnonce' I use 39, i.e. the same value for application/ace+cbor defined in the framework. Yes, for now we can skip the ones with no value:
- 'pub_key_repos' is defined in ace-key-groupcomm but never used here, since the GM does act as key repo itself;
- 'mgt_key_material' is defined in ace-key-groupcomm but never used here, since the group relies on the plain point-to-point rekeying;
- 'control_path' is not used yet, I plan to add it later on.


> JLS - Where is sign_info used for this type?  Currently only in token post.

> MT - Right, it's not used for this type, just removed it. Othen than in the Token POST and following response, it can also be in a 4.00 response to a Join Request, see third bullet point in https://tools.ietf.org/html/draft-ietf-ace-key-groupcomm-oscore-08#section-6.3

> JLS - Where is pub_key_enc used for this message type?

> MT - Also removed, it's not needed altogether anymore. After we changed the sign_info format, that information is now just an element of an array, so we don't need a label.


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
