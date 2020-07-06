# Questions, Comments and Clarifications

1. When a signature key is provided as part of a group member, is the algorithm required to be part of that COSE key or not?  (JLS)
    1. For my implementation that value is not used and not required to be part of the COSE key. (Rikard)

2. Is there a reason that the Pairwise key derivation is not expressed in the same terms as the RFC 8613 method?
   salt = Recipient Key or Sender Key
   IKM = secret
   info - per above
   - only use the KEY and not the IV - which is ****
