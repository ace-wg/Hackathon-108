# Questions, Comments and Clarifications

1. When a signature key is provided as part of a group member, is the algorithm required to be part of that COSE key or not?  (JLS)
    1. For my implementation that value is not used and not required to be part of the COSE key. (Rikard)

2. Is there a reason that the Pairwise key derivation is not expressed in the same terms as the RFC 8613 method?
   salt = Recipient Key or Sender Key
   IKM = secret
   info - per above
   - only use the KEY and not the IV - which is ****

> Rikard: Could you elaborate a bit on this point 2 and the subpoint?

3. Regarding the use of Weierstrass curves. I have begun implementing also som key remapping functions from Curve25519 and Edwards25519 to Wei25519 in 
[the following location](https://github.com/rikard-sics/californium/blob/group_oscore/cf-oscore/src/main/java/org/eclipse/californium/oscore/group/KeyRemapping.java#L296) with testing code [here](https://github.com/rikard-sics/californium/blob/group_oscore/cf-oscore/src/test/java/org/eclipse/californium/oscore/group/KeyRemappingTest.java#L163), based on the alternative curve representations [LWIG draft section E](https://tools.ietf.org/html/draft-ietf-lwig-curve-representations-10#appendix-E).
My understanding is that in the case Weierstrass curves are used that would mean the signing can be done with [ECDSA25519](https://tools.ietf.org/html/draft-ietf-lwig-curve-representations-10#section-10.2) and the shared secret calculation with [ECDH25519](https://tools.ietf.org/html/draft-ietf-lwig-curve-representations-10#section-10.3), although I am still looking into this. (Rikard)


