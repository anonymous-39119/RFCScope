# Errata 5049 - RFC 8078

- **RFC Title:** Managing DS Records from the Parent via CDS/CDNSKEY
- **RFC Publication Date:** March 2017
- Link to original errata report: [rfc-editor.org/errata/eid5049](https://www.rfc-editor.org/errata/eid5049)

```
Section 4 says:


   The contents of the CDS or CDNSKEY RRset MUST contain one RR and only
   contain the exact fields as shown below.

      CDS 0 0 0 0

      CDNSKEY 0 3 0 0

   The keying material payload is represented by a single 0.  This
   record is signed in the same way as regular CDS/CDNSKEY RRsets are
   signed.

   Strictly speaking, the CDS record could be "CDS X 0 X 0" as only the
   DNSKEY algorithm is what signals the DELETE operation, but for
   clarity, the "0 0 0 0" notation is mandated -- this is not a
   definition of DS digest algorithm 0.  The same argument applies to
   "CDNSKEY 0 3 0 0"; the value 3 in the second field is mandated by
   [RFC4034], Section 2.1.2.


It should say:

   The contents of the CDS or CDNSKEY RRset MUST contain one RR and only
   contain the exact fields as shown below.

      CDS 0 0 0 00

      CDNSKEY 0 3 0 AA==

   The keying material payload is represented by a single octet with
   the value 00. This record is signed in the same way as regular
   CDS/CDNSKEY RRsets are signed.

   Strictly speaking, the CDS record could be "CDS X 0 X X" as only the
   DNSKEY algorithm is what signals the DELETE operation, but for
   clarity, the "0 0 0 00" notation is mandated -- this is not a
   definition of DS digest algorithm 0.  The same argument applies to
   "CDNSKEY 0 3 0 AA=="; the value 3 in the second field is mandated by
   [RFC4034], Section 2.1.2.

Notes:

RFC 7344 defines both CDS and CDNSKEY record wire and presentation format to be identical to DS and DNSKEY wire and presentation format defined in RFC 4034.

In case of CDNSKEY record, RFC 4034 section 2.2 requires that:
> The Public Key field MUST be represented as a Base64 encoding of the Public Key.

As Base64 encoding encodes 6 bits into one character, one character alone can never be a valid Base64 sequence. The proper encoding of one-byte long sequence with binary value of 00 is AA==.

In case of CDS record, RFC 4034 section 5.3 requires that:
> The Digest MUST be represented as a sequence of case-insensitive hexadecimal digits

Although the value of a single 0 fulfils this requirement per se, it's not properly parsable by many implementations since it is expected to be even number of hex digits to align with octet boundaries in the wire format. So proper form of CDS record should contain two zeroes in place of the digest.


[ AD Note: Discussion on the DNSOP list: - https://www.ietf.org/mail-archive/web/dnsop/current/msg20267.html ]
```

## Explanation

The errata report highlights inconsistencies in the examples of CDS and CDNSKEY records in Section 4 of RFC 8078. The corrections involve changes to the keying material payload representation and base64 encoding, which directly impact the implementation of CDS and CDNSKEY record creation and parsing.  These are not stylistic changes but changes to the specifications' technical requirements, resulting in inconsistencies between the example and proper implementation.  The note about proper base64 encoding and the correct number of digits in the CDS record are critical to interoperability and therefore classify this as an inconsistency.
