## Inconsistent Use of DNS Resolver Terminology in Section 1

- [RFC 9704 - Establishing Local DNS Authority in Validated Split-Horizon Environments](https://www.rfc-editor.org/rfc/rfc9704)
- **Category**: (I-3) Inconsistency with common knowledge

Excerpt from Section 1:  
 “To resolve a DNS query, there are three main behaviors that an
 implementation can apply: (1) answer from a local database, (2) query
 the relevant authorities and their parents, or (3) ask a server to
 query those authorities and return the final answer. Implementations
 that use these behaviors are called ‘authoritative nameservers’, ‘full/recursive resolvers’, and ‘forwarders’ (or ‘stub resolvers’), respectively.”

Explanation:  
The text equates the third behavior with both “forwarders” and “stub resolvers.”  
• In established DNS terminology (e.g., as described in RFC 1035), a stub resolver is defined as the minimal client‐side component that simply forwards queries to a recursive resolver. In contrast, a forwarder is a dedicated DNS server that receives queries (often from stub resolvers or clients) and then recursively retrieves the answer on behalf of the requester.  
• Conflating these two roles can lead to confusion regarding their distinct operational responsibilities and security implications. For instance, a system implementer might mistakenly assume that the properties and protections associated with a forwarder are also inherent in a stub resolver—although in practice the two are implemented and deployed differently.  
• This mixing of terminology represents an inconsistency in the document’s specification and may adversely affect the correct implementation of split-horizon DNS resolution behavior.

Notes:  
A clear distinction between the terms “forwarder” and “stub resolver” is essential for accurate interpretation of DNS behavior. To avoid misinterpretation, this inconsistency should be addressed by clarifying that the third mechanism refers solely to a DNS server that performs forwarding, not to a client-side stub resolver.
