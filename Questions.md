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
  - For an OSCORE token, I need to return a new/old/no nonce2 value?  I believe that we have said we should not be regenerating the OSCORE security context.
  - For a Join request, do I return a new/old/no kdcchallange value?
