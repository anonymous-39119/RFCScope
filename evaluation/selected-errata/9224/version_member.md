## Underspecification of the "version" Member Value

- [RFC 9224 - Finding the Authoritative Registration Data Access Protocol (RDAP) Service](https://www.rfc-editor.org/rfc/rfc9224)
- **Category**: (U-3) Indirect under-specification

Excerpt from Section 10.2:
  version:  a MEMBER with MEMBER-NAME "version" and MEMBER-VALUE a STRING

Explanation:
Section 3 of RFC 9224 states:  
  “The 'version' corresponds to the format version of the registry. This specification defines version '1.0'.”  
However, the formal definition in Section 10.2 merely requires that the “version” be any JSON string, with no constraint enforcing that the value be exactly "1.0." This oversight is an underspecification—a missing constraint—that leaves room for divergent interpretations. For example, one implementation might accept a registry with version "1.1" as valid while another, in strict compliance with the normative text, would reject it. Ensuring that only the literal value "1.0" is accepted is necessary to guarantee consistent behavior across implementations.
