## Underspecification in RA Option Length Calculation and ADN‑Only Mode Encoding

- [RFC 9463 - DHCP and Router Advertisement Options for the Discovery of Network‐designated Resolvers (DNR)](https://www.rfc-editor.org/rfc/rfc9463)
- **Category**: (U-3) Indirect under-specification

Excerpt (from Figure 7 and accompanying text) from Section 6.1:
   "Length:  8-bit unsigned integer.  The length of the option (including
   the Type and Length fields) is in units of 8 octets."  

   …  
   "Note that the 'Addr Length', 'ipv6-address(es)', and 'Service Parameters (SvcParams)' fields are not present if the ADN‑only mode is used (Section 3.1.6)."  

Explanation:
The text defines the option’s “Length” field but does not provide an explicit formula for computing the overall option length from its variable‐length subfields (such as ADN Length, Addr Length, and SvcParams Length). In contrast, the DHCPv4 and DHCPv6 options (Sections 4 and 5) include formulas (for example, the DHCP option states that when only an ADN is provided, the option length equals “ADN Length + 4”). Furthermore, when ADN‑only mode is applied the omission of the “Addr Length”, “ipv6-address(es)” and “SvcParams” fields is noted but there is no guidance on how this omission affects the overall option length.  
• Impact: Implementations could differ—for example, one might calculate the RA option length as “6 + (ADN Length)” (with ensuing padding to the next multiple of 8), while another might mistakenly apply the DHCP formula. This divergence can lead to mismatches in validation and processing of the RA option.
