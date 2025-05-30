## Between Specification and Common Knowledge (Documented Knowledge)

- [RFC 9567 - DNS Error Reporting](https://www.rfc-editor.org/rfc/rfc9567)
- **Category**: (I-3) Inconsistency with common knowledge

Excerpts from the RFC Section 1:
 “When an authoritative server serves a stale DNSSEC‑signed zone, the
  cryptographic signatures over the resource record sets (RRsets) may
  have lapsed.  A validating resolver will fail to validate these
  resource records.”

“Similarly, when there is a mismatch between the Delegation Signer (DS)
 records at a parent zone and the key signing key at the child zone, a
 validating resolver will fail to authenticate records in the child zone.”

Explanation:
 The text uses two different terms—“fail to validate” and “fail to authenticate”—in very similar failure scenarios. In the context of DNSSEC, the established and standard term for checking cryptographic integrity is “validate.” The use of “authenticate” in the second scenario is therefore inconsistent with the first and may lead to ambiguity regarding the exact operation expected from a validating resolver. This inconsistency in terminology may lead implementers to misinterpret the intended DNSSEC behavior.
