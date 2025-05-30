## Incorrect Parameter Name in Section 1 – “QDCODE” vs. “QDCOUNT”

- [RFC 9619 - In the DNS, QDCOUNT Is (Usually) One](https://www.rfc-editor.org/rfc/rfc9619)
- **Category**: (I-2) Indirect inconsistency

Excerpt from Section 1:
  “…update the DNS base specification to clarify the allowable values of the QDCODE parameter in the specific case of DNS messages with OPCODE = 0.”

Explanation:
Section 1 of RFC 9619 consistently refers to the DNS header field that indicates the number of questions as “QDCOUNT” in both the introductory text and in related discussions. However, in the final clause of Section 1 the specification mistakenly uses “QDCODE” instead of “QDCOUNT.” Since no DNS header field named “QDCODE” exists—and the established DNS specifications (RFC 1034 and RFC 1035) only define and use QDCOUNT—this constitutes a clear typographical error.

Reasoning:
• The error undermines the internal consistency of the document by introducing a term that is not defined or used elsewhere.
• Implementations referencing this part of the RFC may be confused about which parameter is intended, potentially leading to incorrect behavior.
• Given the importance of precise parameter naming in DNS protocol specifications, this error should be corrected to ensure clarity and consistent interpretation.
