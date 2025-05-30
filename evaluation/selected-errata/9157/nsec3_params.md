## Ambiguous Naming of NSEC3-Related Items

- [RFC 9157 - Revised IANA Considerations for DNSSEC](https://www.rfc-editor.org/rfc/rfc9157)
- **Category**: (I-2) Indirect inconsistency

Excerpt from Section 2:  
  “…by allowing any DS hash algorithms, NSEC3 hash algorithms, NSEC3 parameters, and NSEC3 flags that are fully described in an RFC to have identifiers assigned in the IANA registries…”

Issue Explanation:  
Section 2 lists four items (DS hash algorithms, NSEC3 hash algorithms, NSEC3 parameters, and NSEC3 flags) but does not use the precise registry names found in Section 4. In Section 4 the relevant registries are identified as:  
  – “DNSSEC NSEC3 Hash Algorithms”  
  – “DNSSEC NSEC3 Flags”  
  – “DNSSEC NSEC3PARAM Flags”  

In particular, the term “NSEC3 parameters” in Section 2 is ambiguous—it appears intended to correspond to the registry “DNSSEC NSEC3PARAM Flags,” while “NSEC3 flags” is meant to correspond with “DNSSEC NSEC3 Flags.” The lack of an exact match in terminology may lead readers to be uncertain about which set of IANA assignments is being updated.

Additional Note:  
Clarification in Section 2 to directly refer to the registry names (i.e., “DNSSEC NSEC3 Hash Algorithms”, “DNSSEC NSEC3 Flags”, “DNSSEC NSEC3PARAM Flags”) would eliminate the ambiguity.
