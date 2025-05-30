## Undefined Use of the Term “Endpoint”

- [RFC 9704 - Establishing Local DNS Authority in Validated Split-Horizon Environments](https://www.rfc-editor.org/rfc/rfc9704)
- **Category**: (U-1) Direct under-specification (undefined terms)

Excerpt from Section 3:
 “The protocol is applicable to any type of network offering split‐horizon DNS configuration.  
 The endpoint does not need any prior configuration to confirm that a local domain hint was indeed  
 authorized by the domain.”

Explanation:  
The term “endpoint” is used without a clear, precise definition, creating uncertainty about whether it refers to a DNS client, a stub resolver, or some other network component involved in DNS resolution. Although later parts of the document refer to “clients,” this section’s use of “endpoint” remains undefined. This underspecification could lead implementers to make divergent assumptions regarding what constitutes an endpoint and whether additional configuration might be required for certain devices. For example, an implementation that interprets “endpoint” narrowly might inadvertently impose unnecessary configuration requirements, while another following a broader interpretation might not—resulting in inconsistent behavior.
