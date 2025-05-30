## Ambiguity in Handling Queries with an Included CIDR Prefix

- [RFC 9224 - Finding the Authoritative Registration Data Access Protocol (RDAP) Service](https://www.rfc-editor.org/rfc/rfc9224)
- **Category**: (U-2) Direct under-specification (incomplete constraints)

Excerpt (from the IPv4 example in Section 5.1):
 “For example, a query for ‘192.0.2.1/25’ matches the ‘192.0.0.0/8’ entry and the ‘192.0.2.0/24’ entry in the example registry above. The latter is chosen by the client because it is the longest match.”

Explanation:
The examples show that query strings include a CIDR prefix (e.g. “/25” for IPv4 and “/48” for IPv6). However, the document does not clearly state whether—and if so, how—the provided prefix length in the query should influence the matching process. It is unclear whether the client is expected to use the full CIDR block as supplied (thereby narrowing the lookup) or to ignore the supplied prefix length and perform the longest prefix match solely on the address portion. This ambiguity in the role of the CIDR notation in the query may lead to inconsistent interpretation and implementation among RDAP clients.
