## Inconsistent Format for the PvD Identifier in the JSON Object

- [RFC 9704 - Establishing Local DNS Authority in Validated Split-Horizon Environments](https://www.rfc-editor.org/rfc/rfc9704)
- **Category**: (I-1) Direct inconsistency

Excerpt from Section 8:
 {
  "identifier": "pvd.example.com",
  "expires": "2025-05-23T06:00:00Z",
  "prefixes": ["2001:db8:1::/48", "2001:db8:4::/48"],
  "splitDnsClaims": [{ … }]
 }

Issue and Explanation:  
According to RFC 8801 (Section 4.3), the “identifier” key in the PvD Additional Information must be a PvD ID expressed as a fully qualified domain name (FQDN), which is typically represented with a trailing dot (e.g., "pvd.example.com."). In the JSON example in Section 8 the identifier is given without the trailing dot. This discrepancy creates uncertainty as to whether implementers should normalize the identifier by appending a trailing dot or treat the shown value as complete.  
Such ambiguity can lead to implementations that compare the received identifier against the PvD ID FQDN differently—one expecting “pvd.example.com.” versus one using “pvd.example.com”—potentially leading to validation mismatches.
