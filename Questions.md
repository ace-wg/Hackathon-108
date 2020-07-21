# Questions, Comments and Clarifications

1. When a signature key is provided as part of a group member, is the algorithm required to be part of that COSE key or not?  (JLS)
    1. For my implementation that value is not used and not required to be part of the COSE key. (Rikard)
    2. I initially required that it be present so that the server could validte that the key is for the correct algorithm.  My code currently does not require it but will check if present. (JLS)

2. Is there a reason that the Pairwise key derivation is not expressed in the same terms as the RFC 8613 method?
   salt = Recipient Key or Sender Key
   IKM = secret
   info - per above
   - only use the KEY and not the IV - which is ****

> Rikard: Could you elaborate a bit on this point 2 and the subpoint?

> JLS:  The key derivation process is the same as that in section 3.2.1 of RFC 8613 with the following changes:
> 1. Salt is set to the group sending key for the sender or receipient.
> 2. IKM is set to the computed key agreement secret
> 3. If no changes to how the partialIV and baseIV are used ("copied" from the group context"), then only the derived key is used, the derived IV is tossed.

3. Regarding the use of Weierstrass curves. I have begun implementing also som key remapping functions from Curve25519 and Edwards25519 to Wei25519 in 
[the following location](https://github.com/rikard-sics/californium/blob/group_oscore/cf-oscore/src/main/java/org/eclipse/californium/oscore/group/KeyRemapping.java#L296) with testing code [here](https://github.com/rikard-sics/californium/blob/group_oscore/cf-oscore/src/test/java/org/eclipse/californium/oscore/group/KeyRemappingTest.java#L163), based on the alternative curve representations [LWIG draft section E](https://tools.ietf.org/html/draft-ietf-lwig-curve-representations-10#appendix-E).
My understanding is that in the case Weierstrass curves are used that would mean the signing can be done with [ECDSA25519](https://tools.ietf.org/html/draft-ietf-lwig-curve-representations-10#section-10.2) and the shared secret calculation with [ECDH25519](https://tools.ietf.org/html/draft-ietf-lwig-curve-representations-10#section-10.3), although I am still looking into this. (Rikard)

> JLS:  This is also my understanding based on my conversations and review of Rene's document.
> I have asked Rene to provide either examples or a firm statement that the current examples are the same point and thus can be used for testing.
> The documents need to be clear which mapping is going to be used.

4. What date and time would fit best for you to do the interop testing? After you have gotten to Madrid time on Wednesday? Both Marco and I are quite flexible with the schedule. (Rikard)

>   [JLS] I will be on late Madrid time tomorrow.  I am currently up around Noon Stockholm time.  My schedule is wide open - If I am awake I will generally be online.

> Rikard: Alright, then shall we say tomorrow July 21 at 10.00 Madrid time? Or if you prefer during the afternoon perhaps at 14.00? For communication Marco and I sometimes use https://jitsi.org/ which can be convenient, we could use that during the session.

> JLS: 14:00 is much better than 10:00.  I am agnostic about the communication tool to use.  I am most likely going to hang out in the gather application when I am not elsewhere.  I will also try to be on Jabber most of the time as well.

> Rikard: Okay, sounds good. I have created a Jitsi meeting room at https://meet.jit.si/OSCOREGroupCommunication. Then we can all join at 14.00 tomorrow.

5. When a token is posted a second time and it is already present on the server, I am getting some conflicting advice about what should be happening.  Specifically:

> MT - I guess it's about a new Token updating access rights?

  - For an OSCORE token, I need to return a new/old/no nonce2 value?  I believe that we have said we should not be regenerating the OSCORE security context.
  
> MT - Based on the second from last paragraph in [1], Nonce2 is not returned, and the same context is used. I have not yet implemented this recent addition in the OSCORE profile, I can try during the hackathon.

[1] https://tools.ietf.org/html/draft-ietf-ace-oscore-profile-11#section-4.2

  - For a Join request, do I return a new/old/no kdcchallange value?

> MT - Based on [2], if a new/update Token is posted, the Client uses the the kdcchallenge in the response to the Token POST. That value is supposed to live as long as the posted Token. If the RS decides to change the value earlier than that, it replies with a 4.00 to a Joining Request, indicating the new value in the payload.

[2] https://tools.ietf.org/html/draft-ietf-ace-key-groupcomm-oscore-08#section-6.2.1

> JLS - In my state of semi-sleep last night I cam up with the following algorithm:
~~~
TokenA => The token that was posted
TokenB => The token for the security context if any
TokenC => The token in my database that I am comparing to

if TokenA matches TokenC:
   if TokenB security context wraps TokenA and TokenB.profile == TokenC.profile:
      //  Need to make some assumptions about absent profiles in the token.
      //  This corresponds to a replacement situation
      //  Don't replace a TLS token with an OSCORE token
      Replace w/o a new context
   else if profile == oscore and no OscoreNonce1 in the post:
      //  This can be interpreted as being a replace ask
      Replace w/o a new context
   else:
      Replace w/ a new context
else:
   Add new token w/ a new context

MatchToken(TokenA, TokenB, TokenC):
  if TokenA.issuer == TokenC.issuer and TokenA.cwti == TokenC.cwti:
      //  This should be exactly the same token
      return true
  if TokenA.issuer == TokenC.issuer and TokenA.subject == TokenC.subject:
      //  This would be a token for the same individual
      return true
  if TokenA.cnf + Defaults == TokenC.cnf + Defaults:
      //  This is the same cryptographic key
      return true
  if TokenB == TokenC and TokenA carried under TokenB security context:
     //  I posted the new certificate using the old certificate for security
     return true
  return false
~~~

6.  Trying to figure out all of the locations where we switch from multicast to unicode.  Did I miss anything?
*  Unsecure blockwise transfer (unicast) (what about multicast?)
*  Secure blockwise transfer
*  Respond to a group message (unicast or multicast)
*  Reply to a message
