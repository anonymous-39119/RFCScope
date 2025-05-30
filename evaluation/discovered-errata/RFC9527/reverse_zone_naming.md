## Inconsistency in the Naming of the Reverse DNS Zone  

- [RFC 9527 - DHCPv6 Options for the Homenet Naming Authority](https://www.rfc-editor.org/rfc/rfc9527)
- **Category**: (I-2) Indirect inconsistency

Excerpts from Section 1:
 • Paragraph 2 states:  
  “…The ISP delegates an IP prefix and the associated reverse zone to the home network. … becomes a natural candidate for hosting the Homenet Reverse Zone – that is, the Reverse Distribution Manager (RDM) and potentially the Reverse Public Authoritative Servers.”
 • Paragraph 4 states:  
  “…the HNA can manage and upload the Public Homenet Zone and the Reverse Public Homenet Zone as described in [RFC9526].”

Issue and Explanation:
There is an inconsistency in the naming of the reverse DNS zone between Paragraph 2 and Paragraph 4. In Paragraph 2 the reverse zone is referred to simply as the “Homenet Reverse Zone,” while in Paragraph 4 it is called the “Reverse Public Homenet Zone.” Since the forward zone is consistently named the “Public Homenet Zone,” this discrepancy creates an ambiguity as to whether the reverse zone should follow the same naming convention (i.e. “Reverse Public Homenet Zone”) or if it represents a distinct concept.  
 • This inconsistency belongs to the category of “inconsistency within the specification” and “use of incorrect terms.” It may lead to divergent interpretations or implementations — for example, confusion over which DNS zone to publish or manage — and therefore merits clarification by the authors.
 • Clarification of this naming convention is critical to ensure that implementers have a clear, consistent understanding of the roles and naming of both forward and reverse zones.
