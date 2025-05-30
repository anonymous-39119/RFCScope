## Ambiguity in the Zone Outsourcing Procedure  

- [RFC 9527 - DHCPv6 Options for the Homenet Naming Authority](https://www.rfc-editor.org/rfc/rfc9527)
- **Category**: (I-2) Indirect inconsistency

Excerpts from Section 3:
 “The HNA is willing to outsource the Public Homenet Zone or  
  Homenet Reverse Zone. …”
 
Later in Step 1:
 “… the DHCPv6 client is configured to include in its Option Request Option (ORO) the Registered Homenet Domain Option (OPTION_REGISTERED_DOMAIN), the Forward Distribution Manager Option (OPTION_FORWARD_DIST_MANAGER), and the Reverse Distribution Manager Option (OPTION_REVERSE_DIST_MANAGER) …”
 
And in Step 3:
 “… The HNA is authenticated (see ‘Securing the Control Channel’ (Section 6.6) of [RFC9526]) by the DM and the RDM. The HNA builds the Homenet Zone (or the Homenet Reverse Zone) …”

Explanation of the Inconsistency:
 • The opening sentence of Section 3 implies a mutually exclusive choice (“or”) between outsourcing the Public Homenet Zone and the Homenet Reverse Zone.
 • However, the procedure later mandates that the DHCPv6 client must always include both the Forward Distribution Manager Option and Reverse Distribution Manager Option. In addition, authentication is performed involving both the DM and the RDM.
 • This contradiction creates ambiguity: if an HNA were meant to outsource only one zone (as the “or” suggests), then why require a DHCPv6 client to unconditionally request both options and why authenticate against both distribution managers? Implementers may end up with diverging interpretations of whether the procedure expects simultaneous provisioning for both zones or if one set of options should be omitted when only one zone is intended.
 
Notes:
 No recommendation is provided; the report serves solely to point out the ambiguity requiring clarification by the RFC authors.
