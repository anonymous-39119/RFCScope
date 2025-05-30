## Ambiguity in “consistent RESINFO” Requirement in Resolver Groups

- [RFC 9606 - DNS Resolver Information](https://www.rfc-editor.org/rfc/rfc9606)
- **Category**: (U-1) Direct under-specification (undefined terms)

Excerpt from Section 3:
 “If a group of resolvers is sharing the same ADN and/or anycast address, then these instances SHOULD expose a consistent RESINFO.”

Issue:
The directive “consistent RESINFO” is ambiguous. The document does not specify whether “consistent” requires that all resolvers publish RESINFO data that is byte‐for‐byte identical or whether semantic equivalence is sufficient. In the absence of a precise definition (for example, in terms of key/value ordering or allowed formatting variations), different implementations may interpret “consistent” in divergent ways.

Explanation and Reasoning:
• The term “consistent” is used without a clear definition. As a result, implementers might be unsure if minor differences—such as the ordering of key/value pairs or inconsequential formatting differences (e.g., nonsemantic whitespace variations) in the RESINFO record—constitute a violation of consistency.
• For instance, one resolver might output its RESINFO with keys sorted alphabetically while another (sharing the same ADN and/or anycast address) might preserve an insertion order. Although both representations are semantically equivalent, a DNS client that enforces a strict, byte‐for‐byte consistency check could falsely consider these records inconsistent.
• This ambiguity can lead to interoperability issues where clients may reject valid RESINFO responses or fail to enforce intended resolver selection policies.
• A clarifying statement regarding what “consistent” means in this context (e.g., that semantic equivalence is acceptable rather than requiring an exact, bit-for-bit match) would resolve this underspecification.

Conclusion:
The current wording in Section 3 leaves the expectation of RESINFO consistency under-specified. This ambiguity directly impacts interoperability in multi-resolver deployments. No additional underspecifications in this section that are not resolved by later references were identified.
