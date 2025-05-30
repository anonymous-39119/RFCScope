## Terminology Inconsistency for DS Algorithms

- [RFC 9157 - Revised IANA Considerations for DNSSEC](https://www.rfc-editor.org/rfc/rfc9157)
- **Category**: (I-2) Indirect inconsistency

Excerpt from Section 2:  
  “…by allowing any DS hash algorithms, NSEC3 hash algorithms, NSEC3 parameters, and NSEC3 flags that are fully described in an RFC to have identifiers assigned in the IANA registries…”

Issue Explanation:  
Section 2 uses the term “DS hash algorithms” even though the corresponding IANA registry (as detailed in Section 4) is titled “DNSSEC Delegation Signer (DS) Resource Record (RR) Type Digest Algorithms”. Furthermore, RFC 6014 explicitly uses “Digest Algorithms” rather than “hash algorithms.” Although “hash” and “digest” are sometimes used interchangeably in informal discussion, the official registry language is precise. This discrepancy may cause confusion for implementers comparing the language in Section 2 with the formal registry title.

Additional Note:  
Including a direct quotation from Section 4 (e.g., the exact registry title “DNSSEC Delegation Signer (DS) Resource Record (RR) Type Digest Algorithms”) would clarify the precise nature of the inconsistency.
