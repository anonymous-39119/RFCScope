## Incomplete Guidance on “Loop Detection Heuristics” in the SVCB Resolution Procedure

- [RFC 9460 - Service Binding and Parameter Specification via the DNS (SVCB and HTTPS Resource Records)](https://www.rfc-editor.org/rfc/rfc9460)
- **Category**: (U-4) Incorrect/missing references

Excerpt from Section 3:
  “3. If an AliasMode SVCB record is returned for $QNAME (after following CNAMEs as normal), set $QNAME to its TargetName (without additional prefixes) and loop back to Step 2, subject to chain length limits and loop detection heuristics (see Section 3.1).”

Explanation:
 Step 3 instructs that if an AliasMode record is received the client must use its TargetName and reissue a SVCB query – but only while observing “chain length limits and loop detection heuristics.” However, Section 3.1 (“Handling Resolution Failures”) details what should occur if the chain length limit is exceeded (i.e. falling back to the authority endpoint) and does not offer any description or algorithm for “loop detection heuristics.”
 
 The absence of guidance on how to detect or terminate an alias loop leaves a critical gap. Without a clear definition, different implementations could apply ad hoc or inconsistent methods to detect loops, risking denial of service or interoperability issues. The reference “see Section 3.1” suggests that comprehensive guidance on loop detection was intended but was not provided.

Notes:
 • For robust implementation, the RFC should either provide a concrete description of the loop detection heuristics or revise the text to remove the reference if such heuristics are deemed unnecessary.
 • Clarifying this point is essential because the alias resolution procedure is foundational to SVCB operation, and any ambiguity can lead to potential security concerns or non-interoperable behavior.
