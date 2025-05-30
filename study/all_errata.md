<details>
<summary><b>Errata 4197</b> from <b>RFC 7110</b> - Return Path Specified Label Switched Path (LSP) Ping (January 2014)</summary>

```
Section 4 says:


The Reply Path TLV contains one or more nested sub-TLVs that can be
used


It should say:

The Reply Path TLV contains zero or more nested sub-TLVs that can be
used

Notes:

As section 4.2 correctly states, the Reply Path TLV can contain zero
sub-TLVs; this brings section 4 inline.
```

</details>

<br>**Explanation:**
The erratum points out an inconsistency between Section 4 and Section 4.2 regarding the number of nested sub-TLVs in the Reply Path TLV.  Section 4 incorrectly states "one or more", while Section 4.2 correctly states "zero or more."  This impacts implementation because an implementation relying on Section 4's description would incorrectly reject valid messages with zero sub-TLVs.

---

<details>
<summary><b>Errata 3944</b> from <b>RFC 7139</b> - GMPLS Signaling Extensions for Control of Evolving G.709 Optical Transport Networks (March 2014)</summary>

```
Section 5.1 says:


      ODUk.ts       Minimum          Nominal          Maximum
      -----------------------------------------------------------
      ODU2.ts    1,249,384.632    1,249,409.620     1,249,434.608
      ODU3.ts    1,254,678.635    1,254,703.729     1,254,728.823
      ODU4.ts    1,301,683.217    1,301,709.251     1,301,735.285

              Table 1: Actual TS Bit Rate of ODUk (in Kbps)


It should say:

      ODTUk.ts       Minimum          Nominal           Maximum
      ------------------------------------------------------------
      ODTU2.ts    1,249,384.632    1,249,409.620     1,249,434.608
      ODTU3.ts    1,254,678.635    1,254,703.729     1,254,728.823
      ODTU4.ts    1,301,683.217    1,301,709.251     1,301,735.285

              Table 1: Actual TS Bit Rate of ODUk (in Kbps)
```

</details>

<br>**Explanation:**
The erratum corrects a typographical error in Table 1, changing "ODUk.ts" to "ODTUk.ts".  While seemingly minor, this inconsistency could lead to implementation issues if an implementation is strictly following the incorrect label in the original text.  The inconsistency is in the naming of the transport units which would directly impact how an implementation would interpret the values in the table.

---

<details>
<summary><b>Errata 3945</b> from <b>RFC 7139</b> - GMPLS Signaling Extensions for Control of Evolving G.709 Optical Transport Networks (March 2014)</summary>

```
Section 7 says:


For the ingress node, a Path message with SE style SHOULD also be
sent for decreasing the ODUflex bandwidth.

It should say:

For the ingress node, a Path message with SE style MUST also be
sent for decreasing the ODUflex bandwidth.

Notes:

Section 7 requires that Shared Explicit (SE) MUST be used at the beginning when creating a resizable ODUflex connection. Thus, the SE style MUST also be used when signaling for bandwidth increase or decrease.  The increase procedure mandates the use of SE style; however, the decrease procedure uses SHOULD.  The decrease procedure should also make the SE signaling mandatory.

This change, that looks to be a change of substance, has been verified with the authors to be an editorial issue that was caused by not keeping the paragraphs in synch.
```

</details>

<br>**Explanation:**
The erratum corrects a discrepancy in the use of SHOULD versus MUST for signaling bandwidth decrease.  The original text uses SHOULD, which is weaker and leaves room for non-compliant implementations. The correction to MUST ensures consistent and unambiguous behavior.  The inconsistency is between the requirements for increasing bandwidth (MUST use SE style) and decreasing bandwidth (SHOULD use SE style), which directly affects implementation correctness.

---

<details>
<summary><b>Errata 3946</b> from <b>RFC 7139</b> - GMPLS Signaling Extensions for Control of Evolving G.709 Optical Transport Networks (March 2014)</summary>

```
Section 7 says:


After decreasing the bandwidth, the ingress node
SHOULD send a ResvErr message to tear down the old control state.

It should say:

After decreasing the bandwidth, the ingress node
SHOULD send a PathTear message to tear down the old control state.

Notes:

PathTear is the usual mechanism to teardown old control state. This is would also make the bandwidth decreasing procedure consistent with the bandwidth increasing procedure (bandwidth increasing procedure uses PathTear to teardown old control state.)

This change looks like a change of substance, but the authors confirm that their intent was to use the same process for both the increase and decrease in bandwidth.
```

</details>

<br>**Explanation:**
The erratum corrects the message type used to tear down the old control state after decreasing bandwidth. The original text suggests using a ResvErr message, while the correction specifies PathTear.  This inconsistency creates ambiguity in implementation, as ResvErr and PathTear have different meanings and functions within the protocol. Maintaining consistency between the bandwidth increase and decrease procedures is crucial for correct implementation.

---

<details>
<summary><b>Errata 3915</b> from <b>RFC 7159</b> - The JavaScript Object Notation (JSON) Data Interchange Format (March 2014)</summary>

```
Section 12 says:


   Since JSON's syntax is borrowed from JavaScript, it is possible to
   use that language's "eval()" function to parse JSON texts.

It should say:

   Since JSON's syntax is borrowed from JavaScript, it is possible to
   use that language's "eval()" function to parse most (but not all)
   JSON texts.

Notes:

This wording may be construed as meaning that every compliant JSON text is parseable as JavaScript, which is not the case: <http://timelessrepo.com/json-isnt-a-javascript-subset>. (Actually I would prefer this to be stated clearly elsewhere in the document, e.g. where it says "JSON's design goals were for it to be [...] a subset of JavaScript".)

 --VERIFIER NOTES-- 
As per the above citation, there are characters (in particular line terminators like U+2028 and U+2029) which are permissible in JSON but not permissible in JavaScript. The corrected text makes this clearer.
```

</details>

<br>**Explanation:**
The original statement implies that all valid JSON is directly parseable by JavaScript's eval(), which is incorrect. The correction acknowledges that some JSON texts may not be parseable with eval() due to differences in permitted characters between JSON and JavaScript. This inconsistency impacts implementations that rely on eval() for JSON parsing, potentially leading to errors or security vulnerabilities when processing non-compliant JSON.

---

<details>
<summary><b>Errata 5055</b> from <b>RFC 7162</b> - IMAP Extensions: Quick Flag Changes Resynchronization (CONDSTORE) and Quick Mailbox Resynchronization (QRESYNC) (May 2014)</summary>

```
Section 3.1.2.1 says:


   C: A142 SELECT INBOX
   S: * 172 EXISTS
   S: * 1 RECENT
   S: * OK [UNSEEN 12] Message 12 is first unseen
   S: * OK [UIDVALIDITY 3857529045] UIDs valid
   S: * OK [UIDNEXT 4392] Predicted next UID
   S: * FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
   S: * OK [PERMANENTFLAGS (\Deleted \Seen \*)] Limited
   S: * OK [HIGHESTMODSEQ 715194045007]
   S: A142 OK [READ-WRITE] SELECT completed

It should say:

   C: A142 SELECT INBOX
   S: * 172 EXISTS
   S: * 1 RECENT
   S: * OK [UNSEEN 12] Message 12 is first unseen
   S: * OK [UIDVALIDITY 3857529045] UIDs valid
   S: * OK [UIDNEXT 4392] Predicted next UID
   S: * FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
   S: * OK [PERMANENTFLAGS (\Deleted \Seen \*)] Limited
   S: * OK [HIGHESTMODSEQ 715194045007] Ok
                                       ^^^
   S: A142 OK [READ-WRITE] SELECT completed

Notes:

RFC 7162 purports to extend RFC 3501 by adding the HIGHESTMODSEQ value as an option for the resp-text-code syntax. However, RFC 3501 only uses resp-text-code in the resp-text ABNF production, in which case it is always followed by a single space ("SP") and the "text" non-terminal, which expands to "1*TEXT-CHAR", as in non-empty text. As such, having a response code without any human-readable text suffix is illegal per the RFC 3501 spec, and the examples should be updated to be correct.
```

</details>

<br>**Explanation:**
The erratum points out that the example in Section 3.1.2.1 violates RFC 3501 by omitting the human-readable text after HIGHESTMODSEQ response code.  This is inconsistent with the requirements of RFC 3501 and could result in implementations rejecting valid responses or producing invalid ones, thus directly affecting interoperability.

---

<details>
<summary><b>Errata 5127</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section 5.2. says:


IMSK = First 32 octets of TLS-PRF(EMSK, "TEAPbindkey@ietf.org" |
     "\0" | 64)

It should say:

IMSK = First 32 octets of TLS-PRF(EMSK, "TEAPbindkey@ietf.org" |
     "\0", 64)

Notes:

According to

RFC5246 The Transport Layer Security (TLS) Protocol Version 1.2

5.  HMAC and the Pseudorandom Function

"TLS's PRF is created by applying P_hash to the secret as:

      PRF(secret, label, seed) = P_<hash>(secret, label + seed)"
```

</details>

<br>**Explanation:**
The erratum corrects the formula for IMSK calculation. The original formula incorrectly includes a pipe symbol between "\0" and 64, where it should be a comma.  This is an inconsistency because the corrected formula adheres to the TLS-PRF specification described in RFC 5246, whereas the original formula does not. This inconsistency can lead to incorrect IMSK generation, affecting the security of the TEAP protocol.

---

<details>
<summary><b>Errata 5128</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section 5.2. says:


IMCK[j] = TLS-PRF(S-IMCK[j-1], "Inner Methods Compound Keys",
                IMSK[j], 60)

It should say:

IMCK[j] = the first 60 octets of TLS-PRF(S-IMCK[j-1],
              "Inner Methods Compound Keys",
              IMSK[j])

Notes:

According to

RFC5246 The Transport Layer Security (TLS) Protocol Version 1.2

5.  HMAC and the Pseudorandom Function

"TLS's PRF is created by applying P_hash to the secret as:

     PRF(secret, label, seed) = P_<hash>(secret, label + seed)"

Paul Wouters(AD): Corrected the text proposed by the original submitter, as it now appears in 7170bis
```

</details>

<br>**Explanation:**
The erratum corrects the formula for calculating IMCK[j]. The original formula incorrectly specifies a length of 60 octets as a parameter to the TLS-PRF function, whereas the TLS-PRF function from RFC 5246 does not take an explicit length parameter.  The correction clarifies that only the first 60 octets of the result are used. This inconsistency would lead to an incorrect calculation of IMCK[j], affecting the security of TEAP.

---

<details>
<summary><b>Errata 5765</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section 4.2.2 says:


   M

      Mandatory, set to one (1)


It should say:

   M

      0 (Optional)


Notes:

Authority-ID TLV is used only as an Outer TLV (in TEAP/Start) and Section 4.3.1 mandates all Outer TLVs to be marked as optional ("Outer TLVs MUST be marked as optional"). As such, Section 4.2.2 is incorrect in claiming the Authority-ID TLV to use M=1.
```

</details>

<br>**Explanation:**
The errata highlights a contradiction between Section 4.2.2 and Section 4.3.1 regarding the mandatory/optional status of the Authority-ID TLV.  Section 4.3.1 mandates all Outer TLVs to be optional, while Section 4.2.2 incorrectly states the Authority-ID TLV as mandatory. This directly impacts implementation as it provides conflicting instructions on how to handle this specific TLV.

---

<details>
<summary><b>Errata 5844</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section C.1 says:


                            <- Crypto-Binding TLV (Request),
                                Result TLV (Success),
                                (Optional PAC TLV)

       Crypto-Binding TLV(Response),
       Result TLV (Success),
       (PAC-Acknowledgement TLV) ->


It should say:

                            <- Intermediate-Result-TLV (Success),
                                Crypto-Binding TLV (Request),
                                Result TLV (Success),
                                (Optional PAC TLV)

       Intermediate-Result-TLV (Success),
       Crypto-Binding TLV(Response),
       Result TLV (Success),
       (PAC-Acknowledgement TLV) ->


Notes:

Section 3.3.2 implies that Intermediate-Result TLV is used after each round of Basic-Password-Auth-Req/Resp TLVs. However, the example sequence in C.1 does not show this. The proposed change in this errata adds the Intermediate-Result TLV indication here. Similar change should be done in C.2 (i.e., add Intermediate-Result TLV (Failure) to the messages that include Result TLV) since the language in 3.3.2 describe the indication to be used for both success and failure cases.

In addition to this change in C.1, it would be good to clarify the specification globally to avoid confusion about this case since almost all discussion regarding Intermediate-Result TLV currently is in the context of inner EAP authentication. 3.3.2 should have a MUST statement similar to 3.3.1. 3.6 should cover success or failure indications of basic password auth like it does EAP methods. 4.2.11 should note Intermediate-Result TLV is used with both inner EAP and basic password auth. 4.2.13 should mention basic password auth in the "regardless of whether there is an inner EAP method authentication or not" sentence.
```

</details>

<br>**Explanation:**
The errata report points out that the example message sequence in Section C.1 does not include the Intermediate-Result TLV, which is implied to be used in Section 3.3.2.  This omission creates an inconsistency between the example and the specification.  This inconsistency affects implementations that follow the example sequence literally but must also follow section 3.3.2. The errata proposes to add the missing TLV to correct this inconsistency, which is required to ensure correct implementation.

---

<details>
<summary><b>Errata 7145</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section 3.3.3 says:


   The Crypto-Binding TLV MUST be exchanged and verified
   before the final Result TLV exchange, regardless of whether or not
   there is an inner EAP method authentication.

It should say:

   Except as noted below, the Crypto-Binding TLV MUST be exchanged and verified
   before the final Result TLV exchange, regardless of whether or not
   there is an inner EAP method authentication

Notes:

The text contradicts itself in the same paragraph, because it goes on to say:

   The server may send the final Result TLV along with an
   Intermediate-Result TLV and a Crypto-Binding TLV to indicate its
   intention to end the conversation.  If the peer requires nothing more
   from the server, it will respond with a Result TLV indicating success
   accompanied by a Crypto-Binding TLV and Intermediate-Result TLV if
   necessary.

So there are actually several legal combinations here:

1. Server and peer perform a crypto-binding exchange in anticipation of later sending Result TLVs
2. The server and peer combine their crypto-binding and Result TLV in the same message.
3. One side initiates a crypto-binding TLV and the OTHER responds with both crypto-binding and Result TLV.

The practice seems to be to include the crypto-binding TLVs alongside Result TLVs.
```

</details>

<br>**Explanation:**
The errata highlights a contradiction within Section 3.3.3.  The initial statement mandates a Crypto-Binding TLV exchange before the final Result TLV, regardless of inner EAP method authentication. However, a subsequent sentence describes scenarios where this order is not followed (Result and Crypto-Binding TLVs sent together). This inconsistency creates ambiguity in the specification, impacting implementation.  The proposed addition of 'Except as noted below' resolves this conflict, improving consistency and clarity for implementers.

---

<details>
<summary><b>Errata 4874</b> from <b>RFC 7181</b> - The Optimized Link State Routing Protocol Version 2 (April 2014)</summary>

```
Section 17.1 says:


   If the router changes its originator address, then:

   1.  If there is no Originator Tuple with:

       *  O_orig_addr = old originator address

       then create an Originator Tuple with:

       *  O_orig_addr := old originator address

       The Originator Tuple (existing or new) with:

       *  O_orig_addr = new originator address

       is then modified as follows:

       *  O_time := current time + O_HOLD_TIME


It should say:

   If the router changes its originator address, then:

   1.  If there is an Originator Tuple with:

       *  O_orig_addr = old originator address

       then modify it as follows:

       *  O_orig_addr := new originator address
       *  O_time := current time + O_HOLD_TIME

       otherwise create an Originator Tuple with:

       *  O_orig_addr := new originator address
       *  O_time := current time + O_HOLD_TIME


Notes:

At the time of the modification Originator Tuple with O_orig_addr = new originator address does not yet exist.

===
The Corrected text reflects consultation with the WG.
```

</details>

<br>**Explanation:**
The original description contradicts itself regarding the handling of Originator Tuples when the originator address changes. It states that a new tuple should be created if one with the old address does not exist, but then proceeds to modify a tuple with the new address (which wouldn't yet exist). The correction provides a consistent and unambiguous algorithm by correctly ordering the creation and modification of the Originator Tuple.  This inconsistency would lead to incorrect management of Originator Tuples, affecting the routing protocol's operation.

---

<details>
<summary><b>Errata 4517</b> from <b>RFC 7203</b> - An Incident Object Description Exchange Format (IODEF) Extension for Structured Cybersecurity Information (April 2014)</summary>

```
Section 5.2 says:


The schema has the <sequence> </sequence> tags.

It should say:

The tags should be <xsd:sequence></xsd:sequence>.

Notes:

The schema is invalid without the correction.

The examples use <xsd:sequence>, but the actual schema just has <sequence> and does need to be fixed.  With this errata update, the hope is the IANA registered schema can be updated.
```

</details>

<br>**Explanation:**
The erratum corrects an error in the schema definition. The original schema is invalid due to the missing namespace prefix "xsd:" in the <sequence> tags. This inconsistency directly impacts the usability of the schema as it cannot be parsed by schema validators, affecting implementations that rely on schema validation.

---

<details>
<summary><b>Errata 5436</b> from <b>RFC 7208</b> - Sender Policy Framework (SPF) for Authorizing Use of Domains in Email, Version 1 (April 2014)</summary>

```
Throughout the document, when it says:


    header-field     = "Received-SPF:" [CFWS] result FWS [comment FWS]
                       [ key-value-list ] CRLF

It should say:

    header-field     = "Received-SPF:" [CFWS] result [ FWS comment ]
                       [ FWS key-value-list ] [FWS] CRLF

Notes:

As specified, this ABNF doesn't allow a header field value like result-FWS-comment with no FWS or key-value-list following it, a header field value which occurs very often in Received-SPF header fields I see in practice.  (Note that FWS must contain at least one white space.)  The corrected ABNF better follows practice in implementations.
```

</details>

<br>**Explanation:**
The erratum corrects the ABNF for the header-field, addressing a mismatch between the specification and observed implementations. The original ABNF is too restrictive, preventing valid header field values from being parsed. This inconsistency impacts implementations that parse Received-SPF header fields, leading to potential errors in processing.

---

<details>
<summary><b>Errata 4016</b> from <b>RFC 7210</b> - Database of Long-Lived Symmetric Cryptographic Keys (April 2014)</summary>

```
Section 2 says:


      SendLifetimeStart
         The SendLifetimeStart field specifies the earliest date and
         time in Coordinated Universal Time (UTC) at which this key
         should be considered for use when sending traffic.  The format
         is YYYYMMDDHHSSZ, where four digits specify the year, two
         digits specify the month, two digits specify the day, two
         digits specify the hour, two digits specify the minute, and two
         digits specify the second.  The "Z" is included as a clear
         indication that the time is in UTC.

      SendLifeTimeEnd
         The SendLifeTimeEnd field specifies the latest date and time at
         which this key should be considered for use when sending
         traffic.  The format is the same as the SendLifetimeStart
         field.

      AcceptLifeTimeStart
         The AcceptLifeTimeStart field specifies the earliest date and
         time in Coordinated Universal Time (UTC) at which this key
         should be considered for use when processing received traffic.
         The format is YYYYMMDDHHSSZ, where four digits specify the
         year, two digits specify the month, two digits specify the day,
         two digits specify the hour, two digits specify the minute, and
         two digits specify the second.  The "Z" is included as a clear
         indication that the time is in UTC.


It should say:

      SendLifetimeStart
         The SendLifetimeStart field specifies the earliest date and
         time in Coordinated Universal Time (UTC) at which this key
         should be considered for use when sending traffic.  The format
         is YYYYmmddHHMMSSZ, where four digits specify the year, two
         digits specify the month, two digits specify the day, two
         digits specify the hour, two digits specify the minute, and two
         digits specify the second.  The "Z" is included as a clear
         indication that the time is in UTC.

      SendLifeTimeEnd
         The SendLifeTimeEnd field specifies the latest date and time at
         which this key should be considered for use when sending
         traffic.  The format is the same as the SendLifetimeStart
         field.

      AcceptLifeTimeStart
         The AcceptLifeTimeStart field specifies the earliest date and
         time in Coordinated Universal Time (UTC) at which this key
         should be considered for use when processing received traffic.
         The format is YYYYmmddHHMMSSZ, where four digits specify the
         year, two digits specify the month, two digits specify the day,
         two digits specify the hour, two digits specify the minute, and
         two digits specify the second.  The "Z" is included as a clear
         indication that the time is in UTC.


Notes:

The date and time format in the original document omits minute even though the descriptive text indicates it should be included.
```

</details>

<br>**Explanation:**
The errata corrects the specified format for the date and time fields. The original specification omits the minutes field, which is inconsistent with the description. This inconsistency could lead to incorrect implementation and interpretation of the timestamps, directly affecting the functionality of the key management system.

---

<details>
<summary><b>Errata 4949</b> from <b>RFC 7252</b> - The Constrained Application Protocol (CoAP) (June 2014)</summary>

```
Section 5.10.7 says:


If any
of these reserved option numbers occurs in addition to Location-Path
and/or Location-Query and are not supported, then a 4.02 (Bad Option)
error MUST be returned.

It should say:

If any
of these reserved option numbers occurs in addition to Location-Path
and/or Location-Query and are not supported, then the response MUST
be rejected (Sections 4.2 and 4.3).

Notes:

The Location-* options are used in responses. A client cannot return a 4.02 (Bad Option) response in reply to a response. The correct behavior is to reject the response.
```

</details>

<br>**Explanation:**
The errata report corrects the handling of unsupported reserved option numbers in responses.  The original specification incorrectly states that a 4.02 (Bad Option) error MUST be returned, which is not possible for a client responding to a server. The correct behavior is to reject the response. This inconsistency impacts implementations that rely on the original specification to handle these responses correctly.

---

<details>
<summary><b>Errata 5078</b> from <b>RFC 7252</b> - The Constrained Application Protocol (CoAP) (June 2014)</summary>

```
Section 7.2.1 says:


The Content-Format code
attribute MAY include a space-separated sequence of Content-Format
codes, indicating that multiple content-formats are available.  The
syntax of the attribute value is summarized in the production "ct-
value" in Figure 12, where "cardinal", "SP", and "DQUOTE" are defined
as in [RFC6690].

It should say:

The Content-Format code
attribute MAY include a space-separated sequence of Content-Format
codes, indicating that multiple content-formats are available.
The Content-Format code attribute MUST NOT appear more than once in a 
link.  The syntax of the attribute value is summarized in the 
production "ct-value" in Figure 12, where "cardinal", "SP", and 
"DQUOTE" are defined as in [RFC6690].

Notes:

Insert a sentence that says that the code MUST NOT appear more than once.  This appears to be what was intended, but not stated, by the authors since it supports the space separated values to appear in a single attribute value.
```

</details>

<br>**Explanation:**
The original text does not explicitly prohibit multiple occurrences of the Content-Format attribute within a single link, while the space-separated sequence implies that multiple content formats can be specified within a single attribute value. This creates an inconsistency and ambiguity in how the Content-Format attribute should be used. The correction clarifies that the attribute MUST NOT appear more than once, resolving the ambiguity.

---

<details>
<summary><b>Errata 4450</b> from <b>RFC 7273</b> - RTP Clock Source Signalling (June 2014)</summary>

```
Section 4.8 says:


  ; PTP domain allowed characters: 0x21-0x7E (IEEE 1588-2002)
   ptp-domain-name = "domain-name=" 1*16ptp-domain-char
   ptp-domain-char = %x21-7E

   ; PTP domain allowed number range: 0-127 (IEEE 1588-2008)
   ptp-domain-nmbr = "domain-nmbr=" ptp-domain-dgts
   ptp-domain-dgts = ptp-domain-n1 / ptp-domain-n2 / ptp-domain-n3
   ptp-domain-n1   = DIGIT             ; 0-9
   ptp-domain-n2   = POS-DIGIT DIGIT   ; 10-99
   ptp-domain-n3   = ("10"/"11") DIGIT ; 100-119
                   / "12" %x30-37      ; 120-127


It should say:

   ; PTP domain allowed characters: 0x21-0x7E (IEEE 1588-2002)
   ptp-domain-name = 1*16ptp-domain-char
   ptp-domain-char = %x21-7E

   ; PTP domain allowed number range: 0-127 (IEEE 1588-2008)
   ptp-domain-nmbr = ptp-domain-dgts
   ptp-domain-dgts = ptp-domain-n1 / ptp-domain-n2 / ptp-domain-n3
   ptp-domain-n1   = DIGIT             ; 0-9
   ptp-domain-n2   = POS-DIGIT DIGIT   ; 10-99
   ptp-domain-n3   = ("10"/"11") DIGIT ; 100-119
                   / "12" %x30-37      ; 120-127


Notes:

There is an inconsistency between ABNF in section 4.8 and examples in section 5.5. Due to evidence that current implementations are working to what is shown in the examples, this is resolved by updating the ABNF specification.
```

</details>

<br>**Explanation:**
The original ABNF for ptp-domain-name and ptp-domain-nmbr includes unnecessary prefixes ("domain-name=" and "domain-nmbr="). The correction removes these prefixes, making the ABNF consistent with the examples provided in Section 5.5 and the actual practice of implementations. This inconsistency would affect parsers that strictly adhere to the original ABNF.

---

<details>
<summary><b>Errata 6940</b> from <b>RFC 7296 a.k.a. STD 79</b> - Internet Key Exchange Protocol Version 2 (IKEv2) (October 2014)</summary>

```
Section .10 says:


o SPI Size (1 octet) - Length in octets of the SPI as defined by the
 IPsec protocol ID or zero if no SPI is applicable. For a
 notification concerning the IKE SA, the SPI Size MUST be zero and
 the field must be empty.


It should say:

o SPI Size (1 octet) - Length in octets of the SPI as defined by the
 IPsec protocol ID or zero if no SPI is applicable. For a
 notification concerning the IKE SA, the SPI Size MUST be zero and
 the SPI field must be empty.


Notes:

the field must be empty -> the SPI field must be empty

additional question: so for a notification concerning the IKE SA, the Protocol ID field still shall be zero?

Yes, for IKE SA notifications the SPI can be seen from the header, thus there is no point of repeating the SPIs in notify payload. The Protocol ID field of the notification payload indicates which type of SPI is inside the notification payload, thus if there is no SPI in there, then there is no point of having Protocol ID either.
```

</details>

<br>**Explanation:**
The original text states that the SPI field must be empty for IKE SA notifications but doesn't explicitly mention the SPI Size field. The correction clarifies that the SPI field MUST be empty for IKE SA notifications, resolving the inconsistency and ensuring that both the SPI Size and SPI fields are correctly handled. The original description leaves room for misinterpretation of whether only the SPI field or both the SPI and SPI Size fields should be handled in the IKE SA notification.

---

<details>
<summary><b>Errata 4380</b> from <b>RFC 7361</b> - LDP Extensions for Optimized MAC Address Withdrawal in a Hierarchical Virtual Private LAN Service (H-VPLS) (September 2014)</summary>

```
Section 5.2 says:


   At least one of the following sub-TLVs MUST be included in the MAC
   Flush Parameters TLV if the C-flag is set to 1:

   o  PBB B-MAC List Sub-TLV:

      Type: 0x0407

      Length: Value length in octets.  At least one B-MAC address MUST
      be present in the list.

      Value: One or a list of 48-bit B-MAC addresses.  These are the
      source B-MAC addresses associated with the B-VPLS instance that
      originated the MAC withdraw message.  It will be used to identify
      the C-MAC(s) mapped to the B-MAC(s) listed in the sub-TLV.

   o  PBB I-SID List Sub-TLV:

      Type: 0x0408

      Length: Value length in octets.  Zero indicates an empty I-SID
      list.  An empty I-SID list means that the flushing applies to all
      the I-SIDs mapped to the B-VPLS indicated by the FEC TLV.

      Value: One or a list of 24-bit I-SIDs that represent the
      I-component FIB(s) where the MAC flushing needs to take place.

It should say:

   At least one of the following sub-TLVs MUST be included in the MAC
   Flush Parameters TLV if the C-flag is set to 1:

   o  PBB B-MAC List Sub-TLV:

      Type: 0x01
      Length: Value length in octets.  At least one B-MAC address MUST
      be present in the list.

      Value: One or a list of 48-bit B-MAC addresses.  These are the
      source B-MAC addresses associated with the B-VPLS instance that
      originated the MAC withdraw message.  It will be used to identify
      the C-MAC(s) mapped to the B-MAC(s) listed in the sub-TLV.

   o  PBB I-SID List Sub-TLV:

      Type: 0x02
      Length: Value length in octets.  Zero indicates an empty I-SID
      list.  An empty I-SID list means that the flushing applies to all
      the I-SIDs mapped to the B-VPLS indicated by the FEC TLV.

      Value: One or a list of 24-bit I-SIDs that represent the
      I-component FIB(s) where the MAC flushing needs to take place.

Notes:

Type definition was error. The PBB B-MAC List Sub-TLV abd I-SID List Sub-TLV are only support for one byte, as defined in section 5.1.1 MAC flush parameters TLV.
This error was imported from draft-ietf-l2vpn-vpls-ldp-mac-opt-12. For this version, it submit the 2 sub-tlv to IANA for alloc id. But the two kinds tlv were sub-tlv, not LDP TLV
```

</details>

<br>**Explanation:**
The original text uses incorrect Type values (0x0407 and 0x0408) for the PBB sub-TLVs. The correction provides the correct Type values (0x01 and 0x02), resolving the inconsistency.  This inconsistency would directly affect implementations that rely on the original, incorrect Type values, rendering them unable to correctly interpret and process the PBB sub-TLVs.

---

<details>
<summary><b>Errata 4212</b> from <b>RFC 7366</b> - Encrypt-then-MAC for Transport Layer Security (TLS) and Datagram Transport Layer Security (DTLS) (September 2014)</summary>

```
Section 3 says:


   In TLS [2] notation, the MAC calculation for TLS 1.0 without
   the explicit Initialization Vector (IV) is:

   MAC(MAC_write_key, seq_num +
       TLSCipherText.type +
       TLSCipherText.version +
       TLSCipherText.length +
       ENC(content + padding + padding_length));

   and for TLS 1.1 and greater with an explicit IV is:

   MAC(MAC_write_key, seq_num +
       TLSCipherText.type +
       TLSCipherText.version +
       TLSCipherText.length +
       IV +
       ENC(content + padding + padding_length));


It should say:

Note that the length value used for the MAC computation differs from 
the value of the 'uint16 length' field in the TLSCiphertext record as 
encoded on the wire.  The encoded TLSCiphertext record contains both 
the ciphtertext and the MAC, while the MAC calculation is performed 
only over the ciphertext.  The length value encoded in the 
TLSCiphertext record is therefore 'length' while the length value 
used in the MAC calculation is 'length - SecurityParameters.mac_length'.

More formally, if:

  TLSCiphertext.enc_content = ENC(content + padding + padding_length)

then in TLS notation the MAC calculation for TLS 1.0 without the 
explicit Initialization Vector (IV) is:

   MAC(MAC_write_key, seq_num +
       TLSCipherText.type +
       TLSCipherText.version +
       length of (TLSCiphertext.enc_content) +
       TLSCiphertext.enc_content);

and for TLS 1.1 and greater with an explicit IV is:

   MAC(MAC_write_key, seq_num +
       TLSCipherText.type +
       TLSCipherText.version +
       length of (IV + TLSCiphertext.enc_content) +
       IV +
       TLSCiphertext.enc_content);


Notes:

After the RFC was published a new set of implementers (who hadn't been part of the pre-publication interop testing) pointed out that the text covering the use of length values could be interpreted in two different ways.  This correction attempts to remove the ambiguity by making explicit what's MACd vs. what's encoded on the wire.
```

</details>

<br>**Explanation:**
The errata corrects the description of the length value used in the MAC calculation for TLS. The original description used the length of the entire TLSCipherText record, which includes both the ciphertext and the MAC, whereas the MAC calculation should only include the ciphertext length. This inconsistency could lead to incorrect MAC calculations. The corrected description clarifies that the length used for MAC calculation is the length of the ciphertext only, resolving the ambiguity.

---

<details>
<summary><b>Errata 4297</b> from <b>RFC 7394</b> - Definition of Time to Live TLV for LSP-Ping Mechanisms (November 2014)</summary>

```
Section 3.1 says:


3.1. TTL TLV Format


   0                   1                   2                   3
   0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  Type = 32769                 |   Length = 8                  |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |   Value       |   Reserved    |   Flags                       |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

                  Figure 1: Time To Live TLV Format

It should say:

3.1. TTL TLV Format


   0                   1                   2                   3
   0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  Type = 32769                 |   Length = 4                  |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |   Value       |   Reserved    |   Flags                       |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

                  Figure 1: Time To Live TLV Format

Notes:

In an LSP Ping TTL, Length value should show length of the value fields only. See RFC 4379 section 3.
```

</details>

<br>**Explanation:**
The original specification incorrectly defines the Length field as 8 octets. The correction sets it to 4 octets, aligning with RFC 4379, which mandates that the Length field in TLVs only includes the size of the value. This inconsistency would lead to incorrect interpretation and processing of the Time To Live TLV.

---

<details>
<summary><b>Errata 4408</b> from <b>RFC 7401</b> - Host Identity Protocol Version 2 (HIPv2) (April 2015)</summary>

```
Section 4.4.4 says:


     .   +---------+  recv I2, send R2                       |         |
   +---->| I1-SENT |--------------------------------------+  |         |
   |     +---------+            +----------------------+  |  |         |
   |          | recv R2,        | recv I2, send R2     |  |  |         |
   |          v send I2         |                      v  v  v         |
   |       +---------+          |                    +---------+       |
   |  +--->| I2-SENT |----------+     +--------------| R2-SENT |<---+  |
   |  |    +---------+                |              +---------+    |  |

It should say:

     .   +---------+  recv I2, send R2                       |         |
   +---->| I1-SENT |--------------------------------------+  |         |
   |     +---------+            +----------------------+  |  |         |
   |          | recv R1,        | recv I2, send R2     |  |  |         |
   |          v send I2         |                      v  v  v         |
   |       +---------+          |                    +---------+       |
   |  +--->| I2-SENT |----------+     +--------------| R2-SENT |<---+  |
   |  |    +---------+                |              +---------+    |  |

Notes:

This state machine figure is informative.  Normative (correct) specification for the I1-SENT to I2-SENT state transition (due to recv R1 event) is in Section 6.8.
```

</details>

<br>**Explanation:**
The errata corrects a state machine diagram, showing an incorrect transition from I1-SENT to I2-SENT.  The original diagram incorrectly shows a transition upon reception of R2, while the correct behavior is a transition upon reception of R1 (as specified in Section 6.8). This inconsistency affects the understanding and implementation of the HIPv2 state machine.

---

<details>
<summary><b>Errata 6654</b> from <b>RFC 7401</b> - Host Identity Protocol Version 2 (HIPv2) (April 2015)</summary>

```
Section 5.3.3 says:


   If present in the I1 packet, the Initiator MUST include an unmodified
   copy of the R1_COUNTER parameter received in the corresponding R1
   packet into the I2 packet.


It should say:

   If present in the R1 packet, the Initiator MUST include an unmodified
   copy of the R1_COUNTER parameter received in the corresponding R1
   packet into the I2 packet.


Notes:

Packet name error, must be R1
```

</details>

<br>**Explanation:**
The errata corrects a statement about the source of the R1_COUNTER parameter. The original text incorrectly stated that the parameter must be included in the I2 packet if it was present in the I1 packet. The correct source for the R1_COUNTER parameter is the R1 packet. This inconsistency affects the implementation of the HIPv2 protocol.

---

<details>
<summary><b>Errata 4508</b> from <b>RFC 7468</b> - Textual Encodings of PKIX, PKCS, and CMS Structures (April 2015)</summary>

```
Section 3 says:


  preeb      = "-----BEGIN " label "-----" ; unlike [RFC1421] (A)BNF,
                                           ; eol is not required (but
  posteb     = "-----END " label "-----"   ; see [RFC1421], Section 4.4)


It should say:

  preeb      = "-----" %x42.45.47.49.4E " " label "-----" 

  posteb     = "-----" %x45.4E.44 " " label"-----"
                         ; unlike [RFC1421] (A)BNF, eol is not required
                         ; (but see [RFC1421], Section 4.4)

OR:

  preeb      = %s"-----BEGIN " label "-----" ; unlike [RFC1421] (A)BNF,
                                             ; eol is not required (but
  posteb     = %s"-----END " label "-----"   ; see [RFC1421],
                                             ; Section 4.4)

...with reference to RFC 7405.

Notes:

The encapsulation boundaries are case-sensitive, including (especially) the BEGIN and END characters. Nearly all implementations enforce the case sensitivity of BEGIN and END on input, and all surveyed implementations output all-caps.
```

</details>

<br>**Explanation:**
The original ABNF for preeb and posteb does not correctly enforce the case sensitivity of the BEGIN and END keywords. The correction uses hexadecimal notation to explicitly specify the uppercase characters, ensuring that implementations correctly handle case sensitivity.  The original ABNF is inconsistent with the actual behavior of implementations and the case sensitivity requirements of the specified encoding.

---

<details>
<summary><b>Errata 4503</b> from <b>RFC 7483</b> - JSON Responses for the Registration Data Access Protocol (RDAP) (March 2015)</summary>

```
Section 5.2 and 5.3 says:


In Section 5.2:

"ldhName" : "ns1.xn--fo-5ja.example",
"unicodeName" : "ns1.foo.example",

In Section 5.3:

"ldhName" : "xn--fo-5ja.example",
"unicodeName" : "foo.example",

"ldhName" : "xn--fo-cka.example",
"unicodeName" : "foo.example"

"ldhName" : "xn--fo-fka.example",
"unicodeName" : "foo.example"

"ldhName": "xn--fo-8ja.example",
"unicodeName" : "foo.example"

It should say:

In Section 5.2:

"ldhName" : "ns1.xn--fo-5ja.example",
"unicodeName" : "ns1.fóo.example",

In Section 5.3:

"ldhName" : "xn--fo-5ja.example",
"unicodeName" : "fóo.example",

"ldhName" : "xn--fo-cka.example",
"unicodeName" : "fõo.example"

"ldhName" : "xn--fo-fka.example",
"unicodeName" : "föo.example"

"ldhName" : "xn--fo-8ja.example",
"unicodeName" : "fôo.example"

Notes:

The unicodeName examples in RFC 7483 are invalid per RFC 5890. Here's an example from Section 5.2 on page 23:

"unicodeName" : "ns1.foo.example",

Section 3 of 7483 says this about Unicode names:

"Unicode names: Textual representations of DNS names where one or more of the labels are U-labels as described by [RFC5890]."

5890 says: "A "U-label" is an IDNA-valid string of Unicode characters, in Normalization Form C (NFC) and including at least one non-ASCII character, expressed in a standard Unicode Encoding Form (such as UTF-8)."

The examples in 7483 contain all ASCII characters. Syntactically valid examples are shown in the corrected text.
```

</details>

<br>**Explanation:**
The original examples for unicodeName in sections 5.2 and 5.3 use only ASCII characters, which contradicts the definition in Section 3 and RFC 5890, requiring at least one non-ASCII character. The correction provides examples that correctly include non-ASCII characters, resolving the inconsistency.  This inconsistency would lead to implementations that incorrectly handle unicodeName values containing non-ASCII characters.

---

<details>
<summary><b>Errata 4980</b> from <b>RFC 7483</b> - JSON Responses for the Registration Data Access Protocol (RDAP) (March 2015)</summary>

```
Section 5.5 says:


country -- a string containing the name of the two-character
country code of the autnum

It should say:

country -- a string containing the two-character country
code of the autnum


Notes:

As described in Section 3, country codes should consistently be represented as two-character string values. Note that this differs from the "full name" format used in jCard representations of entity objects.
```

</details>

<br>**Explanation:**
The errata corrects the description of the `country` field. The original description referred to a "two-character country code" as a string containing the name of the country code, which is inconsistent. The corrected description clarifies that `country` should be a two-character string representing the country code, matching the definition in section 3.

---

<details>
<summary><b>Errata 6158</b> from <b>RFC 7483</b> - JSON Responses for the Registration Data Access Protocol (RDAP) (March 2015)</summary>

```
Section 10.2.3 says:


Description: The object instance was transferred from one registrant to another.

It should say:

Description: The object instance was transferred from one registrar to another.

Notes:

I believe the corrected text is what was intended for this particular registry value, and is what is being implemented by operators today. Registrant-to-registrant transfers are also possible, but they're not performed using EPP and are not logged as an event action. The text in the RFC should be changed and the description of the action in the IANA registry should also be changed.
```

</details>

<br>**Explanation:**
The original description uses the term "registrant", which is incorrect in the context of EPP object transfers. The correction uses the term "registrar", which aligns with the intended meaning of object transfers performed using EPP and is consistent with current implementations. The inconsistency would lead to misinterpretations of the event action.

---

<details>
<summary><b>Errata 4471</b> from <b>RFC 7530</b> - Network File System (NFS) Version 4 Protocol (March 2015)</summary>

```
Section 16.10.4. says:


   In the case that the lock is denied, the owner, offset, and length of
   a conflicting lock are returned.

It should say:

   In the case that the lock is denied, the owner, offset, length, and
   type of a conflicting lock are returned.

Notes:

The locktype in LOCK4denied is not specified for the LOCK operation.  See 16.11.4. for similar wording for LOCKT.
```

</details>

<br>**Explanation:**
The original description omits the lock type in the LOCK4denied response when a lock is denied. This is inconsistent with the description of LOCKT in section 16.11.4, which includes the lock type. The omission leads to incomplete information in the response, making it inconsistent and affecting implementations that depend on having complete information about the conflicting lock.

---

<details>
<summary><b>Errata 8105</b> from <b>RFC 7542</b> - The Network Access Identifier (May 2015)</summary>

```
Section 3.4 says:


Examples of valid Network Access Identifiers include the following:
[...]
        \(user\)@example.net

It should say:

Examples of invalid Network Access Identifiers include the following:
[...]
        \(user\)@example.net

Notes:

\(user\)@example.net is listed as a valid example, but neither backslashes nor parentheses are allowed in the ABNF rules (sections 2.1 and 2.2).  Obsoleted RFC 4282 had ABNF rules to allow for backslash escapes, but RFC 7542 does not.  These are the only backslashes in the entire document.

Perhaps this example should be moved to the invalid examples list?

Or perhaps the ABNF rules should be extended to allow some forms of backslash escapes, although probably not to the same wide-open extent as RFC 4282?
```

</details>

<br>**Explanation:**
The errata report identifies an example of a NAI that is listed as valid but violates the ABNF rules specified in sections 2.1 and 2.2. This inconsistency between the examples and the ABNF rules could lead to incorrect implementations. The inconsistency needs to be resolved either by correcting the example or updating the ABNF rules.

---

<details>
<summary><b>Errata 4724</b> from <b>RFC 7574</b> - Peer-to-Peer Streaming Peer Protocol (PPSPP) (July 2015)</summary>

```
Section 1.3 says:


swarm ID
Unique identifier for a swarm of peers, in PPSPP a sequence of
bytes. For video on demand with content integrity protection
enabled, the identifier is the so-called root hash of a Merkle
hash tree over the content. For live streaming, the swarm ID is
a public key.

It should say:

swarm ID
Unique identifier for a swarm of peers, in PPSPP a sequence of
bytes. For video on demand, the identifier is the so-called root hash
of a Merkle hash tree over the content. For live streaming, the 
swarm ID is a public key.

Notes:

According to chapter 5 and chapter 6.1, it seems that it is not mandatory to use content integrity protection scheme.
The definition of swarm ID in the original text does not define how the ID is used in environment with the content integrity protection disabled.
It is possible to add new description on how swarm ID is defined in the content integrity protection scheme is disabled. 
Or, it is possible to remove the parts regarding content integrity protection.

We propose to remove "with content integrity protection enabled" part.

Spencer: confirmed in conversations with Victor Grishchenko <victor.grishchenko@gmail.com> on the PPSP mailing list.
```

</details>

<br>**Explanation:**
The original description of swarm ID is inconsistent with the specification in chapters 5 and 6.1, which do not mandate content integrity protection.  The original text implies that the swarm ID is only defined when content integrity protection is enabled, while it should be defined regardless. The corrected description removes the reference to content integrity protection, addressing this inconsistency.

---

<details>
<summary><b>Errata 4880</b> from <b>RFC 7574</b> - Peer-to-Peer Streaming Peer Protocol (PPSPP) (July 2015)</summary>

```
Section 7.5 says:


   A peer MUST include the content integrity method used by a swarm.
   The code for this option is 3.  Defined values are listed in Table 4.

                   +--------+-------------------------+
                   | Method | Description             |
                   +--------+-------------------------+
                   | 0      | No integrity protection |
                   | 1      | Merkle Hash Tree        |
                   | 2      | Sign All                |
                   | 3      | Unified Merkle Tree     |
                   | 4-255  | Unassigned              |
                   +--------+-------------------------+

            Table 4: PPSPP Content Integrity Protection Methods

It should say:

   A peer MUST include the content integrity method used by a swarm.
   The code for this option is 3.  Defined values are listed in Table 4.

                   +--------+-------------------------+
                   | Method | Description             |
                   +--------+-------------------------+
                   | 0      | Unassigned              |
                   | 1      | Merkle Hash Tree        |
                   | 2      | Sign All                |
                   | 3      | Unified Merkle Tree     |
                   | 4-255  | Unassigned              |
                   +--------+-------------------------+

            Table 4: PPSPP Content Integrity Protection Methods

Notes:

As stated in the first sentence of chapter 7.5, “A peer MUST include the content integrity method used by a swarm.”, “No integrity protection” must not be one of the option for PPSPP content integrity protection method. Or, IETF 7574 must define PPSP-PP that does not use the integrity protection method.

The proposed is to remove option of “No integrity protection”  in Table 4.

Spencer: confirmed in conversations with Victor Grishchenko <victor.grishchenko@gmail.com> on the PPSP mailing list.
```

</details>

<br>**Explanation:**
The original text includes "No integrity protection" as a defined content integrity method, while the requirement that a peer MUST include the content integrity method used by a swarm makes this option contradictory.  The correction removes this option, resolving the inconsistency. This inconsistency would lead to implementations allowing for undefined behavior.

---

<details>
<summary><b>Errata 4676</b> from <b>RFC 7578</b> - Returning Values from Forms: multipart/form-data (July 2015)</summary>

```
Section 4.6. says:


       --AaB03x
       content-disposition: form-data; name="_charset_"

       iso-8859-1
       --AaB03x--
       content-disposition: form-data; name="field1"

       ...text encoded in iso-8859-1 ...
       AaB03x--

It should say:

       --AaB03x
       content-disposition: form-data; name="_charset_"

       iso-8859-1
       --AaB03x
       content-disposition: form-data; name="field1"

       ...text encoded in iso-8859-1 ...
       --AaB03x--

Notes:

Boundary hyphens were misplaced, I think.  The second boundary delimiter should not have them on the end of the line, and the last boundary delimiter should have them on the beginning of the line too.
```

</details>

<br>**Explanation:**
The original example incorrectly places boundary hyphens, resulting in an invalid multipart/form-data message. The corrected version correctly positions the boundary hyphens, ensuring a valid message format. This inconsistency could lead to implementations incorrectly parsing or generating multipart/form-data messages.

---

<details>
<summary><b>Errata 4865</b> from <b>RFC 7598</b> - DHCPv6 Options for Configuration of Softwire Address and Port-Mapped Clients (July 2015)</summary>

```
Section 4.3 says:


dmr-prefix6-len: 8 bits long; expresses the bitmask length of the 
IPv6 prefix specified in the dmr-ipv6-prefix field.  Allowed
values range from 0 to 128.

It should say:

dmr-prefix6-len: 8 bits long; expresses the bitmask length of the 
IPv6 prefix specified in the dmr-ipv6-prefix field.  Allowed
values range from 0 to 96.

Notes:

This field is used to provision the default mapping rule prefix length, which is defined in section 5.1 of RFC7599:
The DMR IPv6 prefix length SHOULD be 64 bits long by default and in any case MUST NOT exceed 96 bits.
```

</details>

<br>**Explanation:**
The original specification allows values up to 128 for the `dmr-prefix6-len` field, while RFC 7599 limits the maximum length to 96. This inconsistency needs to be resolved to ensure that implementations conform to both specifications. The corrected range is consistent with RFC 7599.

---

<details>
<summary><b>Errata 5225</b> from <b>RFC 7599</b> - Mapping of Address and Port using Translation (MAP-T) (July 2015)</summary>

```
Section 6 says:


In the case of an IPv4 prefix, the IPv4 address field is right-padded
with zeros up to 32 bits.  The PSID is left-padded with zeros to
create a 16-bit field.  For an IPv4 prefix or a complete IPv4
address, the PSID field is zero.

It should say:

The PSID is left-padded with zeros to
create a 16-bit field.  For an IPv4 prefix or a complete IPv4
address, the PSID field is zero.

Notes:

This text has been copied from RFC7597 (MAP-E). While it is correct in the context of MAP-E, for MAP-T the complete IPv4 source address must be embedded in the interface-identifier for correct translation in the case of an IPv4 prefix. Right padding the prefix with zeroes would lead to the translated packet having all zeroes in its source address.
```

</details>

<br>**Explanation:**
The original description for MAP-T incorrectly states that the IPv4 address field is right-padded with zeros, while the correct behavior is to embed the complete IPv4 source address in the interface-identifier. This inconsistency is due to the text being copied from MAP-E where it is correct, but incorrect for MAP-T.  This inconsistency would lead to incorrect translation of IPv4 packets.

---

<details>
<summary><b>Errata 5324</b> from <b>RFC 7599</b> - Mapping of Address and Port using Translation (MAP-T) (July 2015)</summary>

```
Section Appendix A says:


Example 5:

PSID:                    0x20 (provisioned with DHCPv6)

It should say:

Example 5:

PSID:                    0x34 (provisioned with DHCPv6)

Notes:

In IPv4, IPv6 and port ranges presented in the example the PSID matches to 0x34 and not 0x20:

   PSID:                    0x34
   Available ports (63 ranges): 1232-1235, 2256-2259, ...... ,
                                63696-63699, 64720-64723
   IPv6 address of MAP CE:  2001:db8:0012:3400:0000:c000:0212:0034
```

</details>

<br>**Explanation:**
The original example uses an incorrect PSID value (0x20). The correction provides the correct PSID value (0x34), making the example consistent with the provided IPv6 address and port ranges. This inconsistency would lead to confusion in interpreting the example and implementing the specification correctly.

---

<details>
<summary><b>Errata 7160</b> from <b>RFC 7599</b> - Mapping of Address and Port using Translation (MAP-T) (July 2015)</summary>

```
Section 10.1 says:


Translating an IPv4 packet to carry it across the MAP domain will increase its size (typically by 20 bytes).

It should say:

Translating an IPv4 packet to carry it across the MAP domain will increase its size (typically either 20 or 28 bytes with fragmentation).

Notes:

In the context of MTU, it is important to account for packet fragmentation. If an IPv4 packet is fragmented, the size will increase by 28 bytes during translation. The IPv6 header is 20 bytes larger than the IPv4 header, and in addition the 8 byte IPv6 Fragmentation Header must be added.

----
Verifier note
==========
 with help of Yong Cui: fragmentation indeed needs to be taken into account.
```

</details>

<br>**Explanation:**
The original text only considers the size increase without fragmentation, while fragmentation can also occur, leading to a different size increase.  The correction accounts for both scenarios, providing a more complete and accurate description of the size increase during translation. This inconsistency would lead to incorrect calculations of the size of translated packets.

---

<details>
<summary><b>Errata 5687</b> from <b>RFC 7636</b> - Proof Key for Code Exchange by OAuth Public Clients (September 2015)</summary>

```
Section 5 says:


Server implementations of this specification MAY accept OAuth2.0
clients that do not implement this extension.  If the "code_verifier"
is not received from the client in the Authorization Request, servers
supporting backwards compatibility revert to the OAuth 2.0 [RFC6749]
protocol without this extension.

As the OAuth 2.0 [RFC6749] server responses are unchanged by this
specification, client implementations of this specification do not
need to know if the server has implemented this specification or not
and SHOULD send the additional parameters as defined in Section 4 to
all servers.


It should say:

Server implementations of this specification MAY accept OAuth2.0
clients that do not implement this extension.  If the "code_challenge"
is not received from the client in the Authorization Request, servers
supporting backwards compatibility revert to the OAuth 2.0 [RFC6749]
protocol without this extension.

As the OAuth 2.0 [RFC6749] server responses are unchanged by this
specification, client implementations of this specification do not
need to know if the server has implemented this specification or not
and SHOULD send the additional parameters as defined in Section 4 to
all servers.


Notes:

The code_verifier is not sent in the authorization request.
```

</details>

<br>**Explanation:**
The original text refers to "code_verifier" when describing the parameter that may be absent in an authorization request. However, the specification defines "code_challenge" as the parameter sent in the request, and "code_verifier" as the parameter sent later in the token request.  This inconsistency affects implementations that need to correctly handle the absence of the code_challenge parameter.

---

<details>
<summary><b>Errata 4549</b> from <b>RFC 7683</b> - Diameter Overload Indication Conveyance (October 2015)</summary>

```
Section 4.3 says:


The overloaded realm is identified by the Destination-Realm AVP 
of the message containing the OLR.

It should say:

The overloaded realm is identified by the Origin-Realm AVP
of the message containing the OLR.

Notes:

When the overload report is of type "REALM_REPORT", the overloaded realm is identified by the Origin-Realm AVP of the Diameter command i.e. the realm of the originator of the Diameter command with the overload report.
```

</details>

<br>**Explanation:**
The original text incorrectly identifies the Destination-Realm AVP as the identifier of the overloaded realm in an Overload Indication message. The correct AVP to identify the overloaded realm is the Origin-Realm AVP.  This inconsistency affects the interpretation and implementation of the Diameter Overload Indication Conveyance mechanism.

---

<details>
<summary><b>Errata 8104</b> from <b>RFC 7684</b> - OSPFv2 Prefix/Link Attribute Advertisement (November 2015)</summary>

```
Section 2.1 says:


   Route Type
      The type of the OSPFv2 route.  If the route type is 0
      (Unspecified), the information inside the OSPFv2 External Prefix
      TLV applies to the prefix regardless of prefix's route type.  This
      is useful when prefix-specific attributes are advertised by an
      external entity that is not aware of the route type associated
      with the prefix.  Supported types are:

It should say:

   Route Type
      The type of the OSPFv2 route.  If the route type is 0
      (Unspecified), the information inside the OSPFv2 Extended Prefix
      TLV applies to the prefix regardless of prefix's route type.  This
      is useful when prefix-specific attributes are advertised by an
      external entity that is not aware of the route type associated
      with the prefix.  Supported types are:

Notes:

s/External Prefix/Extended Prefix/
```

</details>

<br>**Explanation:**
The original text incorrectly refers to "OSPFv2 External Prefix TLV", while the correct term is "OSPFv2 Extended Prefix TLV". This inconsistency creates a mismatch between the description and the actual TLV used, affecting the correct interpretation and implementation of the specification.

---

<details>
<summary><b>Errata 5342</b> from <b>RFC 7761 a.k.a. STD 83</b> - Protocol Independent Multicast - Sparse Mode (PIM-SM): Protocol Specification (Revised) (March 2016)</summary>

```
Section 4.4.2 says:


set KeepaliveTimer(S,G) to RP_Keepalive_Period;

It should say:

set KeepaliveTimer(S,G) to max(Keepalive_Period, RP_Keepalive_Period);

Notes:

The normal keepalive period for the KAT(S,G) defaults to 210 seconds. However, at the RP, the keepalive period must be at least the Register_Suppression_Time, or the RP may time out the (S,G) state before the next Null-Register arrives. Thus, the KAT(S,G) is set to max(Keepalive_Period, RP_Keepalive_Period) when a Register-Stop is sent.

====
Note that the text above comes from §4.11.
```

</details>

<br>**Explanation:**
The original specification sets the KeepaliveTimer to RP_Keepalive_Period, which may be shorter than the actual keepalive period. This inconsistency can lead to premature timeouts. The corrected specification uses the maximum of Keepalive_Period and RP_Keepalive_Period, ensuring that the timer is long enough to avoid premature timeouts.

---

<details>
<summary><b>Errata 4677</b> from <b>RFC 7788</b> - Home Networking Control Protocol (April 2016)</summary>

```
Section 8 says:


   A network-wide
   zone is appended to all single labels or unqualified zones in order
   to qualify them. ".home" is the default; however, an administrator
   MAY configure the announcement of a Domain-Name TLV (Section 10.6)
   for the network to use a different one.

It should say:

   A network-wide
   zone is appended to all single labels or unqualified zones in order 
   to qualify them.  A default value for this TLV MUST be set, although 
   the default value of the Domain-Name TLV (Section 10.6) is out of 
   scope of this document, and an administrator MAY configure the 
   announcement of a Domain-Name TLV for the network.

Notes:

It may appear that the use of the label ".home" is unofficially assigning this to be added to the Special Use Domain Registry. That registry can only be updated using the process outlined in RFC6761, therefore the text identifying ".home" as the default network-wide zone is in error.

It is unclear of the IESG and the IETF in publishing this proposed standard if the intent was to use ".home" as an example or placeholder until a name can be reserved.

AD Note: A default label is a requirement for HNCP and its interoperability. As such the Homenet chosen label, ".home", is a strong candidate for the RFC6761 process. The WG will be directed to follow this process and seek (again) the consensus on the ".home" label and work with other IETF WGs as appropriate.
```

</details>

<br>**Explanation:**
The original text states that ".home" is the default network-wide zone, implying that this value is implicitly defined.  The correction clarifies that a default value MUST be set but that the specific default value is out of scope of this document, thus removing the implicit definition of ".home" as the default.  This inconsistency could lead to implementations using ".home" as the default without proper consideration of the process for defining such values.

---

<details>
<summary><b>Errata 5021</b> from <b>RFC 7788</b> - Home Networking Control Protocol (April 2016)</summary>

```
RFC 7787 (DNCP) in section 9 defines DNCP_NODE_IDENTIFIER_LENGTH as being bytes, not bits.

-- Verifier note --
Indeed, section 9 of RFC 7787 clearly specifies "DNCP_NODE_IDENTIFIER_LENGTH: The fixed length of a node identifier (in bytes)."
```

</details>

<br>**Explanation:**
RFC 7788 incorrectly describes DNCP_NODE_IDENTIFIER_LENGTH as bits when RFC 7787 defines it as bytes. This inconsistency creates a conflict between the two specifications, leading to potential incompatibility between implementations.

---

<details>
<summary><b>Errata 5113</b> from <b>RFC 7788</b> - Home Networking Control Protocol (April 2016)</summary>

```
Section 10 says:


10.2.2.  DHCPv6-Data TLV

    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |    Type: DHCPv6-Data (37)     |          Length: > 0          |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

[...]

10.2.3.  DHCPv4-Data TLV

    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |     Type: DHCPv4-Data (38)    |          Length: > 0          |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+


It should say:

10.2.2.  DHCPv6-Data TLV

    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |    Type: DHCPv6-Data (38)     |          Length: > 0          |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

[...]

10.2.3.  DHCPv4-Data TLV

    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |     Type: DHCPv4-Data (37)    |          Length: > 0          |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+


Notes:

Section 13 (IANA Considerations) of the document says:

      37: DHCPv4-Data

      38: DHCPv6-Data

Those code points from Section 13 are in the "HNCP TLV Types" IANA registry as well as in the current source code of shncpd and tcpdump. The code points shown in Sections 10.2.2 and 10.2.3 were likely swapped by mistake.

-- Verifier note --
The IANA registry for HNCP TLV types (https://www.iana.org/assignments/dncp-registry/dncp-registry.xhtml#hncp-tlv-types) has indeed 37 for DHCPv4 and the open source SHNCPD has the same https://github.com/jech/shncpd/blob/master/receive.c
```

</details>

<br>**Explanation:**
The Type values for DHCPv4-Data and DHCPv6-Data TLVs are swapped in Section 10.  This inconsistency is between the values shown in Section 10 and the values defined in Section 13 and the IANA registry.  This inconsistency would affect implementations parsing or generating these TLVs.

---

<details>
<summary><b>Errata 7016</b> from <b>RFC 7839</b> - Access-Network-Identifier Option in DHCP (June 2016)</summary>

```
Section 4.4.1 says:


   Length
      4

   Operator-Identifier
      The Operator-Identifier is a variable-length Private Enterprise
      Number (PEN) ...

It should say:

   Length
      4

   Operator-Identifier
      The Operator-Identifier is a 32-bit Private Enterprise
      Number (PEN) ...

Notes:

Either the length is 4, and the contents are 32-bits.  Or the length is >1, and the length is variable.

My guess is that the intention is to have a fixed length.  The variable-length encoding from RFC 6757 is likely not needed here.


*** verifier note ***
See Bernie Volz's reply in https://mailarchive.ietf.org/arch/msg/dhcwg/Y4yaYwaqxS0B2nWw5f4xER2fSMk/
```

</details>

<br>**Explanation:**
The description of the Operator-Identifier field is inconsistent. The length is specified as 4 bytes, while the description indicates that it is a variable-length PEN. This inconsistency should be resolved by either changing the length description to reflect that the PEN is encoded as 32 bits or by changing the description to indicate a variable length.

---

<details>
<summary><b>Errata 6849</b> from <b>RFC 7852</b> - Additional Data Related to an Emergency Call (July 2016)</summary>

```
Section 11.7 says:


Example(s):  TEL;VALUE=uri;TYPE="main,voice";PREF=1:tel:+1-418-656-90
      00

It should say:

Example(s):  TEL;VALUE=uri;TYPE="main-number,voice";PREF=1:tel:+1-418-656-90
      00

Notes:

The type value is specified as "main-number" but in the example is simply "main".
```

</details>

<br>**Explanation:**
The example provided for the TYPE parameter uses "main" while the specification indicates that it should be "main-number".  This inconsistency between the specification and the example could lead to misinterpretations and incorrect implementations.

---

<details>
<summary><b>Errata 7679</b> from <b>RFC 7852</b> - Additional Data Related to an Emergency Call (July 2016)</summary>

```
Section 6.1 says:


An example
   Call-Info header field for this would be:

   Call-Info:  https://www.example.com/23sedde3;
       purpose="EmergencyCallData.ProviderInfo"

It should say:

An example
   Call-Info header field for this would be:

   Call-Info:  https://www.example.com/23sedde3;
       purpose=EmergencyCallData.ProviderInfo

Notes:

Remove double quote on purpose attribute. It's a token type instead of "String" type.
```

</details>

<br>**Explanation:**
The original example includes double quotes around the purpose attribute, which is a token type and should not be quoted. This inconsistency between the example and the specification of the attribute type affects the interpretation and correct implementation of the Call-Info header field.

---

<details>
<summary><b>Errata 7703</b> from <b>RFC 7854</b> - BGP Monitoring Protocol (BMP) (June 2016)</summary>

```
Section 4.2 says:


      *  The L flag, if set to 1, indicates that the message reflects
         the post-policy Adj-RIB-In (i.e., its path attributes reflect
         the application of inbound policy).  It is set to 0 if the
         message reflects the pre-policy Adj-RIB-In.  Locally sourced
         routes also carry an L flag of 1.  See Section 5 for further
         detail.  This flag has no significance when used with route
         mirroring messages (Section 4.7).

It should say:

      *  The L flag, if set to 1, indicates that the message reflects
         the post-policy Adj-RIB-In (i.e., its path attributes reflect
         the application of inbound policy).  It is set to 0 if the
         message reflects the pre-policy Adj-RIB-In.  Locally sourced
         routes also carry an L flag of 1.  See Section 5 for further
         detail.  This flag has significance only when used with Route
         Monitoring messages.

Notes:

The L flag is used to indicate whether the route monitoring update reflects Adj-RIB-In pre-policy or post-policy (RFC 7854), or Adj-RIB-Out pre-policy or post-policy (RFC 8671). It does not apply to any message other than the Route Monitoring message.
```

</details>

<br>**Explanation:**
The original description of the L flag incorrectly states that it has no significance for route mirroring messages. The corrected description clarifies that the L flag is only significant for Route Monitoring messages.  This inconsistency between the original description and the actual usage of the L flag could lead to misinterpretations and incorrect implementations.

---

<details>
<summary><b>Errata 6955</b> from <b>RFC 7915</b> - IP/ICMP Translation Algorithm (June 2016)</summary>

```
Section 4.5 says:


Calculating an IPv6 checksum and forwarding the packet (which has performance implications).

It should say:

Calculating an UDP checksum and forwarding the packet (which has performance implications).

Notes:

IPv6 doesn't have a checksum. The text appears to refer to the UDP checksum
```

</details>

<br>**Explanation:**
The errata corrects a factual error in Section 4.5. The original text incorrectly mentions calculating an IPv6 checksum, while IPv6 doesn't have a header checksum. This error is directly related to implementation as it provides an instruction that is impossible to implement correctly and suggests a different protocol's checksum, UDP checksum, instead.  The correction is essential for correct implementation.

---

<details>
<summary><b>Errata 5986</b> from <b>RFC 7940</b> - Representing Label Generation Rulesets Using XML (August 2016)</summary>

```
Section 6.3.1 says:


   A simple rule to match a label where all characters are members of
   some class called "preferred-codepoint":          

       <rule name="preferred-label">
           <start />
           <class by-ref="preferred-codepoint" count="1"/>
           <end />
       </rule>

It should say:

   A simple rule to match a label where all characters are members of
   some class called "preferred-codepoint":           

       <rule name="preferred-label">
           <start />
           <class by-ref="preferred-codepoint" count="1+"/>
           <end />
       </rule>

Notes:

Currently the value for count is 1, which means that the rule will match a label composed of only one char.
However, since the rule is supposed to match a label composed one or more chars, the value ofr count must be "1+" .
```

</details>

<br>**Explanation:**
The original specification uses "count="1", which only matches labels with one character, while the description indicates that it should match labels with one or more characters.  The correction uses "count="1+", resolving the inconsistency. This inconsistency would lead to implementations incorrectly matching labels based on the length.

---

<details>
<summary><b>Errata 5274</b> from <b>RFC 7950</b> - The YANG 1.1 Data Modeling Language (August 2016)</summary>

```
Section 7.16.3 says:


   A corresponding XML instance example of the complete notification:

     <notification
       xmlns="urn:ietf:params:xml:ns:netconf:notification:1.0">
       <eventTime>2008-07-08T00:01:00Z</eventTime>
       <event xmlns="urn:example:event">
         <event-class>fault</event-class>
         <reporting-entity>
           /ex:interface[ex:name='Ethernet0']
         </reporting-entity>
         <severity>major</severity>
       </event>
     </notification>

It should say:

   A corresponding XML instance example of the complete notification
   follows.  This example reports an event for an interface from the
   "example-foo" module defined in Section 13.1.1.

     <notification
       xmlns="urn:ietf:params:xml:ns:netconf:notification:1.0">
       <eventTime>2008-07-08T00:01:00Z</eventTime>
       <event xmlns="urn:example:event">
         <event-class>fault</event-class>
         <reporting-entity xmlns:ex="urn:example:foo">
           /ex:interface[ex:name='Ethernet0']
         </reporting-entity>
         <severity>major</severity>
       </event>
     </notification>


Notes:

The "ex" prefix is not declared.  The "example-foo" module in 13.1.1 is the only module in the draft that matches the given instance-identifier.  An alternative fix would be to use a different module and a matching instance-identifier.
```

</details>

<br>**Explanation:**
The original XML example lacks a namespace declaration for the "ex" prefix, leading to an invalid XML instance. The correction adds the necessary namespace declaration, making the example consistent and valid. This inconsistency would cause issues for implementations that validate the XML instance against the YANG module.

---

<details>
<summary><b>Errata 5489</b> from <b>RFC 7950</b> - The YANG 1.1 Data Modeling Language (August 2016)</summary>

```
Section 7.20.3.2 says:


The argument "delete" deletes properties from the target node.  The
   properties to delete are identified by substatements to the "delete"
   statement. 

It should say:

The argument "delete" deletes properties from the target node.  The
   properties to delete are identified by substatements to the "deviate"
   statement.
```

</details>

<br>**Explanation:**
The errata points out that Section 7.20.3.2 incorrectly states that properties are deleted using substatements to the "delete" statement.  The correction indicates that it should refer to substatements of the "deviate" statement. This is a direct contradiction within the specification impacting implementation. The text instructs the use of a non-existent mechanism, resulting in an inconsistent specification.

---

<details>
<summary><b>Errata 6078</b> from <b>RFC 7950</b> - The YANG 1.1 Data Modeling Language (August 2016)</summary>

```
Section 6.4. says:


   For example, consider the following definition:

     leaf lxiv {
       type decimal64 {
         fraction-digits 18;
       }
       must ". <= 10";
     }

   An instance of the "lxiv" leaf having the value of
   10.0000000000000001 will then successfully pass validation.

It should say:

   For example, consider the following definition:

     leaf lxiv {
       type decimal64 {
         fraction-digits 18;
       }
       must ". <= 9";
     }

   An instance of the "lxiv" leaf having the value of
   9.0000000000000001 will then successfully pass validation.

Notes:

Value 10.0000000000000001 is not a valid decimal64 value with 18 fraction digits as per Section 9.3.4.
```

</details>

<br>**Explanation:**
The original example uses a decimal64 value (10.0000000000000001) that is not valid given the specified constraints (fraction-digits 18 and must ". <= 10").  The correction uses a valid value (9.0000000000000001), making the example consistent. This inconsistency would lead to implementations incorrectly validating the example.

---

<details>
<summary><b>Errata 6258</b> from <b>RFC 7950</b> - The YANG 1.1 Data Modeling Language (August 2016)</summary>

```
Section 5.6.5 says:


For example, with these modules:

     module a {
       yang-version 1.1;
       namespace "urn:example:a";
       prefix "a";

       import b {
         revision-date 2015-01-01;
       }
       import c;

       revision 2015-01-01;


It should say:

For example, with these modules:

     module a {
       yang-version 1.1;
       namespace "urn:example:a";
       prefix "a";

       import b {
         revision-date 2015-01-01;
         prefix b;
       }
       import c {
         prefix c;
       }

       revision 2015-01-01;


Notes:

As is considered in 7.1.5, The mandatory "prefix" substatement assigns a prefix for the imported module that is scoped to the importing module or submodule. 

So, there should be a prefix substatement in the "import b" and "import c" statement respectively.
```

</details>

<br>**Explanation:**
The original example omits the mandatory "prefix" substatement within the "import" statements, violating the rules defined in Section 7.1.5. The correction adds the missing "prefix" substatements, making the example consistent with the specification. This inconsistency would affect implementations that rely on the correct usage of the "prefix" substatement within import statements.

---

<details>
<summary><b>Errata 6570</b> from <b>RFC 7950</b> - The YANG 1.1 Data Modeling Language (August 2016)</summary>

```
Section 11 says:


   o  New typedefs, groupings, rpcs, notifications, extensions,
      features, and identities may be added.

It should say:

   o  New typedefs, groupings, rpcs, actions, notifications,
      extensions, features, and identities may be added.

Notes:

The original text unintentionally fails to mention actions. A definition in a published module may be revised by adding actions to this definition.
```

</details>

<br>**Explanation:**
The original text omits actions from the list of YANG constructs that can be added to a module. This omission creates an inconsistency because actions are valid constructs that can be added. The correction adds actions to the list, resolving the inconsistency.

---

<details>
<summary><b>Errata 7020</b> from <b>RFC 7951</b> - JSON Encoding of Data Modeled with YANG (August 2016)</summary>

```
Section 6.8 says:


An "identityref" value is represented as a string -- the name of an
identity.  If the identity is defined in a module other than the leaf
node containing the identityref value, the namespace-qualified form
(Section 4) MUST be used.  Otherwise, both the simple and namespace-
qualified forms are permitted.

It should say:

An "identityref" value is represented as a string -- the name of an
identity.  If the identity is defined in a module other than the leaf or
leaf-list node containing the identityref value, the namespace-qualified
form (Section 4) MUST be used.  Otherwise, both the simple and namespace-
qualified forms are permitted.

Notes:

The original text omitted leaf-list nodes, which may also be of "identityref" type.
```

</details>

<br>**Explanation:**
The original text incorrectly limits the description to only leaf nodes when describing the usage of namespace-qualified forms for identityref values. The correction extends this to include leaf-list nodes as well, which can also be of the identityref type.  This omission creates an inconsistency between the description and the actual permissible usage.

---

<details>
<summary><b>Errata 5351</b> from <b>RFC 7970</b> - The Incident Object Description Exchange Format Version 2 (November 2016)</summary>

```
Section 2.16 says:


The attributes of the iodef:ExtensionType type are:

   name
      Optional.  STRING.  A free-form name of the field or data element.

   dtype
      Required.  ENUM.  The data type of the element content.  The
      default value is "string".  These values are maintained in the
      "ExtensionType-dtype" IANA registry per Section 10.2.

      1.   boolean.  The element content is of type BOOLEAN.

      2.   byte.  The element content is of type BYTE.

      3.   bytes.  The element content is of type HEXBIN.

      4.   character.  The element content is of type CHARACTER.

      5.   date-time.  The element content is of type DATETIME.

      6.   ntpstamp.  Same as date-time.

      7.   integer.  The element content is of type INTEGER.

      8.   portlist.  The element content is of type PORTLIST.

      9.   real.  The element content is of type REAL.

      10.  string.  The element content is of type STRING.

      11.  file.  The element content is a base64-encoded binary file
           encoded as a BYTE[] type.

      12.  path.  The element content is a file-system path encoded as a
           STRING type.

      13.  frame.  The element content is a Layer 2 frame encoded as a
           HEXBIN type.

      14.  packet.  The element content is a Layer 3 packet encoded as a
           HEXBIN type.

      15.  ipv4-packet.  The element content is an IPv4 packet encoded
           as a HEXBIN type.

      16.  ipv6-packet.  The element content is an IPv6 packet encoded
           as a HEXBIN type.

      17.  url.  The element content is of type URL.

      18.  csv.  The element content is a comma-separated value (CSV)
           list per Section 2 of [RFC4180] encoded as a STRING type.

      19.  winreg.  The element content is a Microsoft Windows registry
           key encoded as a STRING type.

      20.  xml.  The element content is XML.  See Section 5.2.

      21.  ext-value.  A value used to indicate that this attribute is
           extended and the actual value is provided using the
           corresponding ext-* attribute.  See Section 5.1.1.

It should say:

The attributes of the iodef:ExtensionType type are:

   name
      Optional.  STRING.  A free-form name of the field or data element.

   dtype
      Required.  ENUM.  The data type of the element content.  The
      default value is "string".  These values are maintained in the
      "ExtensionType-dtype" IANA registry per Section 10.2.

      1.   boolean.  The element content is of type BOOLEAN.

      2.   byte.  The element content is of type BYTE.

      3.   bytes.  The element content is of type HEXBIN[].

      4.   character.  The element content is of type CHARACTER.

      5.   date-time.  The element content is of type DATETIME.

      6.   ntpstamp.  Same as date-time.

      7.   integer.  The element content is of type INTEGER.

      8.   portlist.  The element content is of type PORTLIST.

      9.   real.  The element content is of type REAL.

      10.  string.  The element content is of type STRING.

      11.  file.  The element content is a base64-encoded binary file
           encoded as a BYTE[] type.

      12.  path.  The element content is a file-system path encoded as a
           STRING type.

      13.  frame.  The element content is a Layer 2 frame encoded as a
           HEXBIN[] type.

      14.  packet.  The element content is a Layer 3 packet encoded as a
           HEXBIN[] type.

      15.  ipv4-packet.  The element content is an IPv4 packet encoded
           as a HEXBIN[] type.

      16.  ipv6-packet.  The element content is an IPv6 packet encoded
           as a HEXBIN[] type.

      17.  url.  The element content is of type URL.

      18.  csv.  The element content is a comma-separated value (CSV)
           list per Section 2 of [RFC4180] encoded as a STRING type.

      19.  winreg.  The element content is a Microsoft Windows registry
           key encoded as a STRING type.

      20.  xml.  The element content is XML.  See Section 5.2.

      21.  ext-value.  A value used to indicate that this attribute is
           extended and the actual value is provided using the
           corresponding ext-* attribute.  See Section 5.1.1.

Notes:

Section 2.5.2 (explanation of HEXBIN and HEXBIN[] types) says:
" A binary octet encoded as a character tuple consistent of two
   hexadecimal digits is represented in the information model by the
   HEXBIN data type.  A sequence of these octets is of the HEXBIN[] data
   type.
   The HEXBIN and HEXBIN[] data types are implemented in the data model
   as an "xs:hexBinary" type per Section 3.2.15 of [W3C.SCHEMA.DTYPES]."

If I am reading that section correctly, HEXBIN is for hex-encoded things that decode to exactly one byte, while HEXBIN[] is for hex-encoded things that decode to one or more bytes. Thus, things that may decode to multiple bytes should be HEXBIN[], not HEXBIN. 

The extension types in Section 2.16  that are currently HEXBIN should probably be HEXBIN[]. The name "bytes" implies decoding to multiple bytes (so it should be HEXBIN[]). Frames and packets (regardless of layer) tend to be multiple bytes long (so they should be HEXBIN[] as well).
```

</details>

<br>**Explanation:**
The original description uses the HEXBIN type for data elements that can contain multiple bytes, while the specification defines HEXBIN for single bytes and HEXBIN[] for multiple bytes.  The correction updates the dtype descriptions for 'bytes', 'frame', 'packet', 'ipv4-packet', and 'ipv6-packet' to use HEXBIN[], resolving the inconsistency.  This inconsistency could lead to implementations incorrectly interpreting the data types.

---

<details>
<summary><b>Errata 5543</b> from <b>RFC 7970</b> - The Incident Object Description Exchange Format Version 2 (November 2016)</summary>

```
Section 8 says:


    <xs:element name="Confidence">
      <xs:complexType>
        <xs:attribute name="rating"
                      type="confidence-rating-type" use="required"/>
        <xs:attribute name="ext-rating"
                      type="xs:string" use="optional"/>
      </xs:complexType>
    </xs:element>

It should say:

    <xs:element name="Confidence">
      <xs:complexType>
        <xs:simpleContent>
          <xs:extension base="xs:float">
            <xs:attribute name="rating"
                          type="confidence-rating-type" use="required"/>
            <xs:attribute name="ext-rating"
                          type="xs:string" use="optional"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
    </xs:element>

Notes:

Section 3.12.5 says as follows:
  "The content of the class is of type REAL and specifies a numerical
   assessment in the confidence of the data when the value of the rating
   attribute is "numeric".  Otherwise, this element MUST be empty."

The current schema does not allow the confidence class to have the content (REAL type), thus the correction (note the addition of "<xs:extension base="xs:float">") is proposed.
```

</details>

<br>**Explanation:**
The original schema definition for the Confidence element does not allow for a numerical value, while Section 3.12.5 specifies that a numerical assessment of confidence is possible.  The correction includes an xs:extension of xs:float, thus allowing for a numerical value, resolving the inconsistency. This inconsistency would prevent implementations from correctly handling numerical confidence values.

---

<details>
<summary><b>Errata 5544</b> from <b>RFC 7970</b> - The Incident Object Description Exchange Format Version 2 (November 2016)</summary>

```
Section 8 says:


 <xs:element name="Node">
      <xs:complexType>
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element ref="iodef:DomainData"
                        minOccurs="0" maxOccurs="unbounded"/>
            <xs:element ref="iodef:Address"
                        minOccurs="0" maxOccurs="unbounded"/>
          </xs:choice>
          <xs:element ref="iodef:PostalAddress" minOccurs="0"/>
          <xs:element ref="iodef:Location"
                      minOccurs="0" maxOccurs="unbounded"/>
          <xs:element ref="iodef:Counter"
                      minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>

It should say:

 <xs:element name="Node">
      <xs:complexType>
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element ref="iodef:DomainData"
                        maxOccurs="unbounded"/>
            <xs:element ref="iodef:Address"
                        maxOccurs="unbounded"/>
          </xs:choice>
          <xs:element ref="iodef:PostalAddress" minOccurs="0"/>
          <xs:element ref="iodef:Location"
                      minOccurs="0" maxOccurs="unbounded"/>
          <xs:element ref="iodef:Counter"
                      minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
      </xs:complexType>
    </xs:element>

Notes:

Section 3.18 says as follows:

"DomainData
      Zero or more.  The domain (DNS) information associated with this
      node.  If an Address is not provided, at least one DomainData MUST
      be specified.  See Section 3.19.

   Address
      Zero or more.  The hardware, network, or application address of
      the node.  If a DomainData is not provided, at least one Address
      MUST be specified.  See Section 3.18.1."

To comply with the above definition, "minOccurs" attribute for both DomainData and Address elements need to be removed. (Current schema allows to omit both of the elements, but the RFC says that at least one of them need to be presented.)
```

</details>

<br>**Explanation:**
The original schema allows both DomainData and Address elements to be omitted, while the specification in section 3.18 requires at least one of them to be present.  The corrected schema removes the minOccurs="0" attribute from both elements to enforce this requirement, resolving the inconsistency.

---

<details>
<summary><b>Errata 5053</b> from <b>RFC 8007</b> - Content Delivery Network Interconnection (CDNI) Control Interface / Triggers (December 2016)</summary>

```
Section 5.2.3 says:


| canceling |
| canceled  |

It should say:

| cancelling |
| cancelled  |


Notes:

In the final editing phase, I believe it was agreed that text would use the American spelling with 1 "l", but that the actual status strings would use 2 "l"s.  In sections 2.3, 4.3, 4.5, and Appendix A, the quoted status strings all use 2 "l"s.  The first column of the table in section 5.2.3 is providing the JSON string values, which should match the quoted status strings in sections 2.3, 4.3, 4.5, and Appendix A and have 2 "l"s.
```

</details>

<br>**Explanation:**
The table in section 5.2.3 uses inconsistent spellings ("canceling", "canceled") compared to other sections (2.3, 4.3, 4.5, Appendix A) which use ("cancelling", "cancelled"). The inconsistent spelling affects the interpretation and implementation of the JSON status strings.

---

<details>
<summary><b>Errata 5054</b> from <b>RFC 8007</b> - Content Delivery Network Interconnection (CDNI) Control Interface / Triggers (December 2016)</summary>

```
Section 5.2.7 says:


| ecanceled    |

It should say:

| ecancelled   |



Notes:

In the final editing phase, I believe it was agreed that text would use the American spelling with 1 "l", but that the status strings would use 2 "l"s.  This should apply to the error codes as well.  The first column of the table in section 5.2.7 is providing the Error Code values, which like the status code strings in sections 2.3, 4.3, 4.5, 5.2.3, and Appendix A, should have 2 "l"s.  Note: The IANA registry has the error code as "ecancelled" with 2 "l"s.  http://www.iana.org/assignments/cdni-parameters/cdni-parameters.xhtml#error-codes

Note: This errata also applies to Appendix A.
```

</details>

<br>**Explanation:**
The table in section 5.2.7 uses inconsistent spelling for the error code compared to other sections of the document and the IANA registry. The corrected table uses the double-l spelling that matches the rest of the document and the IANA registry, resolving the inconsistency.

---

<details>
<summary><b>Errata 6385</b> from <b>RFC 8007</b> - Content Delivery Network Interconnection (CDNI) Control Interface / Triggers (December 2016)</summary>

```
Section 4.1 says:


   When a CI/T Trigger Command is accepted, the uCDN MUST create a new
   Trigger Status Resource that will convey a specification of the CI/T
   Command and its current status.  The HTTP response to the dCDN MUST
   have status code 201 and MUST convey the URI of the Trigger Status
   Resource in the Location header field [RFC7231].

It should say:

   When a CI/T Trigger Command is accepted, the dCDN MUST create a new
   Trigger Status Resource that will convey a specification of the CI/T
   Command and its current status.  The HTTP response to the uCDN MUST
   have status code 201 and MUST convey the URI of the Trigger Status
   Resource in the Location header field [RFC7231].

Notes:

There has been an accidental switch between "uCDN" and "dCDN" terms in this statement. If my understanding is correct, when the uCDN post a CI/T command to the dCDN, the latter must create a trigger status resource and returns in the response (HTTP code 201) “Location” header the URI of that status resource.
```

</details>

<br>**Explanation:**
The original text incorrectly describes the roles of the uCDN and dCDN when a CI/T Trigger Command is accepted.  The corrected text swaps the roles, accurately reflecting that the dCDN creates the Trigger Status Resource and sends its URI to the uCDN. This inconsistency affects the understanding of the protocol's operation and the correct implementation of the interaction between the two CDNs.

---

<details>
<summary><b>Errata 6938</b> from <b>RFC 8013</b> - Forwarding and Control Element Separation (ForCES) Inter-FE Logical Functional Block (LFB) (February 2017)</summary>

```
Section 5.1.1 says:


Caution needs to be exercised on how low the resulting reported link MTU could be: for IPv4 packets, the minimum size is 64 octets [RFC791] and for IPv6 the minimum size is 1280 octets [RFC2460].

It should say:

Caution needs to be exercised on how low the resulting reported link MTU could be: for IPv4 the recommended minimum size is 576 octets [RFC1122] and for IPv6 the minimum size is 1280 octets [RFC2460].

Notes:

The original text mixed minimum packet size with minimum MTU size.
```

</details>

<br>**Explanation:**
The original text incorrectly states the minimum IPv4 packet size, confusing it with the minimum MTU.  The correction uses the recommended minimum IPv4 MTU size, resolving the inconsistency. This inconsistency would mislead implementations calculating or interpreting the reported link MTU.

---

<details>
<summary><b>Errata 7639</b> from <b>RFC 8029</b> - Detecting Multiprotocol Label Switched (MPLS) Data-Plane Failures (March 2017)</summary>

```
Section 4.5 says:


If the Reply Mode in the echo request is "Reply via an
IPv4 UDP packet with Router Alert", then the IP header MUST contain
the Router Alert IP Option of value 0x0 [RFC2113] for IPv4 or 69
[RFC7506] for IPv6.

It should say:

If the Reply Mode in the echo request is "Reply via an
IPv4/IPv6 UDP packet with Router Alert", then the IP header MUST contain
the Router Alert IP Option of value 0x0 [RFC2113] for IPv4 or 69
[RFC7506] for IPv6.

Notes:

The description of the Reply Mode recorded in the IANA "Reply Modes" sub-registry of the "Multiprotocol Label Switching (MPLS) Label Switched Paths (LSPs) Ping Parameters" registry is "Reply via an IPv4/IPv6 UDP packet with Router Alert".
```

</details>

<br>**Explanation:**
The original text only mentions IPv4 packets in the description of the Reply Mode, while the IANA registry and the actual behavior include both IPv4 and IPv6 packets. This omission creates an inconsistency between the description and the broader functionality.

---

<details>
<summary><b>Errata 5131</b> from <b>RFC 8072</b> - YANG Patch Media Type (February 2017)</summary>

```
Section 2.2 says:


Regarding section 2.2 of RFC 8072, the third paragraph states:


                                       ... If the edit does not identify
    any existing resource instance and the operation for the edit is not
    "create", then the request MUST NOT be processed and a "404 Not
    Found" error response MUST be sent by the server.

It should say:

                                      ... If the edit does not identify
   any existing resource instance and the operation for the edit is
   "delete" or "move" then the request MUST NOT be processed and a
   "404 Not Found" error response MUST be sent by the server.

Notes:

As per the second paragraph of section 2.2 of RFC 8072, the operations are expected to mirror the semantics of the "operation" attribute described in Section 7.2 of [RFC6241].

The spec also doesn't specify what happens if it is a "create" operation and the resource already exists.  It should probably also state that "400 Bad Request" is returned.
```

</details>

<br>**Explanation:**
The original specification states that a 404 error MUST be returned if an edit does not identify an existing resource instance and the operation is not "create". However, this is inconsistent with the semantics of RFC 6241, which specifies that a 404 error should only be returned for "delete" or "move" operations. The corrected specification aligns with RFC 6241, specifying that a 404 error MUST be returned only for "delete" or "move" operations and that a 400 error is returned for a create operation if the resource already exists.

---

<details>
<summary><b>Errata 5353</b> from <b>RFC 8103</b> - Using ChaCha20-Poly1305 Authenticated Encryption in the Cryptographic Message Syntax (CMS) (February 2017)</summary>

```
Section 6 says:


   The amount of encrypted data possible in a single invocation of
   AEAD_CHACHA20_POLY1305 is 2^32-1 blocks of 64 octets each, because of
   the size of the block counter field in the ChaCha20 block function.
   This gives a total of 247,877,906,880 octets, which is likely to be
   sufficient to handle the size of any CMS content type.  Note that the
   ciphertext length field in the authentication buffer will accommodate
   2^64 octets, which is much larger than necessary.

It should say:

   The amount of encrypted data possible in a single invocation of
   AEAD_CHACHA20_POLY1305 is 2^32-1 blocks of 64 octets each, because of
   the size of the block counter field in the ChaCha20 block function.
   This gives a total of 274,877,906,880 octets, which is likely to be
   sufficient to handle the size of any CMS content type.  Note that the
   ciphertext length field in the authentication buffer will accommodate
   2^64 octets, which is much larger than necessary.

Notes:

The calculated total number of octets that can be encrypted in a single invocation is incorrect. See RFC Errata, Erratum ID 4858, RFC 7539.
```

</details>

<br>**Explanation:**
The original calculation of the maximum encrypted data size for AEAD_CHACHA20_POLY1305 is incorrect. The correction provides the correct calculation, resolving the inconsistency. This inconsistency would affect implementations that rely on the correct maximum size for encryption.

---

<details>
<summary><b>Errata 7752</b> from <b>RFC 8147</b> - Next-Generation Pan-European eCall (May 2017)</summary>

```
Section 13 says:


<?xml version="1.0"?>
<xs:schema
    targetNamespace="urn:ietf:params:xml:ns:EmergencyCallData:control"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:pi="urn:ietf:params:xml:ns:EmergencyCallData:control"
    xmlns:xml="http://www.w3.org/XML/1998/namespace"
    elementFormDefault="qualified"
    attributeFormDefault="unqualified">
    
    <xs:import namespace="http://www.w3.org/XML/1998/namespace"/>
    
    <xs:element name="EmergencyCallData.Control"
        type="pi:controlType"/>
    
    <xs:complexType name="controlType">
        <xs:complexContent>
            <xs:restriction base="xs:anyType">
                <xs:choice>
                    <xs:element name="capabilities"
                        type="pi:capabilitiesType"/>
                    <xs:element name="request" type="pi:requestType"/>
                    <xs:element name="ack" type="pi:ackType"/>
                    <xs:any namespace="##any" processContents="lax"
                        minOccurs="0"
                        maxOccurs="unbounded"/>
                </xs:choice>
                <xs:anyAttribute/>
            </xs:restriction>
        </xs:complexContent>
    </xs:complexType>
    
    <xs:complexType name="ackType">
        <xs:complexContent>
            <xs:restriction base="xs:anyType">
                <xs:sequence minOccurs="1" maxOccurs="unbounded">
                    <xs:element name="actionResult" minOccurs="0"
                        maxOccurs="unbounded">
                        <xs:complexType>
                            <xs:attribute name="action"
                                type="xs:token"
                                use="required"/>
                            <xs:attribute name="success"
                                type="xs:boolean"
                                use="required"/>
                            <xs:attribute name="reason"
                                type="xs:token">
                                <xs:annotation>
                                    <xs:documentation>
                                        conditionally mandatory
                                        when @success="false"
                                        to indicate reason code
                                        for a failure
                                    </xs:documentation>
                                </xs:annotation>
                            </xs:attribute>
                            <xs:attribute name="details"
                                type="xs:string"/>
                            <xs:anyAttribute
                                processContents="skip"/>
                        </xs:complexType>
                    </xs:element>
                    <xs:any namespace="##any" processContents="lax"
                        minOccurs="0"
                        maxOccurs="unbounded"/>
                </xs:sequence>
                <xs:attribute name="ref"
                    type="xs:anyURI"
                    use="required"/>
                
                <xs:attribute name="received"
                    type="xs:boolean"/>
                <xs:anyAttribute/>
            </xs:restriction>
        </xs:complexContent>
    </xs:complexType>
    
    <xs:complexType name="capabilitiesType">
        <xs:complexContent>
            <xs:restriction base="xs:anyType">
                <xs:sequence minOccurs="1" maxOccurs="unbounded">
                    <xs:element name="request"
                        type="pi:requestType"
                        minOccurs="1"
                        maxOccurs="unbounded"/>
                    <xs:any namespace="##any" processContents="lax"
                        minOccurs="0"
                        maxOccurs="unbounded"/>
                </xs:sequence>
                <xs:anyAttribute/>
            </xs:restriction>
        </xs:complexContent>
    </xs:complexType>
    
    <xs:complexType name="requestType">
        <xs:complexContent>
            <xs:restriction base="xs:anyType">
                <xs:choice minOccurs="1" maxOccurs="unbounded">
                    <xs:element name="text" minOccurs="0"
                        maxOccurs="unbounded">
                        <xs:complexType>
                            <xs:simpleContent>
                                <xs:extension base="xs:string">
                                    <xs:anyAttribute
                                        namespace="##any"
                                        processContents="skip"/>
                                </xs:extension>
                            </xs:simpleContent>
                        </xs:complexType>
                    </xs:element>
                    <xs:any namespace="##any" processContents="lax"
                        minOccurs="0"
                        maxOccurs="unbounded"/>
                </xs:choice>
                <xs:attribute name="action" type="xs:token"
                    use="required"/>
                
                <xs:attribute name="int-id" type="xs:unsignedInt"/>
                <xs:attribute name="persistence"
                    type="xs:duration"/>
                <xs:attribute name="datatype" type="xs:token"/>
                <xs:attribute name="supported-values"
                    type="xs:string"/>
                <xs:attribute name="element-id" type="xs:token"/>
                <xs:attribute name="requested-state"
                    type="xs:token"/>
                <xs:anyAttribute/>
            </xs:restriction>
        </xs:complexContent>
    </xs:complexType>
</xs:schema>

It should say:

<?xml version="1.0"?>
<xs:schema
    targetNamespace="urn:ietf:params:xml:ns:EmergencyCallData:control"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:pi="urn:ietf:params:xml:ns:EmergencyCallData:control"
    xmlns:xml="http://www.w3.org/XML/1998/namespace"
    elementFormDefault="qualified"
    attributeFormDefault="unqualified">
    
    <xs:import namespace="http://www.w3.org/XML/1998/namespace"/>
    
    <xs:element name="EmergencyCallData.Control"
        type="pi:controlType"/>
    
    <xs:complexType name="controlType">
        <xs:complexContent>
            <xs:restriction base="xs:anyType">
                <xs:choice>
                    <xs:element name="capabilities"
                        type="pi:capabilitiesType"/>
                    <xs:element name="request" type="pi:requestType"/>
                    <xs:element name="ack" type="pi:ackType"/>
                    <xs:any namespace="##other" processContents="lax"
                        minOccurs="0"
                        maxOccurs="unbounded"/>
                </xs:choice>
                <xs:anyAttribute/>
            </xs:restriction>
        </xs:complexContent>
    </xs:complexType>
    
    <xs:complexType name="ackType">
        <xs:complexContent>
            <xs:restriction base="xs:anyType">
                <xs:sequence minOccurs="1" maxOccurs="unbounded">
                    <xs:element name="actionResult" minOccurs="0"
                        maxOccurs="unbounded">
                        <xs:complexType>
                            <xs:attribute name="action"
                                type="xs:token"
                                use="required"/>
                            <xs:attribute name="success"
                                type="xs:boolean"
                                use="required"/>
                            <xs:attribute name="reason"
                                type="xs:token">
                                <xs:annotation>
                                    <xs:documentation>
                                        conditionally mandatory
                                        when @success="false"
                                        to indicate reason code
                                        for a failure
                                    </xs:documentation>
                                </xs:annotation>
                            </xs:attribute>
                            <xs:attribute name="details"
                                type="xs:string"/>
                            <xs:anyAttribute
                                processContents="skip"/>
                        </xs:complexType>
                    </xs:element>
                    <xs:any namespace="##other" processContents="lax"
                        minOccurs="0"
                        maxOccurs="unbounded"/>
                </xs:sequence>
                <xs:attribute name="ref"
                    type="xs:anyURI"
                    use="required"/>
                
                <xs:attribute name="received"
                    type="xs:boolean"/>
                <xs:anyAttribute/>
            </xs:restriction>
        </xs:complexContent>
    </xs:complexType>
    
    <xs:complexType name="capabilitiesType">
        <xs:complexContent>
            <xs:restriction base="xs:anyType">
                <xs:sequence minOccurs="1" maxOccurs="unbounded">
                    <xs:element name="request"
                        type="pi:requestType"
                        minOccurs="1"
                        maxOccurs="unbounded"/>
                    <xs:any namespace="##other" processContents="lax"
                        minOccurs="0"
                        maxOccurs="unbounded"/>
                </xs:sequence>
                <xs:anyAttribute/>
            </xs:restriction>
        </xs:complexContent>
    </xs:complexType>
    
    <xs:complexType name="requestType">
        <xs:complexContent>
            <xs:restriction base="xs:anyType">
                <xs:choice minOccurs="1" maxOccurs="unbounded">
                    <xs:element name="text" minOccurs="0"
                        maxOccurs="unbounded">
                        <xs:complexType>
                            <xs:simpleContent>
                                <xs:extension base="xs:string">
                                    <xs:anyAttribute
                                        namespace="##any"
                                        processContents="skip"/>
                                </xs:extension>
                            </xs:simpleContent>
                        </xs:complexType>
                    </xs:element>
                    <xs:any namespace="##other" processContents="lax"
                        minOccurs="0"
                        maxOccurs="unbounded"/>
                </xs:choice>
                <xs:attribute name="action" type="xs:token"
                    use="required"/>
                
                <xs:attribute name="int-id" type="xs:unsignedInt"/>
                <xs:attribute name="persistence"
                    type="xs:duration"/>
                <xs:attribute name="datatype" type="xs:token"/>
                <xs:attribute name="supported-values"
                    type="xs:string"/>
                <xs:attribute name="element-id" type="xs:token"/>
                <xs:attribute name="requested-state"
                    type="xs:token"/>
                <xs:anyAttribute/>
            </xs:restriction>
        </xs:complexContent>
    </xs:complexType>
</xs:schema>

Notes:

The complex types "controlType", "ackType", "capabilitiesType" and "requestType" define extension points by using xs:any with namespace ##any. This violates the "Unique Particle Attribution" rule for XSD 1.0 (see: https://www.w3.org/wiki/UniqueParticleAttribution) and shows up as an error in some tools.

I suggest changing the namespace to ##other like it's done in other schemas (for example, RFC7865 defines extension points in this way: https://datatracker.ietf.org/doc/html/rfc7865#section-9 ).

[Verifier note:]

Replace all four occurrences of:

<xs:any namespace="##any" processContents="lax">

with:

<xs:any namespace="##other" processContents="lax">
```

</details>

<br>**Explanation:**
The original schema uses `xs:any namespace="##any"`, which violates the "Unique Particle Attribution" rule for XSD 1.0.  The corrected schema uses `xs:any namespace="##other"`, which resolves this inconsistency and produces a schema that is valid and correctly parses.

---

<details>
<summary><b>Errata 5066</b> from <b>RFC 8152</b> - CBOR Object Signing and Encryption (COSE) (July 2017)</summary>

```
Section 14 says:


   o  The restriction applies to the encoding of the Sig_structure, the
      Enc_structure, and the MAC_structure.

It should say:

   o  The restriction applies to the encoding of the COSE_KDF_Context, 
      Sig_structure, the Enc_structure, and the MAC_structure.


Notes:

When listing the set of structure that need to be canonically encoded, I missed this one.

Verifier Notes: this is being fixed in draft-ietf-cose-rfc8152bis-algs.
```

</details>

<br>**Explanation:**
The original text omits COSE_KDF_Context from the list of structures that require canonical encoding. The correction includes COSE_KDF_Context, making the description consistent with the actual requirement. This inconsistency would affect implementations that do not canonically encode the COSE_KDF_Context structure.

---

<details>
<summary><b>Errata 5545</b> from <b>RFC 8152</b> - CBOR Object Signing and Encryption (COSE) (July 2017)</summary>

```
Section 7.1 says:


   +---------+-------+----------------+------------+-------------------+
   | Name    | Label | CBOR Type      | Value      | Description       |
   |         |       |                | Registry   |                   |
   +---------+-------+----------------+------------+-------------------+
   | kty     | 1     | tstr / int     | COSE Key   | Identification of |
   |         |       |                | Common     | the key type      |
   |         |       |                | Parameters |                   |
   |         |       |                |            |                   |
   | kid     | 2     | bstr           |            | Key               |
   |         |       |                |            | identification    |
   |         |       |                |            | value -- match to |
   |         |       |                |            | kid in message    |
   |         |       |                |            |                   |
   | alg     | 3     | tstr / int     | COSE       | Key usage         |
   |         |       |                | Algorithms | restriction to    |
   |         |       |                |            | this algorithm    |
   |         |       |                |            |                   |
   | key_ops | 4     | [+ (tstr/int)] |            | Restrict set of   |
   |         |       |                |            | permissible       |
   |         |       |                |            | operations        |
   |         |       |                |            |                   |
   | Base IV | 5     | bstr           |            | Base IV to be     |
   |         |       |                |            | xor-ed with       |
   |         |       |                |            | Partial IVs       |
   +---------+-------+----------------+------------+-------------------+

                          Table 3: Key Map Labels

It should say:

   +---------+-------+----------------+------------+-------------------+
   | Name    | Label | CBOR Type      | Value      | Description       |
   |         |       |                | Registry   |                   |
   +---------+-------+----------------+------------+-------------------+
   | kty     | 1     | tstr / int     | COSE Key   | Identification of |
   |         |       |                | Types      | the key type      |
   |         |       |                |            |                   |
   |         |       |                |            |                   |
   | kid     | 2     | bstr           |            | Key               |
   |         |       |                |            | identification    |
   |         |       |                |            | value -- match to |
   |         |       |                |            | kid in message    |
   |         |       |                |            |                   |
   | alg     | 3     | tstr / int     | COSE       | Key usage         |
   |         |       |                | Algorithms | restriction to    |
   |         |       |                |            | this algorithm    |
   |         |       |                |            |                   |
   | key_ops | 4     | [+ (tstr/int)] |            | Restrict set of   |
   |         |       |                |            | permissible       |
   |         |       |                |            | operations        |
   |         |       |                |            |                   |
   | Base IV | 5     | bstr           |            | Base IV to be     |
   |         |       |                |            | xor-ed with       |
   |         |       |                |            | Partial IVs       |
   +---------+-------+----------------+------------+-------------------+

                          Table 3: Key Map Labels

Notes:

The value registry for kty should be COSE Key Types, as indicated in the text following Table 3. This change affects the IANA registry: https://www.iana.org/assignments/cose/cose.xhtml#key-common-parameters
```

</details>

<br>**Explanation:**
The original table incorrectly describes the value registry for the kty parameter as "COSE Key Common Parameters." The correction uses the correct term "COSE Key Types", resolving the inconsistency between the table and the text following it.

---

<details>
<summary><b>Errata 5650</b> from <b>RFC 8152</b> - CBOR Object Signing and Encryption (COSE) (July 2017)</summary>

```
Section Section 13.2 says:


   | crv  | 1     | -1    | int /  | EC identifier - Taken from the    |
   |      |       |       | tstr   | "COSE Key Common Parameters"      |
   |      |       |       |        | registry                          |

It should say:

   | crv  | 1     | -1    | int /  | EC identifier - Taken from the    |
   |      |       |       | tstr   | "COSE Elliptic Curves" registry   |

Notes:

The set of curve identifiers lives in the COSE Elliptic Curves registry and not in the COSE Key Common Parameters registry.
```

</details>

<br>**Explanation:**
The original text points to the wrong registry for EC identifiers. The correct registry is the "COSE Elliptic Curves" registry, not the "COSE Key Common Parameters" registry. This inconsistency could lead to incorrect interpretation and implementation.

---

<details>
<summary><b>Errata 5669</b> from <b>RFC 8152</b> - CBOR Object Signing and Encryption (COSE) (July 2017)</summary>

```
Section 16.7 says:


Value:  This is the value used to identify the curve.  These values
   MUST be unique.  The value can be a positive integer, a negative
   integer, or a string.

Description:  This field contains a brief description of the curve.

References:  This contains a pointer to the public specification for
   the curve if one exists.

It should say:

Value:  This is the value used to identify the key type.  These values
   MUST be unique.  The values are positive integers.

Description:  This field contains a brief description of the key type.

References:  This contains a pointer to the public specification for
   the key type if one exists.

Notes:

This Registry is about Key Types, but the current text refers to curves.

The value identifying a key type can be only a positive integer.
```

</details>

<br>**Explanation:**
The original description of the registry entries incorrectly refers to curves when the registry is for key types. The corrected description specifies that the values identify key types, using positive integers and providing descriptions and references accordingly. This inconsistency affects the interpretation and use of the key type registry.

---

<details>
<summary><b>Errata 6209</b> from <b>RFC 8152</b> - CBOR Object Signing and Encryption (COSE) (July 2017)</summary>

```
Section 9 says:


can be used to prove the identity

It should say:

cannot be used to prove the identity

Notes:

MACs cannot be used to prove identity to a third party.  There is a missing "not" in the sentence.
```

</details>

<br>**Explanation:**
The original text incorrectly states that MACs can be used to prove identity. The corrected text accurately reflects that MACs cannot be used for this purpose.  This inconsistency affects the understanding of MAC functionality and may lead to incorrect implementations.

---

<details>
<summary><b>Errata 5996</b> from <b>RFC 8163</b> - Transmission of IPv6 over Master-Slave/Token-Passing (MS/TP) Networks (May 2017)</summary>

```
Section Appendix B. says:


       /*
        * Sanity check the encoding to prevent the while() loop below
        * from overrunning the output buffer.
        */
       if (read_index + code > length)
         return 0;


It should say:

       /*
        * Sanity check the encoding to prevent the while() loop below
        * from overrunning the output buffer.
        */
       if (code == 0 || read_index + code > length)
         return 0;


Notes:

This was submitted as a change to [BACnet], Annex T, by James Butler.  The normative procedure for decoding COBS is correct in [BACnet], 9.10.3.2(a) but this bug appears in the informative example in Annex T.  Since the purpose of COBS encoding is to eliminate all zero bytes from the data, the presence of a zero indicates an error.
```

</details>

<br>**Explanation:**
The original code lacks a check for a zero code value, which is an error condition in COBS encoding.  The correction adds this check, making the example code consistent with the normative decoding procedure. This inconsistency would lead to implementations failing to detect errors in COBS encoded data.

---

<details>
<summary><b>Errata 5945</b> from <b>RFC 8200 a.k.a. STD 86</b> - Internet Protocol, Version 6 (IPv6) Specification (July 2017)</summary>

```
Section 4.5 says:


4.5.  Fragment Header

   The Fragment header is used by an IPv6 source to send a packet larger
   than would fit in the path MTU to its destination.  (Note: unlike
   IPv4, fragmentation in IPv6 is performed only by source nodes, not by
   routers along a packet's delivery path -- see [RFC8200].)  The
   Fragment header is identified by a Next Header value of 44 in the
   immediately preceding header and has the following format:

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  Next Header  |   Reserved    |      Fragment Offset    |Res|M|
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                         Identification                        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

      Next Header         8-bit selector.  Identifies the initial header
                          type of the Fragmentable Part of the original
                          packet (defined below).  Uses the same values
                          as the IPv4 Protocol field [IANA-PN].

      Reserved            8-bit reserved field.  Initialized to zero for
                          transmission; ignored on reception.

      Fragment Offset     13-bit unsigned integer.  The offset, in
                          8-octet units, of the data following this
                          header, relative to the start of the
                          Fragmentable Part of the original packet.

      Res                 2-bit reserved field.  Initialized to zero for
                          transmission; ignored on reception.

      M flag              1 = more fragments; 0 = last fragment.

      Identification      32 bits.  See description below.

   In order to send a packet that is too large to fit in the MTU of the
   path to its destination, a source node may divide the packet into
   fragments and send each fragment as a separate packet, to be
   reassembled at the receiver.

   For every packet that is to be fragmented, the source node generates
   an Identification value.  The Identification must be different than
   that of any other fragmented packet sent recently* with the same
   Source Address and Destination Address.  If a Routing header is
   present, the Destination Address of concern is that of the final
   destination.


      *  "recently" means within the maximum likely lifetime of a
         packet, including transit time from source to destination and
         time spent awaiting reassembly with other fragments of the same
         packet.  However, it is not required that a source node knows
         the maximum packet lifetime.  Rather, it is assumed that the
         requirement can be met by implementing an algorithm that
         results in a low identification reuse frequency.  Examples of
         algorithms that can meet this requirement are described in
         [RFC7739].

   The initial, large, unfragmented packet is referred to as the
   "original packet", and it is considered to consist of three parts, as
   illustrated:

   original packet:

   +------------------+-------------------------+---//----------------+
   |  Per-Fragment    | Extension & Upper-Layer |   Fragmentable      |
   |    Headers       |       Headers           |      Part           |
   +------------------+-------------------------+---//----------------+

      The Per-Fragment headers must consist of the IPv6 header plus any
      extension headers that must be processed by nodes en route to the
      destination, that is, all headers up to and including the Routing
      header if present, else the Hop-by-Hop Options header if present,
      else no extension headers.

      The Extension headers are all other extension headers that are not
      included in the Per-Fragment headers part of the packet.  For this
      purpose, the Encapsulating Security Payload (ESP) is not
      considered an extension header.  The Upper-Layer header is the
      first upper-layer header that is not an IPv6 extension header.
      Examples of upper-layer headers include TCP, UDP, IPv4, IPv6,
      ICMPv6, and as noted ESP.

      The Fragmentable Part consists of the rest of the packet after the
      upper-layer header or after any header (i.e., initial IPv6 header
      or extension header) that contains a Next Header value of No Next
      Header.

   The Fragmentable Part of the original packet is divided into
   fragments.  The lengths of the fragments must be chosen such that the
   resulting fragment packets fit within the MTU of the path to the
   packet's destination(s).  Each complete fragment, except possibly the
   last ("rightmost") one, is an integer multiple of 8 octets long.

   The fragments are transmitted in separate "fragment packets" as
   illustrated:

   original packet:

   +-----------------+-----------------+--------+--------+-//-+--------+
   |  Per-Fragment   |Ext & Upper-Layer|  first | second |    |  last  |
   |    Headers      |    Headers      |fragment|fragment|....|fragment|
   +-----------------+-----------------+--------+--------+-//-+--------+

   fragment packets:

   +------------------+---------+-------------------+----------+
   |  Per-Fragment    |Fragment | Ext & Upper-Layer |  first   |
   |    Headers       | Header  |   Headers         | fragment |
   +------------------+---------+-------------------+----------+

   +------------------+--------+-------------------------------+
   |  Per-Fragment    |Fragment|    second                     |
   |    Headers       | Header |   fragment                    |
   +------------------+--------+-------------------------------+
                         o
                         o
                         o
   +------------------+--------+----------+
   |  Per-Fragment    |Fragment|   last   |
   |    Headers       | Header | fragment |
   +------------------+--------+----------+

   The first fragment packet is composed of:

      (1)  The Per-Fragment headers of the original packet, with the
           Payload Length of the original IPv6 header changed to contain
           the length of this fragment packet only (excluding the length
           of the IPv6 header itself), and the Next Header field of the
           last header of the Per-Fragment headers changed to 44.

      (2)  A Fragment header containing:

              The Next Header value that identifies the first header
              after the Per-Fragment headers of the original packet.

              A Fragment Offset containing the offset of the fragment,
              in 8-octet units, relative to the start of the
              Fragmentable Part of the original packet.  The Fragment
              Offset of the first ("leftmost") fragment is 0.

              An M flag value of 1 as this is the first fragment.

              The Identification value generated for the original
              packet.

      (3)  Extension headers, if any, and the Upper-Layer header.  These
           headers must be in the first fragment.  Note: This restricts
           the size of the headers through the Upper-Layer header to the
           MTU of the path to the packet's destinations(s).

      (4)  The first fragment.

   The subsequent fragment packets are composed of:

      (1)  The Per-Fragment headers of the original packet, with the
           Payload Length of the original IPv6 header changed to contain
           the length of this fragment packet only (excluding the length
           of the IPv6 header itself), and the Next Header field of the
           last header of the Per-Fragment headers changed to 44.

      (2)  A Fragment header containing:

              The Next Header value that identifies the first header
              after the Per-Fragment headers of the original packet.

              A Fragment Offset containing the offset of the fragment,
              in 8-octet units, relative to the start of the
              Fragmentable Part of the original packet.

              An M flag value of 0 if the fragment is the last
              ("rightmost") one, else an M flag value of 1.

              The Identification value generated for the original
              packet.

      (3)  The fragment itself.

   Fragments must not be created that overlap with any other fragments
   created from the original packet.

   At the destination, fragment packets are reassembled into their
   original, unfragmented form, as illustrated:

   reassembled original packet:

   +---------------+-----------------+---------+--------+-//--+--------+
   | Per-Fragment  |Ext & Upper-Layer|  first  | second |     | last   |
   |    Headers    |     Headers     |frag data|fragment|.....|fragment|
   +---------------+-----------------+---------+--------+-//--+--------+

   The following rules govern reassembly:

      An original packet is reassembled only from fragment packets that
      have the same Source Address, Destination Address, and Fragment
      Identification.

      The Per-Fragment headers of the reassembled packet consists of all
      headers up to, but not including, the Fragment header of the first
      fragment packet (that is, the packet whose Fragment Offset is
      zero), with the following two changes:

         The Next Header field of the last header of the Per-Fragment
         headers is obtained from the Next Header field of the first
         fragment's Fragment header.

         The Payload Length of the reassembled packet is computed from
         the length of the Per-Fragment headers and the length and
         offset of the last fragment.  For example, a formula for
         computing the Payload Length of the reassembled original packet
         is:

            PL.orig = PL.first - FL.first - 8 + (8 * FO.last) + FL.last


            where
            PL.orig  =  Payload Length field of reassembled packet.
            PL.first =  Payload Length field of first fragment packet.
            FL.first =  length of fragment following Fragment header of
                        first fragment packet.
            FO.last  =  Fragment Offset field of Fragment header of last
                        fragment packet.
            FL.last  =  length of fragment following Fragment header of
                        last fragment packet.

         The Fragmentable Part of the reassembled packet is constructed
         from the fragments following the Fragment headers in each of
         the fragment packets.  The length of each fragment is computed
         by subtracting from the packet's Payload Length the length of
         the headers between the IPv6 header and fragment itself; its
         relative position in Fragmentable Part is computed from its
         Fragment Offset value.

         The Fragment header is not present in the final, reassembled
         packet.

         If the fragment is a whole datagram (that is, both the Fragment
         Offset field and the M flag are zero), then it does not need
         any further reassembly and should be processed as a fully
         reassembled packet (i.e., updating Next Header, adjust Payload
         Length, removing the Fragment header, etc.).  Any other
         fragments that match this packet (i.e., the same IPv6 Source
         Address, IPv6 Destination Address, and Fragment Identification)
         should be processed independently.

   The following error conditions may arise when reassembling fragmented
   packets:

      o  If insufficient fragments are received to complete reassembly
         of a packet within 60 seconds of the reception of the first-
         arriving fragment of that packet, reassembly of that packet
         must be abandoned and all the fragments that have been received
         for that packet must be discarded.  If the first fragment
         (i.e., the one with a Fragment Offset of zero) has been
         received, an ICMP Time Exceeded -- Fragment Reassembly Time
         Exceeded message should be sent to the source of that fragment.

      o  If the length of a fragment, as derived from the fragment
         packet's Payload Length field, is not a multiple of 8 octets
         and the M flag of that fragment is 1, then that fragment must
         be discarded and an ICMP Parameter Problem, Code 0, message
         should be sent to the source of the fragment, pointing to the
         Payload Length field of the fragment packet.

      o  If the length and offset of a fragment are such that the
         Payload Length of the packet reassembled from that fragment
         would exceed 65,535 octets, then that fragment must be
         discarded and an ICMP Parameter Problem, Code 0, message should
         be sent to the source of the fragment, pointing to the Fragment
         Offset field of the fragment packet.

      o  If the first fragment does not include all headers through an
         Upper-Layer header, then that fragment should be discarded and
         an ICMP Parameter Problem, Code 3, message should be sent to
         the source of the fragment, with the Pointer field set to zero.

      o  If any of the fragments being reassembled overlap with any
         other fragments being reassembled for the same packet,
         reassembly of that packet must be abandoned and all the
         fragments that have been received for that packet must be
         discarded, and no ICMP error messages should be sent.

         It should be noted that fragments may be duplicated in the
         network.  Instead of treating these exact duplicate fragments
         as overlapping fragments, an implementation may choose to
         detect this case and drop exact duplicate fragments while
         keeping the other fragments belonging to the same packet.

   The following conditions are not expected to occur frequently but are
   not considered errors if they do:

      The number and content of the headers preceding the Fragment
      header of different fragments of the same original packet may
      differ.  Whatever headers are present, preceding the Fragment
      header in each fragment packet, are processed when the packets
      arrive, prior to queueing the fragments for reassembly.  Only
      those headers in the Offset zero fragment packet are retained in
      the reassembled packet.

      The Next Header values in the Fragment headers of different
      fragments of the same original packet may differ.  Only the value
      from the Offset zero fragment packet is used for reassembly.

      Other fields in the IPv6 header may also vary across the fragments
      being reassembled.  Specifications that use these fields may
      provide additional instructions if the basic mechanism of using
      the values from the Offset zero fragment is not sufficient.  For
      example, Section 5.3 of [RFC3168] describes how to combine the
      Explicit Congestion Notification (ECN) bits from different
      fragments to derive the ECN bits of the reassembled packet.
      


It should say:

4.5.  Fragment Header

   The Fragment header is used by an IPv6 source to send a packet larger
   than would fit in the path MTU to its destination.  (Note: unlike
   IPv4, fragmentation in IPv6 is performed only by source nodes, not by
   routers along a packet's delivery path -- see [RFC8200].)  The
   Fragment header is identified by a Next Header value of 44 in the
   immediately preceding header and has the following format:

   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  Next Header  |   Reserved    |      Fragment Offset    |Res|M|
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                         Identification                        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

      Next Header         8-bit selector.  Identifies the initial header
                          type of the Fragmentable Part of the original
                          packet (defined below).  Uses the same values
                          as the IPv4 Protocol field [IANA-PN].

      Reserved            8-bit reserved field.  Initialized to zero for
                          transmission; ignored on reception.

      Fragment Offset     13-bit unsigned integer.  The offset, in
                          8-octet units, of the data following this
                          header, relative to the start of the
                          Fragmentable Part of the original packet.

      Res                 2-bit reserved field.  Initialized to zero for
                          transmission; ignored on reception.

      M flag              1 = more fragments; 0 = last fragment.

      Identification      32 bits.  See description below.

   In order to send a packet that is too large to fit in the MTU of the
   path to its destination, a source node may divide the packet into
   fragments and send each fragment as a separate packet, to be
   reassembled at the receiver.

   For every packet that is to be fragmented, the source node generates
   an Identification value.  The Identification must be different than
   that of any other fragmented packet sent recently* with the same
   Source Address and Destination Address.  If a Routing header is
   present, the Destination Address of concern is that of the final
   destination.

      *  "recently" means within the maximum likely lifetime of a
         packet, including transit time from source to destination and
         time spent awaiting reassembly with other fragments of the same
         packet.  However, it is not required that a source node knows
         the maximum packet lifetime.  Rather, it is assumed that the
         requirement can be met by implementing an algorithm that
         results in a low identification reuse frequency.  Examples of
         algorithms that can meet this requirement are described in
         [RFC7739].

   The initial, large, unfragmented packet is referred to as the
   "original packet", and it is considered to consist of two parts, as
   illustrated:

   original packet:

   +------------------+-----------------------------//----------------+
   |  Per-Fragment    |               Fragmentable                    |
   |    Headers       |                   Part                        |
   +------------------+-----------------------------//----------------+

      The Per-Fragment headers must consist of the IPv6 header plus any
      extension headers that must be processed by nodes en route to the
      destination, that is, all headers up to and including the Routing
      header if present, else the Hop-by-Hop Options header if present,
      else no extension headers.

      The Fragmentable Part consists of the rest of the packet, that is,
      any extension headers that need be processed only by the final
      destination node(s), plus the upper-layer header and data.

   The Fragmentable Part of the original packet is divided into
   fragments.  The lengths of the fragments must be chosen such that the
   resulting fragment packets fit within the MTU of the path to the
   packet's destination(s).  Each complete fragment, except possibly the
   last ("rightmost") one, is an integer multiple of 8 octets long.

   The fragments are transmitted in separate "fragment packets" as
   illustrated:

   original packet:

    +------------------+--------------+--------------+--//--+----------+
    |  Per-Fragment    |    first     |    second    |      |   last   |
    |   Headers        |   fragment   |   fragment   | .... | fragment |
    +------------------+--------------+--------------+--//--+----------+

   fragment packets:

   +------------------+--------+--------------+
   |  Per-Fragment    |Fragment|    first     |
   |    Headers       | Header |   fragment   |
   +------------------+--------+--------------+

   +------------------+--------+--------------+
   |  Per-Fragment    |Fragment|    second    |
   |    Headers       | Header |   fragment   |
   +------------------+--------+--------------+
                         o
                         o
                         o
   +------------------+--------+----------+
   |  Per-Fragment    |Fragment|   last   |
   |    Headers       | Header | fragment |
   +------------------+--------+----------+

   The first fragment packet is composed of:

      (1)  The Per-Fragment headers of the original packet, with the
           Payload Length of the original IPv6 header changed to contain
           the length of this fragment packet only (excluding the length
           of the IPv6 header itself), and the Next Header field of the
           last header of the Per-Fragment headers changed to 44.

      (2)  A Fragment header containing:

              The Next Header value that identifies the first header
              after the Per-Fragment headers of the original packet.

              A Fragment Offset containing the offset of the fragment,
              in 8-octet units, relative to the start of the
              Fragmentable Part of the original packet.  The Fragment
              Offset of the first ("leftmost") fragment is 0.

              An M flag value of 1 as this is the first fragment.

              The Identification value generated for the original
              packet.

      (3)  Extension headers, if any, and the Upper-Layer header.  These
           headers must be in the first fragment.  Note: This restricts
           the size of the headers through the Upper-Layer header to the
           MTU of the path to the packet's destinations(s).

           Extension headers are all other extension headers that are
           not included in the Per-Fragment headers part of the packet.
           For this purpose, the Encapsulating Security Payload (ESP) is
           not considered an extension header.  The Upper-Layer header
           is the first upper-layer header that is not an IPv6 extension
           header.  Examples of upper-layer headers include TCP, UDP,
           IPv4, IPv6, ICMPv6, and as noted ESP.

      (4)  The remainder of the first fragment.

   The subsequent fragment packets are composed of:

      (1)  The Per-Fragment headers of the original packet, with the
           Payload Length of the original IPv6 header changed to contain
           the length of this fragment packet only (excluding the length
           of the IPv6 header itself), and the Next Header field of the
           last header of the Per-Fragment headers changed to 44.

      (2)  A Fragment header containing:

              The Next Header value that identifies the first header
              after the Per-Fragment headers of the original packet.

              A Fragment Offset containing the offset of the fragment,
              in 8-octet units, relative to the start of the
              Fragmentable Part of the original packet.

              An M flag value of 0 if the fragment is the last
              ("rightmost") one, else an M flag value of 1.

              The Identification value generated for the original
              packet.

      (3)  The fragment itself.

   Fragments must not be created that overlap with any other fragments
   created from the original packet.

   At the destination, fragment packets are reassembled into their
   original, unfragmented form, as illustrated:

   reassembled original packet:

   +------------------+----------------------//------------------------+
   |  Per-Fragment    |                 Fragmentable                   |
   |    Headers       |                     Part                       |
   +------------------+----------------------//------------------------+

   The following rules govern reassembly:

      An original packet is reassembled only from fragment packets that
      have the same Source Address, Destination Address, and Fragment
      Identification.

      The Per-Fragment headers of the reassembled packet consists of all
      headers up to, but not including, the Fragment header of the first
      fragment packet (that is, the packet whose Fragment Offset is
      zero), with the following two changes:

         The Next Header field of the last header of the Per-Fragment
         headers is obtained from the Next Header field of the first
         fragment's Fragment header.

         The Payload Length of the reassembled packet is computed from
         the length of the Per-Fragment headers and the length and
         offset of the last fragment.  For example, a formula for
         computing the Payload Length of the reassembled original packet
         is:

            PL.orig = PL.first - FL.first - 8 + (8 * FO.last) + FL.last


            where
            PL.orig  =  Payload Length field of reassembled packet.
            PL.first =  Payload Length field of first fragment packet.
            FL.first =  length of fragment following Fragment header of
                        first fragment packet.
            FO.last  =  Fragment Offset field of Fragment header of last
                        fragment packet.
            FL.last  =  length of fragment following Fragment header of
                        last fragment packet.

         The Fragmentable Part of the reassembled packet is constructed
         from the fragments following the Fragment headers in each of
         the fragment packets.  The length of each fragment is computed
         by subtracting from the packet's Payload Length the length of
         the headers between the IPv6 header and fragment itself; its
         relative position in Fragmentable Part is computed from its
         Fragment Offset value.

         The Fragment header is not present in the final, reassembled
         packet.

         If the fragment is a whole datagram (that is, both the Fragment
         Offset field and the M flag are zero), then it does not need
         any further reassembly and should be processed as a fully
         reassembled packet (i.e., updating Next Header, adjust Payload
         Length, removing the Fragment header, etc.).  Any other
         fragments that match this packet (i.e., the same IPv6 Source
         Address, IPv6 Destination Address, and Fragment Identification)
         should be processed independently.

   The following error conditions may arise when reassembling fragmented
   packets:

      o  If insufficient fragments are received to complete reassembly
         of a packet within 60 seconds of the reception of the first-
         arriving fragment of that packet, reassembly of that packet
         must be abandoned and all the fragments that have been received
         for that packet must be discarded.  If the first fragment
         (i.e., the one with a Fragment Offset of zero) has been
         received, an ICMP Time Exceeded -- Fragment Reassembly Time
         Exceeded message should be sent to the source of that fragment.

      o  If the length of a fragment, as derived from the fragment
         packet's Payload Length field, is not a multiple of 8 octets
         and the M flag of that fragment is 1, then that fragment must
         be discarded and an ICMP Parameter Problem, Code 0, message
         should be sent to the source of the fragment, pointing to the
         Payload Length field of the fragment packet.

      o  If the length and offset of a fragment are such that the
         Payload Length of the packet reassembled from that fragment
         would exceed 65,535 octets, then that fragment must be
         discarded and an ICMP Parameter Problem, Code 0, message should
         be sent to the source of the fragment, pointing to the Fragment
         Offset field of the fragment packet.

      o  If the first fragment does not include all headers through an
         Upper-Layer header, then that fragment should be discarded and
         an ICMP Parameter Problem, Code 3, message should be sent to
         the source of the fragment, with the Pointer field set to zero.

      o  If any of the fragments being reassembled overlap with any
         other fragments being reassembled for the same packet,
         reassembly of that packet must be abandoned and all the
         fragments that have been received for that packet must be
         discarded, and no ICMP error messages should be sent.

         It should be noted that fragments may be duplicated in the
         network.  Instead of treating these exact duplicate fragments
         as overlapping fragments, an implementation may choose to
         detect this case and drop exact duplicate fragments while
         keeping the other fragments belonging to the same packet.

   The following conditions are not expected to occur frequently but are
   not considered errors if they do:

      The number and content of the headers preceding the Fragment
      header of different fragments of the same original packet may
      differ.  Whatever headers are present, preceding the Fragment
      header in each fragment packet, are processed when the packets
      arrive, prior to queueing the fragments for reassembly.  Only
      those headers in the Offset zero fragment packet are retained in
      the reassembled packet.

      The Next Header values in the Fragment headers of different
      fragments of the same original packet may differ.  Only the value
      from the Offset zero fragment packet is used for reassembly.

      Other fields in the IPv6 header may also vary across the fragments
      being reassembled.  Specifications that use these fields may
      provide additional instructions if the basic mechanism of using
      the values from the Offset zero fragment is not sufficient.  For
      example, Section 5.3 of [RFC3168] describes how to combine the
      Explicit Congestion Notification (ECN) bits from different
      fragments to derive the ECN bits of the reassembled packet.


Notes:

This errata replaces and resolves the issues raised in Errata 5170, 5171, 5172, 5173.   Credit goes to Fernando Gont for reporting the issues raised in these errata.   They correctly reported that the text in Section 4.5 of RFC8200 defined Fragment Offset as pointing to “Fragmentable Part”, this was an error and should have pointed to “Extension & Upper-Layer Headers”.

After review by the 6man working group the conclusion was to fix the issue in a more general way than what was proposed in Errata 5170, 5171, 5172, 5173, hence the need for a new errata.
```

</details>

<br>**Explanation:**
The original description of IPv6 packet fragmentation incorrectly divides the original packet into three parts (Per-Fragment Headers, Extension & Upper-Layer Headers, and Fragmentable Part), and incorrectly describes the composition of the resulting fragment packets.  The correction simplifies the description to two parts (Per-Fragment Headers and Fragmentable Part), and more accurately describes the composition of the fragment packets, resolving inconsistencies with the actual behavior of IPv6 fragmentation.

---

<details>
<summary><b>Errata 6517</b> from <b>RFC 8214</b> - Virtual Private Wire Service Support in Ethernet VPN (August 2017)</summary>

```
Section 5 says:


   Finally, EVPN may employ data-plane egress link protection mechanisms
   not available in VPWS.  This can be done by the primary PE (on local
   AC down) using the label advertised in the per-EVI Ethernet A-D route
   by the backup PE to encapsulate the traffic and direct it to the
   backup PE.

It should say:

   Finally, EVPN may employ data-plane egress link protection mechanisms.
   This can be done by the primary PE (on local AC down) using the label 
   advertised in the per-EVI Ethernet A-D route by the backup PE to
   encapsulate the traffic and direct it to the backup PE.  Similar behavior
   for LDP-signaled PWs can be achieved using LDP extensions defined in RFC 8104, 
   but the EVPN-based solution is simpler to implement (e.g., does not require 
   context-specific label spaces) and operate.





Notes:

RFC 8104 "Pseudowire (PW) Endpoint Fast Failure Protection" defines a solution for egress PW endpoint protection that provides fast local protection against failure of the primary egress PE and failure of the Attachment Circuit of this PE, so that the claim that the data-plane egress link protection mechanisms are not available for LDP-signaled PWs is factually inaccurate. However, the solution defined in RFC 8104is much more complicated both from the POV of implementation and from the operational POV, while the EVPN-based solution is quite straightforward.
```

</details>

<br>**Explanation:**
The original text incorrectly states that data-plane egress link protection mechanisms are not available in LDP-signaled PWs.  The corrected text acknowledges that such mechanisms exist (as defined in RFC 8104) but points out that the EVPN-based solution is simpler.  The original text's factual inaccuracy makes it inconsistent.

---

<details>
<summary><b>Errata 5715</b> from <b>RFC 8224</b> - Authenticated Identity Management in the Session Initiation Protocol (SIP) (February 2018)</summary>

```
Section 4.1 says:


o  Second, the JSON "dest" array MUST be populated.  If the
   destination identity is a telephone number, then the array MUST be
   populated with a JSON object containing a "tn" element with a
   value set to the value of the quoted destination identity, a
   canonicalized telephone number (see Section 8.3).  Otherwise, the
   array MUST be populated with a JSON object containing a "uri"
   element, set to the value of the addr-spec component of the
   To header field, which is the AoR to which the request is being
   sent, per the procedures in Section 8.5.  Multiple JSON objects
   are permitted in "dest" for future compatibility reasons.

...

The "orig" and "dest" arrays may contain identifiers of heterogeneous
type; for example, the "orig" array might contain a "tn" claim, while
the "dest" contains a "uri" claim.  Also note that in some cases, the
"dest" array may be populated with more than one value.  This could,
for example, occur when multiple "dest" identities are specified in a
meshed conference.  Defining how a SIP implementation would align
multiple destination identities in PASSporT with such systems is left
as a subject for future specifications.

It should say:

o  Second, the JSON "dest" object MUST be populated.  If the
   destination identity is a telephone number, then the object MUST
   contain a "tn" element with a value set to an array containing the
   value of the quoted destination identity, a
   canonicalized telephone number (see Section 8.3).  Otherwise, the
   object MUST contain a "uri" element, set to an array containing
   the value of the addr-spec component of the
   To header field, which is the AoR to which the request is being
   sent, per the procedures in Section 8.5.  Additional elements
   are permitted in "dest" for future compatibility reasons.

...

The "orig" and "dest" objects may contain identifiers of heterogeneous
type; for example, the "orig" object might contain a "tn" claim, while
the "dest" contains a "uri" claim.  Also note that in some cases, the
"dest" object may be populated with more than one claim, and its claim
value arrays may contain more than one value.  This could,
for example, occur when multiple "dest" identities are specified in a
meshed conference.  Defining how a SIP implementation would align
multiple destination identities in PASSporT with such systems is left
as a subject for future specifications.

Notes:

The description of the "dest" element does not match RFC8225 or the example that is provided in this section.

The terminology is a bit less clear than in RFC8225 section 5.2.1, in that no differentiation is made between the top level "claims" and embedded "identity claims". The proposed correction does not address this lack of clarity, however.

From RFC8225 section 5.2.1:

The "dest" claim is a JSON object with the claim name of "dest" and
MUST have at least one identity claim object.  The "dest" claim value
is an array containing one or more identity claim JSON objects
representing the destination identities of any type (currently "tn"
or "uri").  If the "dest" claim value array contains both "tn" and
"uri" claim names, the JSON object should list the "tn" array first
and the "uri" array second.  Within the "tn" and "uri" arrays, the
identity strings should be put in lexicographical order, including
the scheme-specific portion of the URI characters.

(The above text might need correction as well, because it refers to the '"dest" claim value array'.)
```

</details>

<br>**Explanation:**
The original description of the "dest" element is inconsistent with RFC 8225 and the provided example. The original description uses an array for the "dest" element, while RFC 8225 and the example use an object containing arrays for telephone numbers and URIs.  The corrected description uses an object containing arrays, aligning with RFC 8225 and the example.

---

<details>
<summary><b>Errata 6499</b> from <b>RFC 8224</b> - Authenticated Identity Management in the Session Initiation Protocol (SIP) (February 2018)</summary>

```
Section 4 says:


Identity = "Identity" HCOLON signed-identity-digest SEMI
          ident-info *( SEMI ident-info-params )
signed-identity-digest = 1*(base64-char / ".")
ident-info = "info" EQUAL ident-info-uri
ident-info-uri = LAQUOT absoluteURI RAQUOT
ident-info-params = ident-info-alg / ident-type /
    ident-info-extension
ident-info-alg = "alg" EQUAL token
ident-type = "ppt" EQUAL token
ident-info-extension = generic-param

base64-char = ALPHA / DIGIT / "/" / "+"


It should say:

Identity = "Identity" HCOLON signed-identity-digest SEMI
          ident-info *( SEMI ident-info-params )
signed-identity-digest = 1*(base64url-char / ".")
ident-info = "info" EQUAL ident-info-uri
ident-info-uri = LAQUOT absoluteURI RAQUOT
ident-info-params = ident-info-alg / ident-type /
    ident-info-extension
ident-info-alg = "alg" EQUAL token
ident-type = "ppt" EQUAL token
ident-info-extension = generic-param

base64url-char = ALPHA / DIGIT / "-" / "_"


Notes:

RFC 8225 makes it clear that the encoding is BASE4URL, not the standard BASE64 encoding.

See also:
- https://datatracker.ietf.org/doc/html/rfc8224#section-4.1.1
- https://datatracker.ietf.org/doc/html/rfc7515#appendix-F
- https://datatracker.ietf.org/doc/html/rfc7515#appendix-C
- https://datatracker.ietf.org/doc/html/rfc4648#section-5
```

</details>

<br>**Explanation:**
The original ABNF uses base64-char, which is not appropriate for the application. The correction uses base64url-char, which is consistent with RFC 8225 and the intended use of base64url encoding for the signed-identity-digest.

---

<details>
<summary><b>Errata 5610</b> from <b>RFC 8226</b> - Secure Telephone Identity Credentials: Certificates (February 2018)</summary>

```
Section Appendix A says:


    JWTClaimPermittedValuesList ::= SEQUENCE SIZE (1..MAX) Of
                                      JWTClaimPermittedValues

It should say:

    JWTClaimPermittedValuesList ::= SEQUENCE SIZE (1..MAX) OF
                                      JWTClaimPermittedValues

Notes:

The ASN.1 Compiler require "OF" to be all capital letters.
```

</details>

<br>**Explanation:**
This is a syntax error in the ASN.1 module.

---

<details>
<summary><b>Errata 5376</b> from <b>RFC 8231</b> - Path Computation Element Communication Protocol (PCEP) Extensions for Stateful PCE (September 2017)</summary>

```
Section 7.2 says:


In case of SRP-ID-number wrapping, the last
   SRP-ID-number before the wrapping MUST be explicitly acknowledged, to
   avoid a situation where SRP-ID-numbers remain unacknowledged after
   the wrap.  This means that the PCC may need to issue two PCUpd
   messages on detecting a wrap.

It should say:

In case of SRP-ID-number wrapping, the last
   SRP-ID-number before the wrapping MUST be explicitly acknowledged, to
   avoid a situation where SRP-ID-numbers remain unacknowledged after
   the wrap.  This means that the PCC may need to issue two PCRpt
   messages on detecting a wrap.

Notes:

incase of srp id wrap, once PCC detects it, PCC needs to issue PCRpt message not PCUpd message.
```

</details>

<br>**Explanation:**
The original text incorrectly states that the PCC should issue PCUpd messages to acknowledge SRP-ID-number wrapping. The correction specifies that PCRpt messages should be used instead, which is consistent with the protocol's operation. This inconsistency would affect the handling of SRP-ID-number wrapping and could lead to unacknowledged SRP-ID-numbers.

---

<details>
<summary><b>Errata 5970</b> from <b>RFC 8231</b> - Path Computation Element Communication Protocol (PCEP) Extensions for Stateful PCE (September 2017)</summary>

```
Section 8.5 says:


19       Invalid Operation

                Error-value
                1:   Attempted LSP Update Request for a non-delegated
                     LSP.  The PCEP-ERROR object is followed by the LSP
                     object that identifies the LSP.

It should say:

19       Invalid Operation

                Error-value
                1:   Attempted LSP Update Request for a non-delegated
                     LSP.

Notes:

RFC 8231 Section 6.3 - LSP Object is not part of PCErr message.
```

</details>

<br>**Explanation:**
The original text incorrectly states that the LSP object is included in the PCErr message for error-value 1. The corrected text removes the reference to the LSP object, as it is not part of the PCErr message. This inconsistency affects the interpretation and implementation of error reporting in stateful PCE.

---

<details>
<summary><b>Errata 6231</b> from <b>RFC 8231</b> - Path Computation Element Communication Protocol (PCEP) Extensions for Stateful PCE (September 2017)</summary>

```
Section 8.5 says:


      20       LSP State Synchronization Error

                Error-value
                1:   A PCE indicates to a PCC that it cannot process (an
                     otherwise valid) LSP State Report.  The PCEP-ERROR
                     object is followed by the LSP object that
                     identifies the LSP.

It should say:

      20       LSP State Synchronization Error

                Error-value
                1:   A PCE indicates to a PCC that it cannot process (an
                     otherwise valid) LSP State Report.  

Notes:

This is a companion errata to https://www.rfc-editor.org/errata/eid5970 which identified the issue in Error-type 19 Error-value 1. The same issue exists for Error-type 20 Error-value 1 i.e. LSP Object is not part of the PCErr message.
```

</details>

<br>**Explanation:**
The original text incorrectly states that the LSP object is included in the PCErr message for error-value 1. The corrected text removes the reference to the LSP object, as it is not part of the PCErr message. This inconsistency affects the interpretation and implementation of error reporting in stateful PCE.

---

<details>
<summary><b>Errata 6289</b> from <b>RFC 8231</b> - Path Computation Element Communication Protocol (PCEP) Extensions for Stateful PCE (September 2017)</summary>

```
Section 7.3.2 says:


   Length (16 bits): indicates the total length of the TLV in octets and
   MUST be greater than 0.  The TLV MUST be zero-padded so that the TLV
   is 4-octet aligned.

It should say:

   Length (16 bits): indicates the length of the value portion of the 
   TLV in octets and MUST be greater than 0.  The TLV MUST be zero-
   padded so that the TLV is 4-octet aligned.


Notes:

The "total length of the TLV" is incorrect, as in PCEP the TLV formatting is as per RFC 5440 which requires the length to be of the value portion only. The other text such as "MUST be greater than 0", the padding rules along with "without a NULL terminator" also point to the fact that the intention of the authors/WG was not "total" (and it is simply a mistake).
```

</details>

<br>**Explanation:**
The original text defines the Length field as the total length of the TLV, including the type and length fields.  This is inconsistent with RFC 5440, which specifies that the length field represents only the length of the value portion of the TLV. The correction clarifies that the length field represents the length of the value portion only, resolving the inconsistency.

---

<details>
<summary><b>Errata 5878</b> from <b>RFC 8288</b> - Web Linking (October 2017)</summary>

```
Section B.2 says:


       15.  Let star_param_names be the set of param_names in the
            (param_name, param_value) tuples of link_parameters where
            the last character of param_name is an asterisk ("*").
       16.  For each star_param_name in star_param_names:
            1.  Let base_param_name be star_param_name with the last
                character removed.
            2.  If the implementation does not choose to support an
                internationalised form of a parameter named
                base_param_name for any reason (including, but not
                limited to, it being prohibited by the parameter's
                specification), remove all tuples from link_parameters
                whose first member is star_param_name, and skip to the
                next star_param_name.
            3.  Remove all tuples from link_parameters whose first
                member is base_param_name.
            4.  Change the first member of all tuples in link_parameters
                whose first member is star_param_name to
                base_param_name.

It should say:

       15.  Let star_param_names be the set of param_names in the
            (param_name, param_value) tuples of target_attributes where
            the last character of param_name is an asterisk ("*").
       16.  For each star_param_name in star_param_names:
            1.  Let base_param_name be star_param_name with the last
                character removed.
            2.  If the implementation does not choose to support an
                internationalised form of a parameter named
                base_param_name for any reason (including, but not
                limited to, it being prohibited by the parameter's
                specification), remove all tuples from target_attributes
                whose first member is star_param_name, and skip to the
                next star_param_name.
            3.  Remove all tuples from target_attributes whose first
                member is base_param_name.
            4.  Change the first member of all tuples in target_attributes
                whose first member is star_param_name to
                base_param_name.

Notes:

The modified link_parameters value is not used, but target_attributes is. Additionally, the normative part of the document states that the RFC 8187 decoding scheme MAY be used for target attributes (especially extension attributes), not the ones that belong to the general link model.
```

</details>

<br>**Explanation:**
The algorithm description uses the variable `link_parameters` which is not used in the algorithm but `target_attributes` which is the correct variable to use.  The algorithm is therefore inconsistent with its own definition.

---

<details>
<summary><b>Errata 5622</b> from <b>RFC 8306</b> - Extensions to the Path Computation Element Communication Protocol (PCEP) for Point-to-Multipoint Traffic Engineering Label Switched Paths (November 2017)</summary>

```
Section 3.13 says:


   The total PCEP message length, including the common header, is
   16 bytes.

It should say:

   The total PCEP message length, including the common header, is
   (2^16)-1 bytes.

Notes:

The message length field is 16 bits, so the maximum message length is (2^16)-1.
```

</details>

<br>**Explanation:**
The original text incorrectly states a fixed message length of 16 bytes, while the message length field is actually 16 bits, allowing for a much larger maximum length.  This inconsistency would lead to implementations incorrectly limiting the maximum PCEP message size. For reference, check Section 6.1 of RFC5440.

---

<details>
<summary><b>Errata 7588</b> from <b>RFC 8325</b> - Mapping Diffserv to IEEE 802.11 (February 2018)</summary>

```
Section 2.3 says:


There are mappings provided in [IEEE.802.11-2016], Annex V Tables V-1 and V2,

It should say:

There are mappings provided in [IEEE.802.11-2016], Annex R Tables R-1 and R-2,

Notes:

It is Annex R in both the 2016 and 2020 editions
```

</details>

<br>**Explanation:**
The original text refers to Annex V Tables V-1 and V2 in [IEEE.802.11-2016], which is incorrect. The mappings are actually in Annex R Tables R-1 and R-2, creating an inconsistency between the reference and the actual location of the mappings.

---

<details>
<summary><b>Errata 5402</b> from <b>RFC 8326</b> - Graceful BGP Session Shutdown (March 2018)</summary>

```
Section C.2.2. says:


      4.  If, for any reason, RR3 processes the withdraw generated in
          step 3 before processing the update generated in step 2, RR3
          transiently suffers from unreachability for the affected
          prefix.

It should say:

      4.  If, for any reason, RR2 processes the withdraw generated in
          step 3 before processing the update generated in step 2, RR2
          transiently suffers from unreachability for the affected
          prefix.

Notes:

The original text names RR3, but it should be RR2. This becomes evident when one works through the example using a diagram.
```

</details>

<br>**Explanation:**
The original text refers to RR3, when it should refer to RR2.  This inconsistency affects the accuracy of the example and could lead to misinterpretations of the graceful BGP session shutdown procedure.

---

<details>
<summary><b>Errata 6900</b> from <b>RFC 8345</b> - A YANG Data Model for Network Topologies (March 2018)</summary>

```
Section Appendix C says:


"network-id": "otn-hc",

It should say:

"network-id": "foo:otn-hc",

Notes:

This is to match the network-id type:

     typedef network-id {
       type inet:uri;
       description
         "Identifier for a network.  The precise structure of the
          network-id will be up to the implementation.  The identifier
          SHOULD be chosen such that the same network will always be
          identified through the same identifier, even if the data model
          is instantiated in separate datastores.  An implementation MAY
          choose to capture semantics in the identifier -- for example,
          to indicate the type of network.";
     }
```

</details>

<br>**Explanation:**
The original example uses a simple string for network-id, which is inconsistent with the definition of the network-id type as an IETF URI.  The correction adds a prefix to make it a valid IETF URI, resolving the inconsistency.

---

<details>
<summary><b>Errata 5870</b> from <b>RFC 8360</b> - Resource Public Key Infrastructure (RPKI) Validation Reconsidered (April 2018)</summary>

```
Section 4.2.3 says:


       ext-pe-autonomousSysIds-v2 EXTENSION ::= {
         SYNTAX ASIdentifiers
         IDENTIFIED BY id-pe-autonomousSysIds-v2
       }

       id-pe-autonomousSysIds OBJECT IDENTIFIER ::= { id-pe 29 }

It should say:

       ext-pe-autonomousSysIds-v2 EXTENSION ::= {
         SYNTAX ASIdentifiers
         IDENTIFIED BY id-pe-autonomousSysIds-v2
       }

       id-pe-autonomousSysIds-v2 OBJECT IDENTIFIER ::= { id-pe 29 }

Notes:

The "-v2" is missing from the identifier.  It is needed for the ASN.1 module to compile properly.
```

</details>

<br>**Explanation:**
The original ASN.1 definition is missing "-v2" in the OBJECT IDENTIFIER, which is necessary for correct compilation and consistency with the EXTENSION definition.  The missing "-v2" creates an inconsistency that could prevent proper use of the ASN.1 module.

---

<details>
<summary><b>Errata 6646</b> from <b>RFC 8366</b> - A Voucher Artifact for Bootstrapping Protocols (May 2018)</summary>

```
Section 5.2 says:


   {
     "ietf-voucher:voucher": {
       "created-on": "2016-10-07T19:31:42Z",
       "expires-on": "2016-10-21T19:31:42Z",
       "assertion": "verified",
       "serial-number": "JADA123456789",
       "idevid-issuer": "base64encodedvalue==",
       "pinned-domain-cert": "base64encodedvalue==",
       "domain-cert-revocation-checks": "true",
       "last-renewal-date": "2017-10-07T19:31:42Z"
     }
   }

It should say:

   {
     "ietf-voucher:voucher": {
       "created-on": "2016-10-07T19:31:42Z",
       "expires-on": "2016-10-21T19:31:42Z",
       "assertion": "verified",
       "serial-number": "JADA123456789",
       "idevid-issuer": "base64encodedvalue==",
       "pinned-domain-cert": "base64encodedvalue==",
       "domain-cert-revocation-checks": true,
       "last-renewal-date": "2017-10-07T19:31:42Z"
     }
   }

Notes:

domain-cert-revocation-checks is defined as boolean in the YANG specification in section 5.3 of the same RFC 8366. Boolean value in JSON are represented using true/false without the quotes.
```

</details>

<br>**Explanation:**
The original JSON example uses quotes around the boolean value for "domain-cert-revocation-checks", which is incorrect according to the YANG specification. The corrected example removes the quotes, making it consistent with the JSON representation of boolean values.

---

<details>
<summary><b>Errata 5374</b> from <b>RFC 8373</b> - Negotiating Human Language in Real-Time Communications (May 2018)</summary>

```
Section 5.4. says:


   An offer or answer indicating written Greek both ways:

      m=text 45020 RTP/AVP 103 104
      a=hlang-send:gr
      a=hlang-recv:gr

It should say:

   An offer or answer indicating written Greek both ways:

      m=text 45020 RTP/AVP 103 104
      a=hlang-send:el
      a=hlang-recv:el

Notes:

The language tag to represent Greek is "el" per BCP 47.

The IANA language subtag registry has the following entry for Greek:

Type: language
Subtag: el
Description: Modern Greek (1453-)
Added: 2005-10-16

https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry
```

</details>

<br>**Explanation:**
The original example uses the incorrect language tag "gr" for Greek. The correct tag is "el", as defined in BCP 47 and the IANA language subtag registry.  This inconsistency affects the interoperability of implementations that rely on the example to represent the Greek language.

---

<details>
<summary><b>Errata 5387</b> from <b>RFC 8373</b> - Negotiating Human Language in Real-Time Communications (May 2018)</summary>

```
Section 5.4. says:


      m=text 45020 RTP/AVP 103 104
      a=hlang-send:sp pt

      m=audio 49250 RTP/AVP 20
      a=hlang-recv:sp pt

   An answer for the above offer, indicating text in which the callee
   will receive written Spanish and audio in which the callee will send
   spoken Spanish.  (The answering party has no video capability):

      m=video 0 RTP/AVP 31 32
      m=text 45020 RTP/AVP 103 104
      a=hlang-recv:sp

      m=audio 49250 RTP/AVP 20
      a=hlang-send:sp

and later on the same page:

   An answer for the above offer, indicating text in which the callee
   will receive written Spanish, audio in which the callee will send
   spoken Spanish, and supplemental video:

      m=text 45020 RTP/AVP 103 104
      a=hlang-recv:sp

      m=audio 49250 RTP/AVP 20
      a=hlang-send:sp

      m=video 51372 RTP/AVP 31 32


It should say:

      m=text 45020 RTP/AVP 103 104
      a=hlang-send:es pt

      m=audio 49250 RTP/AVP 20
      a=hlang-recv:es pt

   An answer for the above offer, indicating text in which the callee
   will receive written Spanish and audio in which the callee will send
   spoken Spanish.  (The answering party has no video capability):

      m=video 0 RTP/AVP 31 32
      m=text 45020 RTP/AVP 103 104
      a=hlang-recv:es

      m=audio 49250 RTP/AVP 20
      a=hlang-send:es

and later on the same page:

   An answer for the above offer, indicating text in which the callee
   will receive written Spanish, audio in which the callee will send
   spoken Spanish, and supplemental video:

      m=text 45020 RTP/AVP 103 104
      a=hlang-recv:es

      m=audio 49250 RTP/AVP 20
      a=hlang-send:es

      m=video 51372 RTP/AVP 31 32


Notes:

The language tag to represent Spanish is "es" per BCP 47.

The IANA language subtag registry has the following entry for Spanish:

Type: language
Subtag: es
Description: Spanish
Description: Castilian
Added: 2005-10-16

https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry
```

</details>

<br>**Explanation:**
The examples use the incorrect language tag "sp" for Spanish. The correct tag is "es", as defined in BCP 47 and the IANA language subtag registry. This inconsistency affects the interoperability of implementations that rely on the examples to represent the Spanish language.

---

<details>
<summary><b>Errata 6183</b> from <b>RFC 8415</b> - Dynamic Host Configuration Protocol for IPv6 (DHCPv6) (November 2018)</summary>

```
Section 18.3.8 says:


   After all the addresses have been processed, the server generates a
   Reply message by setting the "msg-type" field to REPLY and copying
   the transaction ID from the Decline message into the "transaction-id"
   field.  The client includes a Status Code option (see Section 21.13)
   with the value Success, a Server Identifier option (see Section 21.3)
   with the server's DUID, and a Client Identifier option (see
   Section 21.2) with the client's DUID

It should say:

   After all the addresses have been processed, the server generates a
   Reply message by setting the "msg-type" field to REPLY and copying
   the transaction ID from the Decline message into the "transaction-id"
   field.  The server includes a Status Code option (see Section 21.13)
   with the value Success, a Server Identifier option (see Section 21.3)
   with the server's DUID, and a Client Identifier option (see
   Section 21.2) with the client's DUID

Notes:

The corrected text replaces "client" with "server".

I would like to thank Timothy Winters <tim@qacafe.com> for confirming that this is a bug in the specification.
```

</details>

<br>**Explanation:**
The original text incorrectly attributes the inclusion of options in the Reply message to the client. The correction assigns this responsibility to the server, which is consistent with the DHCPv6 protocol. This inconsistency would affect implementations that incorrectly handle option inclusion in the Reply message.

---

<details>
<summary><b>Errata 5869</b> from <b>RFC 8419</b> - Use of Edwards-Curve Digital Signature Algorithm (EdDSA) Signatures in the Cryptographic Message Syntax (CMS) (August 2018)</summary>

```
Section 2.3 says:


      hashalgs  OBJECT IDENTIFIER  ::=  { joint-iso-itu-t(2)
                              country(16) us(840) organization(1)
                              gov(101) csor(3) nistalgorithm(4) 2 }

It should say:

      hashAlgs  OBJECT IDENTIFIER  ::=  { joint-iso-itu-t(2)
                              country(16) us(840) organization(1)
                              gov(101) csor(3) nistalgorithm(4) 2 }

Notes:

The "hashAlgs" requires a capital letter for the other definitions in the section.
```

</details>

<br>**Explanation:**
"hashAlgs" becomes an undefined term if the only provided definition is for "hashalgs".

---

<details>
<summary><b>Errata 5703</b> from <b>RFC 8422</b> - Elliptic Curve Cryptography (ECC) Cipher Suites for Transport Layer Security (TLS) Versions 1.2 and Earlier (August 2018)</summary>

```
Section 5.10. says:


All RSA signatures must be generated and verified according to
   Section 7.2 of [RFC8017].

It should say:

All RSA signatures must be generated and verified according to
   Section 8.2 of [RFC8017].

Notes:

Section 7.2 of RFC 8017 describes the RSAES-PKCS1-v1_5 encryption scheme. Section 8.2 of RFC 8017 describes the RSASSA-PKCS1-v1_5 signature scheme. The original text contradicts the natural expectation and is probably wrong. If it was intended, there should have been a thorough explanation (like in the well-known case of IKEv1 using the encryption scheme for signing).
```

</details>

<br>**Explanation:**
The original text references the RSAES-PKCS1-v1_5 encryption scheme instead of the RSASSA-PKCS1-v1_5 signature scheme for RSA signature generation and verification. This inconsistency between the referenced section and the expected signature scheme affects the correct implementation of RSA signatures.

---

<details>
<summary><b>Errata 5483</b> from <b>RFC 8446</b> - The Transport Layer Security (TLS) Protocol Version 1.3 (August 2018)</summary>

```
Section 4.2.8.2 says:


For X25519 and X448, the contents of the public value are the byte
string inputs and outputs of the corresponding functions defined in
[RFC7748]: 32 bytes for X25519 and 56 bytes for X448.

It should say:

For X25519 and X448, the contents of the public value are the byte
string outputs of the corresponding functions defined in [RFC7748]: 32
bytes for X25519 and 56 bytes for X448.

Notes:

Per Section 7.4.2 of this RFC and Section 6 of RFC7748, the byte string inputs to the corresponding ECDH scalar multiplication function are the private key and the u-coordinate of the standard public base point, the former of which of course must not be transmitted and the latter of which is a known constant.

Paul Wouters (AD): Resolved but with the following Corrected Text:

For X25519 and X448, the contents of the public value is the K_A or
K_B value described in Section 6 of [RFC7748].  This is 32 bytes for
X25519 and 56 bytes for X448.

From another perspective, including the byte string inputs in the contents of the public value would contradict the resulting content sizes given at the end of the cited paragraph as well as the statement in Section 7.4.2 that the public key put into the KeyShareEntry is the output of ECDH scalar multiplication function.
```

</details>

<br>**Explanation:**
The original text states that the public value includes the byte string inputs to the X25519 and X448 functions, which is incorrect. The correction clarifies that only the byte string outputs are included, resolving the inconsistency with Section 7.4.2 and RFC 7748.

---

<details>
<summary><b>Errata 6142</b> from <b>RFC 8446</b> - The Transport Layer Security (TLS) Protocol Version 1.3 (August 2018)</summary>

```
Section 4.6.1. says:


Clients MUST NOT cache tickets for longer than 7 days

It should say:

Clients MUST NOT use tickets for longer than 7 days

Notes:

"MUST NOT cache" is surely overly zealous and may unnecessarily result in non-compliant implementations
```

</details>

<br>**Explanation:**
The original wording is overly restrictive. While it is recommended to limit ticket usage to 7 days, strictly prohibiting caching is unnecessarily strict. The corrected wording focuses on usage duration rather than caching, which offers more flexibility to implementations without compromising security.

---

<details>
<summary><b>Errata 5615</b> from <b>RFC 8466</b> - A YANG Data Model for Layer 2 Virtual Private Network (L2VPN) Service Delivery (October 2018)</summary>

```
Section 5.10.1 says:


   The svc-bandwidth parameter must include a "cos-id" parameter if the
   "type" is set to "bw-per-cos".  The cos-id can be assigned based on
   either (1) the IEEE 802.1p value [IEEE-802-1D] in the C-tag or
   (2) the Differentiated Services Code Point (DSCP) in the Ethernet
   frame header.  Service frames are metered against the bandwidth
   profile based on the cos-id.

It should say:

   The svc-bandwidth parameter must include a "cos-id" parameter if the
   "type" is set to "bw-per-cos".  The cos-id can be assigned based on
   either (1) the IEEE 802.1p value [IEEE-802-1D] in the C-tag or
   (2) the Differentiated Services Code Point (DSCP) in the IP
   header.  Service frames are metered against the bandwidth
   profile based on the cos-id.

Notes:

The DSCP field is part of the IP packet header, not the Ethernet frame руфвук.
```

</details>

<br>**Explanation:**
The original text incorrectly states that the DSCP value is located in the Ethernet frame header. The correction identifies the IP header as the correct location, resolving the inconsistency. This inconsistency would affect implementations that incorrectly attempt to extract the DSCP value from the Ethernet header.

---

<details>
<summary><b>Errata 6922</b> from <b>RFC 8466</b> - A YANG Data Model for Layer 2 Virtual Private Network (L2VPN) Service Delivery (October 2018)</summary>

```
Section 5.5.2.1 says:


...
             <network-access-id>LA1</network-access-id>
                <service>
                  <svc-bandwidth>
                     <bandwidth>
                       <direction>input-bw</direction>
                        <type>bw-per-cos</type>
                         <cir>450000000</cir>
                         <cbs>20000000</cbs>
                         <eir>1000000000</eir>
                         <ebs>200000000</ebs>
                     </bandwidth>
                    </svc-bandwidth>
...
            <network-access-id>LA2</network-access-id>
                <service>
                  <svc-bandwidth>
                     <bandwidth>
                       <direction>input-bw</direction>
                        <type>bw-per-cos</type>
                         <cir>450000000</cir>
                         <cbs>20000000</cbs>
                         <eir>1000000000</eir>
                         <ebs>200000000</ebs>

It should say:

...
             <network-access-id>LA1</network-access-id>
                <service>
                  <svc-bandwidth>
                     <bandwidth>
                       <direction>input-bw</direction>
                        <type>bw-per-cos</type>
                         <cos-id>10</cos-id>
                         <cir>450000000</cir>
                         <cbs>20000000</cbs>
                         <eir>1000000000</eir>
                         <ebs>200000000</ebs>
                     </bandwidth>
                    </svc-bandwidth>
...
            <network-access-id>LA2</network-access-id>
                <service>
                  <svc-bandwidth>
                     <bandwidth>
                       <direction>input-bw</direction>
                        <type>bw-per-cos</type>
                         <cos-id>10</cos-id>
                         <cir>450000000</cir>
                         <cbs>20000000</cbs>
                         <eir>1000000000</eir>
                         <ebs>200000000</ebs>


Notes:

The cos-id must be included when the bandwidth type is set to "bw-per-cos".
```

</details>

<br>**Explanation:**
The original example omits the required "cos-id" parameter when the "type" attribute is set to "bw-per-cos".  The correction adds the missing "cos-id" parameter, resolving the inconsistency. This inconsistency would lead to implementations incorrectly processing svc-bandwidth configurations.

---

<details>
<summary><b>Errata 6268</b> from <b>RFC 8489</b> - Session Traversal Utilities for NAT (STUN) (February 2020)</summary>

```
Section Appendix B.1 says:


        00 01 00 9c      Request type and message length
        21 12 a4 42      Magic cookie
        78 ad 34 33   }
        c6 ad 72 c0   }  Transaction ID
        29 da 41 2e   }
        00 1e 00 20      USERHASH attribute header
        4a 3c f3 8f   }
        ef 69 92 bd   }
        a9 52 c6 78   }
        04 17 da 0f   }  Userhash value (32 bytes)
        24 81 94 15   }
        56 9e 60 b2   }
        05 c4 6e 41   }
        40 7f 17 04   }
        00 15 00 29      NONCE attribute header
        6f 62 4d 61   }
        74 4a 6f 73   }
        32 41 41 41   }
        43 66 2f 2f   }
        34 39 39 6b   }  Nonce value and padding (3 bytes)
        39 35 34 64   }
        36 4f 4c 33   }
        34 6f 4c 39   }
        46 53 54 76   }
        79 36 34 73   }
        41 00 00 00   }
        00 14 00 0b      REALM attribute header
        65 78 61 6d   }
        70 6c 65 2e   }  Realm value (11 bytes) and padding (1 byte)
        6f 72 67 00   }
        00 1c 00 20      MESSAGE-INTEGRITY-SHA256 attribute header
        e4 68 6c 8f   }
        0e de b5 90   }
        13 e0 70 90   }
        01 0a 93 ef   }  HMAC-SHA256 value
        cc bc cc 54   }
        4c 0a 45 d9   }
        f8 30 aa 6d   }
        6f 73 5a 01   }
 

It should say:

   Password Algorithm: SHA-256 (0x0002), and parameters len (0)

      00 01 00 90     Request type and message length
      21 12 a4 42     Magic cookie
      78 ad 34 33  }
      c6 ad 72 c0  }  Transaction ID
      29 da 41 2e  }
      00 1e 00 20     USERHASH attribute header
      4a 3c f3 8f  }
      ef 69 92 bd  }
      a9 52 c6 78  }
      04 17 da 0f  }  Userhash value (32  bytes)
      24 81 94 15  }
      56 9e 60 b2  }
      05 c4 6e 41  }
      40 7f 17 04  }
      00 15 00 29     NONCE attribute header
      6f 62 4d 61  }
      74 4a 6f 73  }
      32 41 41 41  }
      43 66 2f 2f  }
      34 39 39 6b  }  Nonce value and padding (3 bytes)
      39 35 34 64  }
      36 4f 4c 33  }
      34 6f 4c 39  }
      46 53 54 76  }
      79 36 34 73  }
      41 00 00 00  }
      00 14 00 0b     REALM attribute header
      65 78 61 6d  }
      70 6c 65 2e  }  Realm value (11  bytes) and padding (1 byte)
      6f 72 67 00  }
      00 1d 00 04     PASSWORD-ALGORITHM attribute header
      00 02 00 00     PASSWORD-ALGORITHM value (4 bytes)
      00 1c 00 20     MESSAGE-INTEGRITY-SHA256 attribute header
      b5 c7 bf 00  }
      5b 6c 52 a2  }
      1c 51 c5 e8  }
      92 f8 19 24  }  HMAC-SHA256 value
      13 62 96 cb  }
      92 7c 43 14  }
      93 09 27 8c  }
      c6 51 8e 65  }

Notes:

The message length in the test vector (first line, value: 9c) is the absolute length of the whole test vector. However from section 5. STUN Message Structure

"The message length MUST contain the size of the message in bytes, not
   including the 20-byte STUN header."

So the message length in the header should be 20 bytes less than absolute length of the whole message. 

0x9C - 20 = 0x88.

Also the section was missing an indication of what password algorithm that was to be used to derive the password. As SHA-256 was used, and is not the default the PASSWORD-ALGORITHM attribute is required. Thus, this corrected message contains that STUN attribute. 

The corrected message has a recalculated Message-Integrity-SHA256 attribute.
```

</details>

<br>**Explanation:**
The original example has an incorrect message length value in the STUN header, which does not account for the header's own size.  Additionally, the example omits the PASSWORD-ALGORITHM attribute and uses an incorrect Message-Integrity-SHA256 value. The correction adjusts the message length, adds the PASSWORD-ALGORITHM attribute, and provides the correct Message-Integrity-SHA256 value, resolving these inconsistencies.

---

<details>
<summary><b>Errata 7312</b> from <b>RFC 8519</b> - YANG Data Model for Network Access Control Lists (ACLs) (March 2019)</summary>

```
Section A.1 says:


   The "example-newco-acl" module is an example of a company's
   proprietary model that augments the "ietf-acl" module.  It shows how
   to use 'augment' with an XML Path Language (XPath) expression to add
   additional match criteria, actions, and default actions for when no
   ACE matches are found.  All these are company proprietary extensions
   or system feature extensions.  "example-newco-acl" is just an
   example, and it is expected that vendors will create their own
   proprietary models.

It should say:

   The "example-newco-acl" module is an example of a company's
   proprietary model that augments the "ietf-access-control-list" module.  It shows how
   to use 'augment' with an XML Path Language (XPath) expression to add
   additional match criteria, actions, and default actions for when no
   ACE matches are found.  All these are company proprietary extensions
   or system feature extensions.  "example-newco-acl" is just an
   example, and it is expected that vendors will create their own
   proprietary models.

Notes:

There is no "ietf-acl" module in the document.
```

</details>

<br>**Explanation:**
The original text refers to a non-existent module ("ietf-acl"). The correct module name is "ietf-access-control-list". This inconsistency could lead to errors in implementations that attempt to use the example module.

---

<details>
<summary><b>Errata 7313</b> from <b>RFC 8519</b> - YANG Data Model for Network Access Control Lists (ACLs) (March 2019)</summary>

```
Section A.1 says:


   The following figure is the tree diagram of example-newco-acl.  In
   this example, /ietf-acl:acls/ietf-acl:acl/ietf-acl:aces/ietf-acl:ace/
   ietf-acl:matches are augmented with two new choices: protocol-
   payload-choice and metadata.  The protocol-payload-choice uses a
   grouping with an enumeration of all supported protocol values.
   Metadata matches apply to fields associated with the packet, that are
   not in the packet header, such as overall packet length.  In another
   example, /ietf-acl:acls/ietf-acl:acl/ietf-acl:aces/ietf-acl:ace/
   ietf-acl:actions are augmented with a new choice of actions.

It should say:

   The following figure is the tree diagram of example-newco-acl.  In
   this example, /acl:acls/acl:acl/acl:aces/acl:ace/acl:matches
   are augmented with two new choices: protocol-payload-choice and
   metadata.  The protocol-payload-choice uses a
   grouping with an enumeration of all supported protocol values.
   Metadata matches apply to fields associated with the packet, that are
   not in the packet header, such as overall packet length.  In another
   example, /acl:acls/acl:acl/acl:aces/acl:ace/acl:actions 
   are augmented with a new choice of actions.

Notes:

The prefix is "acl" not "ietf-acl"

==
module ietf-access-control-list {
  yang-version 1.1;
  namespace "urn:ietf:params:xml:ns:yang:ietf-access-control-list";
  prefix acl;
  ...
==
```

</details>

<br>**Explanation:**
The original text uses the prefix "ietf-acl", which is incorrect; the correct prefix is "acl".  This inconsistency affects the XPath expressions used for augmentation, making them invalid and impacting the implementation.

---

<details>
<summary><b>Errata 5664</b> from <b>RFC 8520</b> - Manufacturer Usage Description Specification (March 2019)</summary>

```
Throughout the document, when it says:


Universal Resource Locator

Universal Resource Name

It should say:

Uniform Resource Locator

Uniform Resource Name

Notes:

Note that there are multiple instances throughout the document.

There haven't been UNIVERSAL resource locators, identifiers, or names for twenty years.    I've labeled these as technical errata because they refer to something that doesn't exist.
```

</details>

<br>**Explanation:**
The RFC uses "Universal Resource Locator" and "Universal Resource Name" throughout the document, while the correct terms are "Uniform Resource Locator" and "Uniform Resource Name".  The use of the incorrect terms represents an inconsistency and may cause confusion for implementers.

---

<details>
<summary><b>Errata 6295</b> from <b>RFC 8520</b> - Manufacturer Usage Description Specification (March 2019)</summary>

```
Section 4.1 says:


For example, if one saw the line "manufacturer" : "flobbidy.example.com",
then all Things that registered with a MUD URL that contained flobbity.example.com in its authority section would match.

It should say:

For example, if one saw the line "manufacturer" : "flobbity.example.com",
then all Things that registered with a MUD URL that contained flobbity.example.com in its authority section would match.

Notes:

Taken at face value it implies somehow a MUD Manager knows about a relationship between two different names flobbidy.example.com and flobbity.example.com in an unexplained way, the correction removes this confusion.
```

</details>

<br>**Explanation:**
The erratum corrects a simple typographical error ("flobbidy" to "flobbity") in an example. However, this error creates an inconsistency within the example.

---

<details>
<summary><b>Errata 7173</b> from <b>RFC 8520</b> - Manufacturer Usage Description Specification (March 2019)</summary>

```
Section 9 says:


Within each access list, access is permitted to packets flowing to or from the Thing that can be mapped to the domain name of "service.bms.example.com".

It should say:

Within each access list, access is permitted to packets flowing to or from the Thing that can be mapped to the domain name of "test.example.com".

Notes:

The subdomain in the Figure does not correspond to the one in the text.
```

</details>

<br>**Explanation:**
The text describes access control for "service.bms.example.com", which is inconsistent with the diagram showing "test.example.com".  This discrepancy affects the understanding of the example and its implementation.

---

<details>
<summary><b>Errata 7819</b> from <b>RFC 8520</b> - Manufacturer Usage Description Specification (March 2019)</summary>

```
Section 13.1 says:


Note: A MUD file may need to be re-signed if the signature expires.

It should say:

Note: A MUD file may need to be re-signed if the certificate needed
to validate the signature expires.

Notes:

The signature does not expire, but the certificate does.
```

</details>

<br>**Explanation:**
The original text incorrectly states that the signature expires. The certificate used to validate the signature is what expires, not the signature itself. This inconsistency affects the understanding of the MUD file management process.

---

<details>
<summary><b>Errata 6435</b> from <b>RFC 8536</b> - The Time Zone Information Format (TZif) (February 2019)</summary>

```
Section 5.2 says:


   >> Response <<

   HTTP/1.1 200 OK
   Date: Fri, 01 Jun 2018 14:52:23 GMT
   Content-Type: application/json; charset="utf-8"
   Content-Length: xxxx

It should say:

   >> Response <<

   HTTP/1.1 200 OK
   Date: Fri, 01 Jun 2018 14:52:23 GMT
   Content-Type: application/json
   Content-Length: xxxx

Notes:

There is no charset parameter on application/json. See https://tools.ietf.org/html/rfc8259#section-11 (last sentence).
```

</details>

<br>**Explanation:**
The original response includes a charset parameter in the Content-Type header for application/json, which is incorrect according to RFC 8259. The correction removes the charset parameter, making the response consistent with the specification.

---

<details>
<summary><b>Errata 6842</b> from <b>RFC 8561</b> - A YANG Data Model for Microwave Radio Link (June 2019)</summary>

```
Section Annex A.3 says:


 "name": "RLT-A:CT-2",
...
           "tx-frequency": 10618000,


It should say:

 "name": "RLT-A:CT-2",
...
           "tx-frequency": 10728000,


Notes:

A.3 describes the XPIC configuration. The tx-frequency for the two CTs under XPIC configuration should be the same, both should be 10728000.

This should be a copy&paste error from A.2 2+0 configuration.

See also the ccamp mailing list: https://mailarchive.ietf.org/arch/msg/ccamp/_VITOVYwAGg_4M2FHntaLpRTHKs/
```

</details>

<br>**Explanation:**
The original example has an incorrect tx-frequency value for the XPIC configuration. The correction provides the correct value, ensuring consistency within the example. This inconsistency would lead to implementations misinterpreting the example configuration.

---

<details>
<summary><b>Errata 6684</b> from <b>RFC 8572</b> - Secure Zero Touch Provisioning (SZTP) (April 2019)</summary>

```
Section 8.1 says:


   The DHCPv4 server MAY include a single instance of the
   OPTION_V4_SZTP_REDIRECT option in DHCP messages it sends.  Servers
   MUST NOT send more than one instance of the OPTION_V4_SZTP_REDIRECT
   option.

It should say:

   The DHCPv4 server MAY include OPTION_V4_SZTP_REDIRECT in DHCP messages it sends.

Notes:

The original text contradicts the statement in the same section:
   "If the length of the 'bootstrap-server-list' field is too large to
   fit into a single option, then OPTION_V4_SZTP_REDIRECT MUST be split
   into multiple instances of the option according to the process
   described in [RFC3396]."
```

</details>

<br>**Explanation:**
The original specification contains conflicting statements regarding the number of OPTION_V4_SZTP_REDIRECT options allowed in DHCP messages. The corrected version removes the restriction on the number of options, aligning with the text in the same section that allows for multiple instances of the option when necessary.

---

<details>
<summary><b>Errata 5877</b> from <b>RFC 8579</b> - Sieve Email Filtering: Delivering to Special-Use Mailboxes (May 2019)</summary>

```
Section 6 says:


require "imapsieve";
require "special-use";
require "environment";
require "variables";

if environment :contains "imap.mailbox" "*" {
    set "mailbox" "${1}";
}

if allof(
    environment "imap.cause" "COPY",
    specialuse_exists "${mailbox}" "\\Junk") {
    redirect "spam-report@example.org";
}


It should say:

require "imapsieve";
require "special-use";
require "environment";
require "variables";

if environment :matches "imap.mailbox" "*" {
    set "mailbox" "${1}";
}

if allof(
    environment "imap.cause" "COPY",
    specialuse_exists "${mailbox}" "\\Junk") {
    redirect "spam-report@example.org";
}


Notes:

The final example is using the ":contains" match type to extract a match variable, which will not work. It should use ":matches" instead.
```

</details>

<br>**Explanation:**
The original example uses the ":contains" match type, which is incorrect for extracting a match variable. The correction uses the ":matches" type, which is the correct match type for this operation.  This inconsistency would affect the operation of the Sieve script.

---

<details>
<summary><b>Errata 6656</b> from <b>RFC 8588</b> - Personal Assertion Token (PaSSporT) Extension for Signature-based Handling of Asserted information using toKENs (SHAKEN) (May 2019)</summary>

```
Section 6 says:


Protected Header
   {
      "alg":"ES256",
      "typ":"passport",
      "ppt":"shaken",
      "x5u":"https://cert.example.org/passport.cer"
   }
   Payload
   {
      "attest":"A"
      "dest":{"tn":["12155550131"]}
      "iat":"1443208345",
      "orig":{"tn":"12155550121"},
      "origid":"123e4567-e89b-12d3-a456-426655440000"
   }

It should say:

Protected Header
   {
      "alg":"ES256",
      "typ":"passport",
      "ppt":"shaken",
      "x5u":"https://cert.example.org/passport.cer"
   }
   Payload
   {
      "attest":"A"
      "dest":{"tn":["12155550131"]}
      "iat":1443208345,
      "orig":{"tn":"12155550121"},
      "origid":"123e4567-e89b-12d3-a456-426655440000"
   }

Notes:

As per RFC8225 (5.1.1), 'iat' is a NumericDate format, which is a number (commonly referred to as a utime). Section 9.4 also specifies that anything that is numeric must be encoded as a number.
```

</details>

<br>**Explanation:**
The original example uses quotes around the "iat" value, which represents a number and should not have quotes according to RFC 8225 and the JSON specification. This inconsistency needs to be corrected to ensure that the example correctly reflects the JSON encoding of numeric values.

---

<details>
<summary><b>Errata 5791</b> from <b>RFC 8620</b> - The JSON Meta Application Protocol (JMAP) (July 2019)</summary>

```
Section 2.1 says:


"capabilities": {
  "urn:ietf:params:jmap:core": {
    "maxSizeUpload": 50000000,
    "maxConcurrentUpload": 8,
    "maxSizeRequest": 10000000,
    "maxConcurrentRequest": 8,
    "maxCallsInRequest": 32,
    "maxObjectsInGet": 256,
    "maxObjectsInSet": 128,
    "collationAlgorithms": [
      "i;ascii-numeric",
      "i;ascii-casemap",
      "i;unicode-casemap"
    ]
  },
  "urn:ietf:params:jmap:mail": {}
  "urn:ietf:params:jmap:contacts": {},
  "https://example.com/apis/foobar": {
    "maxFoosFinangled": 42
  }
}

It should say:

"capabilities": {
  "urn:ietf:params:jmap:core": {
    "maxSizeUpload": 50000000,
    "maxConcurrentUpload": 8,
    "maxSizeRequest": 10000000,
    "maxConcurrentRequests": 8,
    "maxCallsInRequest": 32,
    "maxObjectsInGet": 256,
    "maxObjectsInSet": 128,
    "collationAlgorithms": [
      "i;ascii-numeric",
      "i;ascii-casemap",
      "i;unicode-casemap"
    ]
  },
  "urn:ietf:params:jmap:mail": {},
  "urn:ietf:params:jmap:contacts": {},
  "https://example.com/apis/foobar": {
    "maxFoosFinangled": 42
  }
}

Notes:

In the capabilities section of the example Session Resource response, "maxConcurrentRequest" should be "maxConcurrentRequests". 

In addition, the following line is missing a trailing comma:
  "urn:ietf:params:jmap:mail": {}
```

</details>

<br>**Explanation:**
The example JSON uses the incorrect parameter name "maxConcurrentRequest" instead of the correct parameter name "maxConcurrentRequests". This inconsistency would cause issues when parsing and generating JMAP capability responses.

---

<details>
<summary><b>Errata 6866</b> from <b>RFC 8632</b> - A YANG Data Model for Alarm Management (September 2019)</summary>

```
Section 6 says:


      container older-than {
        presence "Age specification";
        description
          "Matches the 'last-status-change' leaf in the alarm.";
        choice age-spec {


It should say:

      container older-than {
        presence "Age specification";
        description
          "Matches the 'last-changed' leaf in the alarm.";
        choice age-spec {


Notes:

There is no last-status-change leaf in alarm (and it seems there never was).

See also https://mailarchive.ietf.org/arch/msg/ccamp/wmCgk0DQq0lG6S_e59W-MKW8EOQ/
```

</details>

<br>**Explanation:**
The original text refers to a non-existent leaf ("last-status-change"). The correction uses the correct leaf name ("last-changed"), resolving the inconsistency.  This inconsistency would affect implementations that try to use this container to filter alarms.

---

<details>
<summary><b>Errata 7400</b> from <b>RFC 8650</b> - Dynamic Subscription to YANG Events and Datastores over RESTCONF (November 2019)</summary>

```
Section Appendix A.3 says:


   POST /restconf/operations
        /ietf-subscribed-notifications:establish-subscription
   {
      "ietf-subscribed-notifications:input": {
         "stream": "NETCONF",
         "stream-xpath-filter":
           "/ietf-vrrp:vrrp-protocol-error-event[
             protocol-error-reason='checksum-error']/",
      }
   }

       Figure 16: Establishing a Subscription Error Reason via XPath

...

   POST /restconf/operations
        /ietf-subscribed-notifications:modify-subscription
   {
      "ietf-subscribed-notifications:input": {
         "stream": "NETCONF",
         "stream-subtree-filter": {
           "/ietf-vrrp:vrrp-protocol-error-event" : {}
         }
      }
   }
                Figure 17: Example "modify-subscription" RPC

It should say:

   POST /restconf/operations
        /ietf-subscribed-notifications:establish-subscription

   {
      "ietf-subscribed-notifications:input": {
         "stream": "NETCONF",
         "stream-xpath-filter":
           "/ietf-vrrp:vrrp-protocol-error-event[
             protocol-error-reason='checksum-error']/"
      }
   }

       Figure 16: Establishing a Subscription Error Reason via XPath

...

   POST /restconf/operations
        /ietf-subscribed-notifications:modify-subscription

   {
      "ietf-subscribed-notifications:input": {
         "stream": "NETCONF",
         "stream-subtree-filter": {
           "/ietf-vrrp:vrrp-protocol-error-event" : {}
         }
      }
   }
                Figure 17: Example "modify-subscription" RPC


Notes:

* There is a missing CRLF in both figures as per RFC9112:

--
  HTTP-message   = start-line CRLF
                   *( field-line CRLF )
                   CRLF
                   [ message-body ]
--

* The last item in the JSON of figure 16 includes a trailing "," while it shouldn't.
```

</details>

<br>**Explanation:**
The errata report points out missing CRLF in the HTTP messages and a trailing comma in the JSON of Figure 16, both of which are stylistic issues rather than errors that affect the implementation. The corrected figures include the CRLF and remove the trailing comma.

---

<details>
<summary><b>Errata 6753</b> from <b>RFC 8664</b> - Path Computation Element Communication Protocol (PCEP) Extensions for Segment Routing (December 2019)</summary>

```
Section 4.3.1 says:


If the F bit is set to zero
      (see below), then the NT field has no meaning and MUST be ignored
      by the receiver. 

It should say:

If the F bit is set to one
      (see below), then the NT field has no meaning and MUST be ignored
      by the receiver. 

Notes:

Later it says, when this F bit is set to 1, the NAI value is absent, so the NT field has no meaning. 
     F:   When this bit is set to 1, the NAI value in the subobject
           body is absent.  The F bit MUST be set to 1 if NT=0;
           otherwise, it MUST be set to zero.  The S and F bits MUST NOT
           both be set to 1.
```

</details>

<br>**Explanation:**
The original text incorrectly states that the NT field should be ignored when the F bit is zero. The correction clarifies that the NT field is ignored when the F bit is one, which is consistent with the later description of the F bit. This inconsistency would lead to incorrect interpretation and handling of the NT field.

---

<details>
<summary><b>Errata 6609</b> from <b>RFC 8684</b> - TCP Extensions for Multipath Operation with Multiple Addresses (March 2020)</summary>

```
Section B.3 says:


   initiator                                                    listener
       |                                                           |
       |    S  0(20) <MP_CAPABLE>, <TFO cookie>                    |
       | --------------------------------------------------------> |
       |                                                           |
       |    S. 0(0) ack 21 <MP_CAPABLE>                            |
       | <-------------------------------------------------------- |
       |                                                           |
       |    .  1(100) ack 21 <DSS ack=1 seq=1 ssn=1 dlen=100>      |
       | <-------------------------------------------------------- |
       |                                                           |
       |    .  21(0) ack 1 <MP_CAPABLE>                            |
       | --------------------------------------------------------> |
       |                                                           |
       |    .  21(20) ack 101 <DSS ack=101 seq=1 ssn=1 dlen=20>    |
       | --------------------------------------------------------> |
       |                                                           |

                    Figure 19: The Listener Supports TFO

It should say:

initiator                                                    listener
       |                                                           |
       |    S  0(20) <MP_CAPABLE>, <TFO cookie>                    |
       | --------------------------------------------------------> |
       |                                                           |
       |    S. 0(0) ack 21 <MP_CAPABLE>                            |
       | <-------------------------------------------------------- |
       |                                                           |
       |    .  1(100) ack 21 <DSS seq=1 ssn=1 dlen=100, M=1, A=0>  |
       | <-------------------------------------------------------- |
       |                                                           |
       |    .  21(0) ack 1 <MP_CAPABLE>                            |
       | --------------------------------------------------------> |
       |                                                           |
       |    .  21(20) ack 101 <DSS ack=101 seq=1 ssn=1 dlen=20>    |
       | --------------------------------------------------------> |
       |                                                           |

                    Figure 19: The Listener Supports TFO

Notes:

The example for TCP Fastopen with MPTCPv1 in RFC8684, Appendix-B.3 shows the listener sending an incorrect data-ack in its first data packet to the initiator sent immediately after its SYN-ACK.
At this point, the listener has not received the initiator's key, so it cannot generate the data-ack in it's response packets.
The correct behaviour would be to set flag 'A' to 0 and exclude sending data-ack until the initiator's key is received.
```

</details>

<br>**Explanation:**
The example in Figure 19 shows the listener sending a DSS packet with the ack field set to 1, which is incorrect because the initiator's key is not yet received. The correction sets the A flag to 0 and removes the data-ack until the key is received, resolving the inconsistency.

---

<details>
<summary><b>Errata 7334</b> from <b>RFC 8727</b> - JSON Binding of the Incident Object Description Exchange Format (August 2020)</summary>

```
Section 6 says:


          {iodef-BusinessImpact => BusinessImpact /


It should say:

          {iodef-BusinessImpact => BusinessImpact} /


Notes:

A closing brace is missing in this line of the rule for "Assessment".
```

</details>

<br>**Explanation:**
The original rule for "Assessment" is missing a closing brace, which makes it syntactically incorrect and impacts the processing of the JSON binding.  The correction adds the missing brace to ensure that the rule is correctly parsed.

---

<details>
<summary><b>Errata 7389</b> from <b>RFC 8824</b> - Static Context Header Compression (SCHC) for the Constrained Application Protocol (CoAP) (June 2021)</summary>

```
Section 3.1 says:


For example, the Uri-Path option is
mandatory in the request, and it might not be present in the
response.

It should say:

For example, the Uri-Path option can
be used in the request, while it is not used in the response.

Notes:

The Uri-Path option is not mandatory in a CoAP request, and it is not supposed to be used in a CoAP response.
```

</details>

<br>**Explanation:**
The original text incorrectly states that the Uri-Path option is mandatory in CoAP requests and implies it might be present in responses. The correction clarifies that Uri-Path is not mandatory in requests and is not used in responses, thus resolving the inconsistencies.

---

<details>
<summary><b>Errata 7132</b> from <b>RFC 8851</b> - RTP Payload Format Restrictions (January 2021)</summary>

```
Section 10 says:


rid-id            = 1*(alpha-numeric / "-" / "_")

It should say:

rid-id            = 1*255(alpha-numeric)

Notes:

The BNF should be consistent with the rules for the RtpStreamId/RepairedRtpStreamId SDES from RFC 8852 section 3:

"As with all SDES items, RtpStreamId and RepairedRtpStreamId are limited to a total of 255 octets in length. RtpStreamId and RepairedRtpStreamId are constrained to contain only alphanumeric characters. For avoidance of doubt, the only allowed byte values for these IDs are decimal 48 through 57, 65 through 90, and 97 through 122."
```

</details>

<br>**Explanation:**
The original ABNF for rid-id allows hyphens and underscores, which is inconsistent with RFC 8852's restriction to only alphanumeric characters. The correction limits rid-id to alphanumeric characters and restricts the maximum length to 255 octets, ensuring consistency with RFC 8852.

---

<details>
<summary><b>Errata 7386</b> from <b>RFC 8881</b> - Network File System (NFS) Version 4 Minor Version 1 Protocol (August 2020)</summary>

```
Section 18.46.3. says:


                                                             Operations
   other than SEQUENCE, BIND_CONN_TO_SESSION, EXCHANGE_ID,
   CREATE_SESSION, and DESTROY_SESSION, MUST NOT appear as the first
   operation in a COMPOUND.

It should say:

                                                             Operations
   other than SEQUENCE, BIND_CONN_TO_SESSION, EXCHANGE_ID,
   CREATE_SESSION, DESTROY_SESSION, and DESTROY_CLIENTID, MUST NOT
   appear as the first operation in a COMPOUND.

Notes:

Section 18.50.3. DESCRIPTION of DESTROY_CLIENTID says

"DESTROY_CLIENTID MAY be preceded with a SEQUENCE"

and also says

"If DESTROY_CLIENTID is not prefixed by SEQUENCE, it MUST be the only operation in the COMPOUND request"

which implies that DESTROY_CLIENTID can appear as the first (and the only) operation in a COMPOUND.
```

</details>

<br>**Explanation:**
The original text incorrectly restricts the first operation in a COMPOUND to exclude DESTROY_CLIENTID, while section 18.50.3 allows it as the first (and only) operation. This discrepancy creates an inconsistency between the general rule and the specific exception for DESTROY_CLIENTID.

---

<details>
<summary><b>Errata 8166</b> from <b>RFC 8888</b> - RTP Control Protocol (RTCP) Feedback for Congestion Control (January 2021)</summary>

```
Section 3.1 says:


         Following this, the report block contains a
   16-bit packet metric block for each RTP packet that has a sequence
   number in the range begin_seq to begin_seq+num_reports inclusive
   (calculated using arithmetic modulo 65536 to account for possible
   sequence number wrap-around).

It should say:

         Following this, the report block contains a
   16-bit packet metric block for each RTP packet that has a sequence
   number in the range begin_seq up to, but not including,
   begin_seq+num_reports
   (calculated using arithmetic modulo 65536 to account for possible
   sequence number wrap-around).

Notes:

The text can be read as the range being [begin_seq, begin_seq+num_reports].

If "begin_seq" is taken as the first sequence number you are reporting on, the original text means that you would have to have num_reports be 0 when you are reporting on a single packet. This seems very strange.

Alternatively, if "begin_seq" is taken as the sequence number before the one you are reporting on, the num_reports is consistent, but you are then reporting on the range <begin_seq, begin_seq+num_reports], which also seems strange.

The suggested clarification would report on the sequence [begin_seq, begin_seq + num_reports>, which seems like the most natural interpretation.

This is also consistent with the format of an empty report, which is explicit that begin_seq is the sequence number of the last RTP packet received.
```

</details>

<br>**Explanation:**
The meaning of num_reports intended later in the text contradicts with the fact that the range is inclusive.

---

<details>
<summary><b>Errata 6620</b> from <b>RFC 8910</b> - Captive-Portal Identification in DHCP and Router Advertisements (RAs) (September 2020)</summary>

```
Section 2 says:


   A captive portal MAY do content negotiation (Section 3.4 of
   [RFC7231]) and attempt to redirect clients querying without an
   explicit indication of support for the captive portal API content
   type (i.e., without application/capport+json listed explicitly
   anywhere within an Accept header field as described in Section 5.3 of
   [RFC7231]).  In so doing, the captive portal SHOULD redirect the
   client to the value associated with the "user-portal-url" API key.
   When performing such content negotiation (Section 3.4 of [RFC7231]),
   implementors of captive portals need to keep in mind that such
   responses might be cached, and therefore SHOULD include an
   appropriate Vary header field (Section 7.1.4 of [RFC7231]) or set the
   Cache-Control header field in any responses to "private" or a more
   restrictive value such as "no-store" (Section 5.2.2.3 of [RFC7234]).

It should say:

   A captive portal MAY do content negotiation (Section 3.4 of
   [RFC7231]) and attempt to redirect clients querying without an
   explicit indication of support for the captive portal API content
   type (i.e., without application/captive+json listed explicitly
   anywhere within an Accept header field as described in Section 5.3 of
   [RFC7231]).  In so doing, the captive portal SHOULD redirect the
   client to the value associated with the "user-portal-url" API key.
   When performing such content negotiation (Section 3.4 of [RFC7231]),
   implementors of captive portals need to keep in mind that such
   responses might be cached, and therefore SHOULD include an
   appropriate Vary header field (Section 7.1.4 of [RFC7231]) or set the
   Cache-Control header field in any responses to "private" or a more
   restrictive value such as "no-store" (Section 5.2.2.3 of [RFC7234]).

Notes:

In RFC8908 the relevant Content-Type is defined as "application/captive+json" and not "application/capport+json".
```

</details>

<br>**Explanation:**
The original text uses the incorrect content type "application/capport+json". The correction uses the correct content type, "application/captive+json", which is consistent with RFC 8908.

---

<details>
<summary><b>Errata 7654</b> from <b>RFC 8955</b> - Dissemination of Flow Specification Rules (December 2020)</summary>

```
Section 4 says:


   This NLRI information is encoded using MP_REACH_NLRI and
   MP_UNREACH_NLRI attributes, as defined in [RFC4760].  When
   advertising Flow Specifications, the Length of the Next-Hop Network
   Address MUST be set to 0.  The Network Address of the Next-Hop field
   MUST be ignored.


It should say:

   This NLRI information is encoded using MP_REACH_NLRI and
   MP_UNREACH_NLRI attributes, as defined in [RFC4760].  When
   advertising Flow Specifications, the "Length of Next Hop Network 
   Address" field MUST be set to 0.  The "Network Address of Next Hop" 
   field MUST be ignored.

Notes:

The fields are named incorrectly in the original text -- they don't match the field names they're referencing in RFC 4760. Most importantly there's no hyphen in the RFC 4760 field definitions, but there are other differences too.
```

</details>

<br>**Explanation:**
The original text uses incorrect field names for the Next Hop Network Address attributes.  The correction uses the correct field names from RFC 4760, resolving the inconsistency.  This inconsistency could lead to implementations incorrectly handling the Next Hop Network Address attributes when advertising Flow Specifications.

---

<details>
<summary><b>Errata 7571</b> from <b>RFC 8956</b> - Dissemination of Flow Specification Rules for IPv6 (December 2020)</summary>

```
Section 3.8.1 says:


+======+======================+=========================+==========+
| len  | destination          | source                  | ul-proto |
+======+======================+=========================+==========+
| 0x12 | 01 20 00 20 01 0d bb | 02 68 40 12 34 56 78 9a | 03 81 06 |
+------+----------------------+-------------------------+----------+
                                 Table 1

It should say:

+======+======================+=========================+==========+
| len  | destination          | source                  | ul-proto |
+======+======================+=========================+==========+
| 0x12 | 01 20 00 20 01 0d b8 | 02 68 40 12 34 56 78 9a | 03 81 06 |
+------+----------------------+-------------------------+----------+
                                 Table 1

Notes:

The last byte in the "destination" column of Table 1 in 3.8.1 should be "b8", not "bb".
```

</details>

<br>**Explanation:**
The example in Table 1 contains an incorrect byte value ("bb" instead of "b8") in the destination field, creating an inconsistency between the example and the correct representation.

---

<details>
<summary><b>Errata 8199</b> from <b>RFC 8972</b> - Simple Two-Way Active Measurement Protocol Optional Extensions (January 2021)</summary>

```
Section 4.4 says:


Also, the Session-Reflector MUST copy the value of the DSCP and ECN
fields of the IP header of the received STAMP test packet into the
DSCP2 field in the reflected test packet.

It should say:

Also, the Session-Reflector MUST copy the value of the DSCP and ECN
fields of the IP header of the received STAMP test packet into the
DSCP2 and ECN fields, respectively, in the reflected test packet.

Notes:

First, thank you to all the IETF contributors who do such amazing work to keep the Internet going (seriously!). I noticed this minor omission while implementing the specification. I spoke with Mr. Mirsky (one of the authors) who suggested I file this report. Of course, the authors' intent is not in doubt, but he suggested that I submit this report nonetheless. Besides this very minor misstatement, as someone writing an implementation who was completely uninvolved in drafting the RFC, I have found this document to be incredibly readable and easy to follow -- thank you!

[Edit: WK (Ops AD): Thanks for the Errata (and the kind note) ].
```

</details>

<br>**Explanation:**
The original text only copies the DSCP and ECN fields into the DSCP2 field, while it should copy the DSCP and ECN fields into the DSCP2 and ECN fields, respectively. This inconsistency needs to be corrected to ensure that implementations correctly reflect the DSCP and ECN values.

---

<details>
<summary><b>Errata 6873</b> from <b>RFC 8984</b> - JSCalendar: A JSON Representation of Calendar Data (July 2021)</summary>

```
Section 4.3.2. says:


Identifies the time zone of the main JSCalendar object, of which this
JSCalendar object is a recurrence instance.  This property MUST be
set if the "recurrenceId" property is set.  It MUST NOT be set if the
"recurrenceId" property is not set.

It should say:

Identifies the time zone of the main JSCalendar object, of which this
JSCalendar object is a recurrence instance.  It MUST NOT be set if the
"recurrenceId" property is not set.

Notes:

A recurrence instance may be in floating time, in which case the value of the "recurrenceIdTimeZone" property is null. As null is the default value of the "recurrenceIdTimeZone" property, it is NOT required to be set if "recurrenceId" is set.
```

</details>

<br>**Explanation:**
The original description creates ambiguity by requiring the "recurrenceIdTimeZone" property to be set when "recurrenceId" is set, while it could be null, which is the default value.  The correction removes the requirement, making the specification clearer.

---

<details>
<summary><b>Errata 6809</b> from <b>RFC 8986</b> - Segment Routing over IPv6 (SRv6) Network Programming (February 2021)</summary>

```
Section 4.10 says:


When N receives a packet whose IPv6 DA is S and S is a local End.DX2
SID

It should say:

When N receives a packet whose IPv6 DA is S and S is a local End.DX2V
SID


Notes:

Looks like a typo in the original text
```

</details>

<br>**Explanation:**
The original text uses the incorrect SID type (End.DX2) when referring to a local End.DX2V SID. This inconsistency misidentifies the relevant SID type and may lead to incorrect processing of packets with such SIDs.

---

<details>
<summary><b>Errata 6716</b> from <b>RFC 8995</b> - Bootstrapping Remote Secure Key Infrastructure (BRSKI) (May 2021)</summary>

```
Section 5.8.3 says:


A registrar MAY be configured to ignore (i.e., override
the above policy) the history of the device, but it is RECOMMENDED
that this only be configured if hardware-assisted (i.e., Transport
Performance Metrics (TPM) anchored) Network Endpoint Assessment (NEA)
[RFC5209] is supported.

It should say:

A registrar MAY be configured to ignore (i.e., override
the above policy) the history of the device, but it is RECOMMENDED
that this only be configured if hardware-assisted (i.e., Trusted 
Platform Module (TPM) anchored) Network Endpoint Assessment (NEA)
 [RFC5209] is supported.

Notes:

The logical expansion of 'TPM' in this parenthetical example is the Trusted Platform Module.
```

</details>

<br>**Explanation:**
The logical expansion of 'TPM' in this parenthetical example is the Trusted Platform Module.

---

<details>
<summary><b>Errata 7576</b> from <b>RFC 8995</b> - Bootstrapping Remote Secure Key Infrastructure (BRSKI) (May 2021)</summary>

```
Section 4.3 says:


   objective-value = text       ; name of the (list of) supported
                                ; protocols: "EST-TLS" for RFC 7030.


It should say:

   objective-value = text       ; name of the supported protocol,
                                ; e.g., "EST-TLS" for RFC 7030.


Notes:

This objective does not support a list of supported protocols. 
The comment in the example might lead people to conclude they can do that.
```

</details>

<br>**Explanation:**
The original description allows for multiple protocols, while the intended functionality supports only a single protocol. The ambiguity stems from the use of "(list of)" in the description, leading to multiple interpretations of the objective-value.

---

<details>
<summary><b>Errata 7539</b> from <b>RFC 9002</b> - QUIC Loss Detection and Congestion Control (May 2021)</summary>

```
Section 5. says:


smoothed_rtt = 7/8 * smoothed_rtt + 1/8 * adjusted_rtt
rttvar_sample = abs(smoothed_rtt - adjusted_rtt)
rttvar = 3/4 * rttvar + 1/4 * rttvar_sample


It should say:

rttvar_sample = abs(smoothed_rtt - adjusted_rtt)
rttvar = 3/4 * rttvar + 1/4 * rttvar_sample
smoothed_rtt = 7/8 * smoothed_rtt + 1/8 * adjusted_rtt


Notes:

Per Appendix A.7 of this RFC and Section 2 of the referred RFC 6298,
rttvar should be computed before updating smoothed_rtt itself.
```

</details>

<br>**Explanation:**
The original order of calculations for smoothed_rtt and rttvar is incorrect. The correction places the calculation of rttvar before the update of smoothed_rtt, which is consistent with RFC 6298. This inconsistency would result in incorrect RTT and RTT variance calculations.

---

<details>
<summary><b>Errata 7543</b> from <b>RFC 9008</b> - Using RPI Option Type, Routing Header for Source Routes, and IPv6-in-IPv6 Encapsulation in the RPL Data Plane (April 2021)</summary>

```
Section 6 says:


As the Rank information in the RPI artifact is changed at each hop, it
will typically be zero when it arrives at the DODAG root.

It should say:

As the Rank information in the RPI artifact is changed at each hop, it
will typically be non-zero when it arrives at the DODAG root.

Notes:

The SenderRank is 0 if: 
- The packet comes from Internet (and has an RPI)
- The packet has not been forwarded (ie. if the source is a direct child of the DODAG root), as RFC 6550 section 11.2 tells to set SenderRank to 0 at the source.

The typical case is rather a packet that arrives at the DODAG root from a child node forwarding a packet, in which case SenderRank is set to DAGRank(rank) > 0.
```

</details>

<br>**Explanation:**
The original text incorrectly states that the Rank information in the RPI artifact will typically be zero when it arrives at the DODAG root. The correction clarifies that it will typically be non-zero, which is the more accurate and common case. This inconsistency could lead to misinterpretations of the RPI artifact.

---

<details>
<summary><b>Errata 7323</b> from <b>RFC 9051</b> - Internet Message Access Protocol (IMAP) - Version 4rev2 (August 2021)</summary>

```
Section 6.4.4.4. says:


        S: B283 NO [BADCHARSET UTF-8] KOI8-R is not supported


It should say:

        S: B283 NO [BADCHARSET (KOI8-R)] KOI8-R is not supported


Notes:

The BADCHARSET response code is described in 7.1 as "Optionally followed by a parenthesized list of charsets", and in the formal syntax as:

   resp-text-code =/ "BADCHARSET" [SP "(" charset *(SP charset) ")" ]

Although a client's parser might use a generic resp-text-code (atom [SP 1*<any TEXT-CHAR except "]">]) as a fallback, the server should parenthesize even when only one charset is sent.
```

</details>

<br>**Explanation:**
The original BADCHARSET response code is missing the required parentheses around the charset. The correction adds the parentheses, making the response consistent with the specification.

---

<details>
<summary><b>Errata 6829</b> from <b>RFC 9073</b> - Event Publishing Extensions to iCalendar (August 2021)</summary>

```
Section 7.1 says:


      partprop     = *(
                     ;
                     ; The following are REQUIRED
                     ; but MUST NOT occur more than once.
                     ;
                     participanttype / uid /
                     ;
                     ; The following are OPTIONAL
                     ; but MUST NOT occur more than once.
                     ;
                     calendaraddress / created / description / dtstamp /
                     geo / last-mod / priority / seq /
                     status / summary / url /
                     ;
                     ; The following are OPTIONAL
                     ; and MAY occur more than once.
                     ;
                     attach / categories / comment
                     contact / location / rstatus / related /
                     resources / strucloc / strucres /
                     styleddescription / sdataprop / iana-prop
                     ;
                     )


It should say:

      partprop     = *(
                     ;
                     ; The following are REQUIRED
                     ; but MUST NOT occur more than once.
                     ;
                     participanttype / uid /
                     ;
                     ; The following are OPTIONAL
                     ; but MUST NOT occur more than once.
                     ;
                     calendaraddress / created / description / dtstamp /
                     geo / last-mod / priority / seq /
                     status / summary / url /
                     ;
                     ; The following are OPTIONAL
                     ; and MAY occur more than once.
                     ;
                     attach / categories / comment
                     contact / location / rstatus / related /
                     resources /
                     styleddescription / sdataprop / iana-prop
                     ;
                     )


Notes:

'structloc' and 'structres' are not defined in this document.  These are leftover artifacts from a draft version of this specification and were replaced by 'locationc' and 'resourcec'
```

</details>

<br>**Explanation:**
The original specification includes properties ("strucloc" and "structres") that are not defined in the document.  The removal of these undefined properties resolves the inconsistency.

---

<details>
<summary><b>Errata 7381</b> from <b>RFC 9073</b> - Event Publishing Extensions to iCalendar (August 2021)</summary>

```
Section 7.2 says:


   Format Definition:  This component is defined by the following
      notation:

      locationc    = "BEGIN" ":" "VLOCATION" CRLF
                     locprop
                     "END" ":" "VLOCATION" CRLF

      locprop      = *(
                     ;
                     ; The following are REQUIRED
                     ; but MUST NOT occur more than once.
                     ;
                     uid /
                     ;
                     ; The following are OPTIONAL
                     ; but MUST NOT occur more than once.
                     ;
                     description / geo / loctype / name
                     ;
                     ; The following are OPTIONAL
                     ; and MAY occur more than once.
                     ;
                     sdataprop / iana-prop
                  )

It should say:

   Format Definition:  This component is defined by the following
      notation:

      locationc    = "BEGIN" ":" "VLOCATION" CRLF
                     locprop
                     "END" ":" "VLOCATION" CRLF

      locprop      = *(
                     ;
                     ; The following are REQUIRED
                     ; but MUST NOT occur more than once.
                     ;
                     uid /
                     ;
                     ; The following are OPTIONAL
                     ; but MUST NOT occur more than once.
                     ;
                     description / geo / loctype / name / url /
                     ;
                     ; The following are OPTIONAL
                     ; and MAY occur more than once.
                     ;
                     sdataprop / iana-prop
                  )

Notes:

The url property is missing or the specification clahes with RFC 9074, where in section 8.2 in the example it reads:

   BEGIN:VLOCATION
   UID:123456-abcdef-98765432
   NAME:Office
   URL:geo:40.443,-79.945;u=10
   END:VLOCATION

Either "geo" was intended as a geo uri as defined in RFC 5870 (instead of the geographic position from RFC 2445/5545) or "url" should be added as a valid property (or RFC 9074 is wrong).

--

Verifier's notes: A "/" was missing after "name" and was added after "url" in this same errata.
```

</details>

<br>**Explanation:**
The original specification omits the "url" property from the list of allowed properties in the "locprop" definition, which is inconsistent with the example provided in RFC 9074 and the general allowance for URL properties in iCalendar.

---

<details>
<summary><b>Errata 7094</b> from <b>RFC 9083 part of STD 95</b> - JSON Responses for the Registration Data Access Protocol (RDAP) (June 2021)</summary>

```
Section 2.1 says:


If The Registry of the Moon desires to express information not found
in this specification, it might select "lunarNIC" as its identifying
prefix and insert, as an example, the member named
"lunarNIC_beforeOneSmallStep" to signify registrations occurring
before the first moon landing and the member named
"lunarNIC_harshMistressNotes" that contains other descriptive text.

Consider the following JSON response with JSON names, some of which
should be ignored by clients without knowledge of their meaning.

{
  "handle" : "ABC123",
  "lunarNIC_beforeOneSmallStep" : "TRUE THAT!",
  "remarks" :
  [
    {
      "description" :
      [
        "She sells sea shells down by the sea shore.",
        "Originally written by Terry Sullivan."
      ]
    }
  ],
  "lunarNIC_harshMistressNotes" :
  [
    "In space,",
    "nobody can hear you scream."
  ]
}
Figure 2

It should say:

If The Registry of the Moon desires to express information not found
in this specification, it might select "lunarNIC_level_0" as its
identifying prefix and insert, as an example, the member named
"lunarNIC_level_0_beforeOneSmallStep" to signify registrations occurring
before the first moon landing and the member named
"lunarNIC_level_0_harshMistressNotes" that contains other descriptive
text.

Consider the following JSON response with JSON names, some of which
should be ignored by clients without knowledge of their meaning.

{
  "handle" : "ABC123",
  "lunarNIC_level_0_beforeOneSmallStep" : "TRUE THAT!",
  "remarks" :
  [
    {
      "description" :
      [
        "She sells sea shells down by the sea shore.",
        "Originally written by Terry Sullivan."
      ]
    }
  ],
  "lunarNIC_level_0_harshMistressNotes" :
  [
    "In space,",
    "nobody can hear you scream."
  ]
}
Figure 2

Notes:

The original text uses the string identifier "lunarNIC" as the prefix for an example extension. This is inconsistent with the example given in Section 4.1, where "lunarNIC_level_0" is used as an example of a registered identifier for an RDAP extension. This inconsistency can lead implementers to believe that the registered identifier and the extension prefix can be inconsistent, when the intent of the specification is that they should be consistent. This inconsistency can cause significant misunderstanding of the technical specification and might result in faulty implementations if not corrected. Changing the examples in Section 2.1 aligns the text with the example in Section 4.1, demonstrating that the extension prefix and the registered identifier should be one and the same.
```

</details>

<br>**Explanation:**
The original example uses the string identifier "lunarNIC" as the prefix for an extension, which is inconsistent with the example in Section 4.1, where "lunarNIC_level_0" is used.  The correction uses the consistent prefix, ensuring that examples accurately reflect the intended use of extension prefixes.

---

<details>
<summary><b>Errata 7986</b> from <b>RFC 9083 part of STD 95</b> - JSON Responses for the Registration Data Access Protocol (RDAP) (June 2021)</summary>

```
Section 9 says:


The following is an elided example of an entity truncated data.

{
  "objectClassName" : "entity",
  "handle" : "ANENTITY",
  "roles" : [ "registrant" ],
  ...
  "entities" :
  [
    {
      "objectClassName" : "entity",
      "handle": "ANEMBEDDEDENTITY",
      "roles" : [ "technical" ],
      ...
    },
    ...
  ],
  "networks" :
  [
    ...
  ],
  ...
  "remarks" :
  [
    {
      "title" : "Data Policy",
      "type" : "object truncated due to unexplainable reason",
      "description" :
      [
        "Some of the data in this object has been removed."
      ],
      "links" :
      [
        {
          "value" : "https://example.net/help",
          "rel" : "alternate",
          "type" : "text/html",
          "href" : "https://www.example.com/data_policy.html"
        }
      ]
    }
  ]
}


It should say:

The following is an elided example of an entity truncated data.

{
  "rdapConformance" :
  [
    "rdap_level_0"
  ],
  "objectClassName" : "entity",
  "handle" : "ANENTITY",
  "roles" : [ "registrant" ],
  ...
  "entities" :
  [
    {
      "objectClassName" : "entity",
      "handle": "ANEMBEDDEDENTITY",
      "roles" : [ "technical" ],
      ...
    },
    ...
  ],
  "networks" :
  [
    ...
  ],
  ...
  "remarks" :
  [
    {
      "title" : "Data Policy",
      "type" : "object truncated due to unexplainable reason",
      "description" :
      [
        "Some of the data in this object has been removed."
      ],
      "links" :
      [
        {
          "value" : "https://example.net/help",
          "rel" : "alternate",
          "type" : "text/html",
          "href" : "https://www.example.com/data_policy.html"
        }
      ]
    }
  ]
}


Notes:

RFC 9083 4.1 states that the rdapConformance data structure MUST appear in the topmost JSON object of RDAP responses. The example error response provided in Figure 33 should include the rdapConformance property but does not.
```

</details>

<br>**Explanation:**
The example JSON response in Section 9 omits the required "rdapConformance" property as specified in Section 4.1, creating an inconsistency between the example and the specification.

---

<details>
<summary><b>Errata 7736</b> from <b>RFC 9085</b> - Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing (August 2021)</summary>

```
Section 2.3.5 says:


   A Prefix NLRI, that has been advertised with a Range TLV, is
   considered a normal routing prefix (i.e., prefix reachability) only
   when there is also an IGP metric TLV (TLV 1095) associated it.
   Otherwise, it is considered only as the first prefix in the range for
   prefix-to-SID mapping advertisement.

It should say:

   A Prefix NLRI, that has been advertised with a Range TLV, is
   considered a normal routing prefix (i.e., prefix reachability) only
   when there is also a Prefix Metric TLV (TLV 1155) associated with it.
   Otherwise, it is considered only as the first prefix in the range for
   prefix-to-SID mapping advertisement.

Notes:

The current text is referring to the wrong BGP-LS TLV. Since the Range TLV is associated with a Prefix NLRI, the "Prefix Metric TLV (TLV 1155)" should be referenced here since the "IGP metric TLV (TLV 1095)" is associated with a Link NLRI.

Verifier note: in addition to the fix proposed by Ketan, I added a preposition: "associated with it", and corrected an indefinite article: "a Prefix".
```

</details>

<br>**Explanation:**
The original text refers to the incorrect TLV (IGP metric TLV, TLV 1095) for Prefix NLRIs. The correction uses the correct TLV (Prefix Metric TLV, TLV 1155), which is consistent with the specification.  This inconsistency could affect implementations that rely on the correct TLV to identify normal routing prefixes.

---

<details>
<summary><b>Errata 7734</b> from <b>RFC 9085</b> - Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing (August 2021)</summary>

```
Section 2.3.5 says:


11 or 12 octets depending on the label or index encoding of the SID.

It should say:

15 or 16 octets depending on the label or index encoding of the SID.

Notes:

Length of the TLV does not account for the Prefix-SID Sub-TLVs type and length fields: 2 octets each = 4 octets in total.
This is valid for all variants: IS-IS, OSPFv2 and OSPFv3.

Note: see also https://mailarchive.ietf.org/arch/msg/idr/G_3KN-XXqyXbSXO1doiNJbK_gIA/
```

</details>

<br>**Explanation:**
The original text incorrectly calculates the length of the TLV, omitting the type and length fields of the Prefix-SID Sub-TLVs. The correction adds these four octets to the length calculation, making it consistent with the actual TLV size.

---

<details>
<summary><b>Errata 7336</b> from <b>RFC 9115</b> - An Automatic Certificate Management Environment (ACME) Profile for Generating Delegated Certificates (September 2021)</summary>

```
Section Appendix A says:


   oid = text .regexp "([0-2])((\.0)|(\.[1-9][0-9]*))*"


It should say:

   oid = text .regexp "([0-2])((\\.0)|(\\.[1-9][0-9]*))*"


Notes:

Backslashes need to be doubled in CDDL strings (as they are done in Appendix B).

An alternative fix would be to replace \\. by [.]

Note that the equivalent fix is not required for

   regtext = text .regexp "([^\*].*)|([\*][^\*].*)|([\*][\*].+)"

as the fact that the single backslashes have no effect is irrelevant here — the backslashes are not needed in the character classes [...].
As an editorial enhancement, the backslashes could be entirely removed from this line.
```

</details>

<br>**Explanation:**
The original regular expression for the oid parameter incorrectly uses single backslashes instead of double backslashes to escape the period character in the CDDL string.  The correction uses double backslashes to properly escape the period, making the regular expression consistent with the CDDL syntax.

---

<details>
<summary><b>Errata 7058</b> from <b>RFC 9132</b> - Distributed Denial-of-Service Open Threat Signaling (DOTS) Signal Channel Specification (September 2021)</summary>

```
Section 5.3 says:


              uses data-channel:target {
                when "/dots-signal/scope/conflict-information/"
                   + "conflict-cause = 'overlapping-targets'";
              }


It should say:

              uses data-channel:target {
                when "../conflict-cause = 'overlapping-targets'";
              }


Notes:

The original YANG statements make the "uses" statement apply to all "list scope" instances as soon as there is at least one "scope" instance that has "conflict-cause" set to "overlapping-targets". I suspect this is not the author's intent.

The corrected YANG statements make the "uses" statement only apply to the specific "scope" instances that have "conflict-cause" set to "overlapping-targets". There are also other ways to fix this issue.
```

</details>

<br>**Explanation:**
The original YANG uses statement applies the augmentation to all list scope instances when it should only apply to instances where conflict-cause is 'overlapping-targets'.  This creates an inconsistency between the intended behavior and the actual effect of the YANG statement.

---

<details>
<summary><b>Errata 7683</b> from <b>RFC 9135</b> - Integrated Routing and Bridging in Ethernet VPN (EVPN) (October 2021)</summary>

```
Section 4.2. says:


  2.  However, if PE2 is configured for asymmetric IRB mode, PE2 will
       advertise TS4 MAC/IP information in a MAC/IP Advertisement route
       with a zero Label2 field and no Route Target identifying IP-VRF1.
       In this case, PE2 will install TS4 information in its ARP table
       and BT1.  When a packet from TS2 to TS4 arrives at PE1, a longest
       prefix match on IP-VRF1's route table will yield the local IRB
       interface to BT1, where a subsequent ARP and bridge table lookup
       will provide the information for an asymmetric forwarding mode to
       PE2.

It should say:

  2.  However, if PE2 is configured for asymmetric IRB mode, PE2 will
       advertise TS4 MAC/IP information in a MAC/IP Advertisement route
       with a zero Label2 field and no Route Target identifying IP-VRF1.
       In this case, PE1 will install TS4 information in its ARP table
       and BT1.  When a packet from TS2 to TS4 arrives at PE1, a longest
       prefix match on IP-VRF1's route table will yield the local IRB
       interface to BT1, where a subsequent ARP and bridge table lookup
       will provide the information for an asymmetric forwarding mode to
       PE2.

Notes:

PE1 will use ARP table for forwarding traffic to PE2 - seems like typo
```

</details>

<br>**Explanation:**
The original text incorrectly states that PE2 installs TS4 information in its ARP table, while the correct behavior is for PE1 to install this information. This inconsistency could lead to implementations incorrectly handling asymmetric IRB forwarding.

---

<details>
<summary><b>Errata 7684</b> from <b>RFC 9135</b> - Integrated Routing and Bridging in Ethernet VPN (EVPN) (October 2021)</summary>

```
Section 6.1 says:


 This route is advertised along with the following extended community:

   *  Tunnel Type Extended Community

It should say:

 This route is advertised along with the following extended community:

   *  Encapsulation Extended Community

Notes:

I guess that solud be Encapsulation Extended Community (or  maybe Tunnel Encapsulation Attribute)

Verifier notes:
See https://mailarchive.ietf.org/arch/msg/bess/TgQR3NHd6wgcYow0B76i7ToBmr0/
```

</details>

<br>**Explanation:**
The original text uses the term "Tunnel Type Extended Community", which is not the correct term for the extended community used in this context. The correction uses the term "Encapsulation Extended Community", which is the correct term and is consistent with the specification.

---

<details>
<summary><b>Errata 7799</b> from <b>RFC 9142</b> - Key Exchange (KEX) Method Updates and Recommendations for Secure Shell (SSH) (January 2022)</summary>

```
Section 1.2.1 says:


+============+=============================+
| Curve Name | Estimated Security Strength |
+============+=============================+
| nistp256   | 128 bits                    |
+------------+-----------------------------+
| nistp384   | 192 bits                    |
+------------+-----------------------------+
| nistp521   | 512 bits                    |
+------------+-----------------------------+
| curve25519 | 128 bits                    |
+------------+-----------------------------+
| curve448   | 224 bits                    |
+------------+-----------------------------+

It should say:

+============+=============================+
| Curve Name | Estimated Security Strength |
+============+=============================+
| nistp256   | 128 bits                    |
+------------+-----------------------------+
| nistp384   | 192 bits                    |
+------------+-----------------------------+
| nistp521   | 256 bits                    |
+------------+-----------------------------+
| curve25519 | 128 bits                    |
+------------+-----------------------------+
| curve448   | 224 bits                    |
+------------+-----------------------------+

Notes:

P-521 has approximately 256 bits of security (rather than 512), as per Table 1 of Section 6.1.1 of FIPS 186-5, and Section 9 Paragraph 5 of RFC 5656.
```

</details>

<br>**Explanation:**
The estimated security strength for nistp521 is incorrectly listed as 512 bits. The correct value is 256 bits, creating an inconsistency with other references that specify the correct security strength.

---

<details>
<summary><b>Errata 7176</b> from <b>RFC 9167</b> - Registry Maintenance Notification for the Extensible Provisioning Protocol (EPP) (December 2021)</summary>

```
Section 5.1 says:


xmlns="https://www.w3.org/2001/XMLSchema"

It should say:

xmlns="http://www.w3.org/2001/XMLSchema"

Notes:

XML Schema standard https://www.w3.org/TR/xmlschema-1/ "The XML representation of schema components uses a vocabulary identified by the namespace name http://www.w3.org/2001/XMLSchema. "
```

</details>

<br>**Explanation:**
The namespace URI for XML Schema is incorrectly specified as "https://www.w3.org/2001/XMLSchema"; the correct URI is "http://www.w3.org/2001/XMLSchema", creating an inconsistency with the XML Schema standard.

---

<details>
<summary><b>Errata 7134</b> from <b>RFC 9252</b> - BGP Overlay Services Based on Segment Routing over IPv6 (SRv6) (July 2022)</summary>

```
Section 6.4 says:


                  +---------------------------------------+
                  |  RD (8 octets)                        |
                  +---------------------------------------+
                  |  Ethernet Tag ID (4 octets)           |
                  +---------------------------------------+
                  |  IP Address Length (1 octet)          |
                  +---------------------------------------+
                  |  Originating Router's IP Address      |
                  |          (4 or 16 octets)             |
                  +---------------------------------------+

                        Figure 10: EVPN Route Type 4


It should say:

                  +---------------------------------------+
                  |  RD (8 octets)                        |
                  +---------------------------------------+
                  |Ethernet Segment Identifier (10 octets)|
                  +---------------------------------------+
                  |  IP Address Length (1 octet)          |
                  +---------------------------------------+
                  |  Originating Router's IP Address      |
                  |          (4 or 16 octets)             |
                  +---------------------------------------+

                        Figure 10: EVPN Route Type 4


Notes:

The 2nd field in the figure should be "Ethernet Segment Identifier" of size 10 octets instead of the "Ethernet Tag ID" of size 4 octets.

RFC7432 is the EVPN specification for Ethernet Segment Route (Type 4) and hence the format in section 7.4 of RFC7432 is the correct one.
RFC9252 has an error when showing the encoding format of this EVPN Route Type 4 as a reminder in Figure 10 in section 6.4. 

This is an editorial error.
```

</details>

<br>**Explanation:**
The original figure uses the incorrect field name and size for the Ethernet Tag ID field, which should be the Ethernet Segment Identifier with 10 octets. This inconsistency should be corrected to reflect the correct encoding of EVPN Route Type 4.

---

<details>
<summary><b>Errata 7817</b> from <b>RFC 9252</b> - BGP Overlay Services Based on Segment Routing over IPv6 (SRv6) (July 2022)</summary>

```
Section 3.2.1 says:


   As defined in [RFC8986], the sum of the Locator Block Length (LBL),
   Locator Node Length (LNL), Function Length (FL), and Argument Length
   (AL) fields MUST be less than or equal to 128 and greater than the
   sum of Transposition Offset and Transposition Length.

It should say:

   As defined in [RFC8986], the sum of the Locator Block Length (LBL),
   Locator Node Length (LNL), Function Length (FL), and Argument Length
   (AL) fields MUST be less than or equal to 128 and greater than or
   equal to the sum of Transposition Offset and Transposition Length.

Notes:

The sum of Trans Off and Trans Length can be equal to the LBL+LNL+FL+AL when the last part of the SID (function or argument) is getting transposed.

This is clear also from the example below in the next paragraph of the same section:

   As an example, consider that the sum of the Locator Block and the
   Locator Node parts is 64.  For an SRv6 SID where the entire Function
   part of size 16 bits is transposed, the transposition offset is set
   to 64 and the transposition length is set to 16.  While for an SRv6
   SID for which the FL is 24 bits and only the lower order 20 bits are
   transposed (e.g., due to the limit of the MPLS Label field size), the
   transposition offset is set to 68 and the transposition length is set
   to 20.
```

</details>

<br>**Explanation:**
The original text incorrectly requires that the sum of LBL, LNL, FL, and AL be strictly greater than the sum of Transposition Offset and Transposition Length. The correction changes this to greater than or equal to, which is consistent with the example provided and the possible scenarios where the last part of the SID is transposed.

---

<details>
<summary><b>Errata 7148</b> from <b>RFC 9260</b> - Stream Control Transmission Protocol (June 2022)</summary>

```
Section 3.3.3 says:


A receiver of an INIT ACK chunk with the a_rwnd value set to a
value smaller than 1500 MUST discard the packet, SHOULD send a
packet in response containing an ABORT chunk and using the
Initiate Tag as the Verification Tag, and MUST NOT change the
state of any existing association.


It should say:

If an endpoint in the COOKIE-WAIT state receives an INIT ACK chunk
with the a_rwnd value set to a value smaller than 1500, it MUST
destroy the TCB and SHOULD send an ABORT chunk.  If such an
INIT ACK chunk is received in any state other than CLOSED or
COOKIE-WAIT, it SHOULD be discarded silently (see Section 5.2.3).


Notes:

The handling of a_rwnd < 1500 should be similar to the handling of OS = 0 or MIS = 0.
```

</details>

<br>**Explanation:**
The original specification for handling an INIT ACK chunk with a_rwnd less than 1500 is inconsistent with the handling of other error conditions.  The correction aligns the handling with other error conditions, ensuring consistent behavior across different scenarios.

---

<details>
<summary><b>Errata 7387</b> from <b>RFC 9260</b> - Stream Control Transmission Protocol (June 2022)</summary>

```
Section 5.2.4.1 says:


   Endpoint A                                          Endpoint Z
   <-------------- Association is established---------------------->
   Tag=Tag_A                                             Tag=Tag_Z
   <--------------------------------------------------------------->
   {A crashes and restarts}
   {app sets up an association with Z}
   (build TCB)
   INIT [I-Tag=Tag_A'
         & other info]  --------\
   (Start T1-init timer)         \
   (Enter COOKIE-WAIT state)      \---> (find an existing TCB,
                                         populate TieTags if needed,
                                         compose Cookie_Z with Tie-Tags
                                         and other info)
                                   /--- INIT ACK [Veri Tag=Tag_A',
                                  /               I-Tag=Tag_Z',
   (Cancel T1-init timer) <------/                Cookie_Z]
                                        (leave original TCB in place)
   COOKIE ECHO [Veri=Tag_Z',
                Cookie_Z]-------\
   (Start T1-init timer)         \
   (Enter COOKIE-ECHOED state)    \---> (Find existing association,
                                         Tie-Tags in Cookie_Z match
                                         Tie-Tags in TCB,
                                         Tags do not match, i.e.,
                                         case X X M M above,
                                         Announce Restart to ULP
                                         and reset association).
                                  /---- COOKIE ACK
   (Cancel T1-init timer, <------/
    Enter ESTABLISHED state)
   {app sends 1st user data; strm 0}
   DATA [TSN=Initial TSN_A
       Strm=0,Seq=0 & user data]--\
   (Start T3-rtx timer)            \
                                    \->
                                 /--- SACK [TSN Ack=init TSN_A,Block=0]
   (Cancel T3-rtx timer) <------/


It should say:

   Endpoint A                                          Endpoint Z
   <-------------- Association is established---------------------->
   Tag=Tag_A                                             Tag=Tag_Z
   <--------------------------------------------------------------->
   {A crashes and restarts}
   {app sets up an association with Z}
   (build TCB)
   INIT [I-Tag=Tag_A'
         & other info]  --------\
   (Start T1-init timer)         \
   (Enter COOKIE-WAIT state)      \---> (find an existing TCB,
                                         populate TieTags if needed,
                                         compose Cookie_Z with Tie-Tags
                                         and other info)
                                   /--- INIT ACK [Veri Tag=Tag_A',
                                  /               I-Tag=Tag_Z',
   (Cancel T1-init timer) <------/                Cookie_Z]
                                        (leave original TCB in place)
   COOKIE ECHO [Veri=Tag_Z',
                Cookie_Z]-------\
   (Start T1-cookie timer)       \
   (Enter COOKIE-ECHOED state)    \---> (Find existing association,
                                         Tie-Tags in Cookie_Z match
                                         Tie-Tags in TCB,
                                         Tags do not match, i.e.,
                                         case X X M M above,
                                         Announce Restart to ULP
                                         and reset association).
                                  /---- COOKIE ACK
   (Cancel T1-cookie timer, <----/
    Enter ESTABLISHED state)
   {app sends 1st user data; strm 0}
   DATA [TSN=Initial TSN_A
       Strm=0,Seq=0 & user data]--\
   (Start T3-rtx timer)            \
                                    \->
                                 /--- SACK [TSN Ack=init TSN_A,Block=0]
   (Cancel T3-rtx timer) <------/


Notes:

A packet containing an COOKIE-ECHO chunk is protected against loss by the T1-cookie timer, not the T1-init timer.
```

</details>

<br>**Explanation:**
The original diagram uses the T1-init timer for COOKIE-ECHO packets, while the T1-cookie timer is the correct timer. This inconsistency needs to be corrected to reflect the intended behavior.

---

<details>
<summary><b>Errata 7118</b> from <b>RFC 9286</b> - Manifests for the Resource Public Key Infrastructure (RPKI) (June 2022)</summary>

```
Section Appendix A says:


fileList           SEQUENCE SIZE (0..MAX) OF FileAndHash

It should say:

fileList           SEQUENCE SIZE (1..MAX) OF FileAndHash

Notes:

Section 7 specifies " A CA's manifest will always contain at least one entry"; therefor, a fileList sequence of size 0 is invalid.
```

</details>

<br>**Explanation:**
The original definition allows for a fileList with zero entries, contradicting Section 7, which states that a manifest will always have at least one entry. The correction sets the minimum size to 1, resolving the inconsistency.

---

<details>
<summary><b>Errata 7423</b> from <b>RFC 9303</b> - Locator/ID Separation Protocol Security (LISP-SEC) (October 2022)</summary>

```
Section 6.9 says:


ITR MUST set the 'EID HMAC ID' field to 0 before computing the HMAC.

It should say:

ITR MUST set the 'EID HMAC' field to 0 before computing the HMAC.

Notes:

0 (zero) must be set in the 'EID HMAC' field, not in the 'EID HMAC ID' field
```

</details>

<br>**Explanation:**
The original text refers to the incorrect field ('EID HMAC ID'). The correction uses the correct field name ('EID HMAC'), resolving the inconsistency. This inconsistency would affect implementations computing the HMAC.

---

<details>
<summary><b>Errata 7822</b> from <b>RFC 9480</b> - Certificate Management Protocol (CMP) Updates (November 2023)</summary>

```
Section A.2 says:


PKIHeader ::= SEQUENCE {
       pvno                INTEGER     { cmp1999(1), cmp2000(2),
                                         cmp2012(3) },

It should say:

PKIHeader ::= SEQUENCE {
       pvno                INTEGER     { cmp1999(1), cmp2000(2),
                                         cmp2021(3) },

Notes:

There is a typo in the ASN.1 module regarding the cmp version.  This was noticed in the RFC 4210-bis draft document and has been corrected there, but also affects this document which has already been published.
```

</details>

<br>**Explanation:**
The original ASN.1 module uses the incorrect version number ("cmp2012") for the CMP protocol. The correction uses the correct version number ("cmp2021"), resolving the inconsistency. This inconsistency would affect implementations that rely on the correct version number for processing CMP messages.

---

<details>
<summary><b>Errata 7833</b> from <b>RFC 9483</b> - Lightweight Certificate Management Protocol (CMP) Profile (November 2023)</summary>

```
Section 4.1.6 says:


-- MUST be 0 for recipientInfo type PasswordRecipientInfo

It should say:

-- MUST be 3 for recipientInfo type PasswordRecipientInfo

Notes:

It turns out that we make a mistake interpreting CMS RFC 5652 section 6.1 (https://datatracker.ietf.org/doc/html/rfc5652#section-6.1).

AFAICS, this was due to a misleadingly formatted condition in that section:

IF ((originatorInfo is present) AND
___(any version 2 attribute certificates are present)) OR
___(any RecipientInfo structures include pwri) OR
___(any RecipientInfo structures include ori)
THEN version is 3

where for clarity the indentation of the 2nd line should be one more character to the right:

IF ((originatorInfo is present) AND
____(any version 2 attribute certificates are present)) OR
___(any RecipientInfo structures include pwri) OR
___(any RecipientInfo structures include ori)
THEN version is 3

(I replaced leading space chars by '_' to make sure the indentation comes across.)

So this can also be seen as an editorial erratum of RFC 5652.
```

</details>

<br>**Explanation:**
The original text specifies an incorrect value (0) for the version number when using PasswordRecipientInfo. The correction uses the correct value (3), which is consistent with RFC 5652. This inconsistency would lead to implementations generating incorrectly formatted CMP messages.

---

<details>
<summary><b>Errata 8183</b> from <b>RFC 9483</b> - Lightweight Certificate Management Protocol (CMP) Profile (November 2023)</summary>

```
Section 4.1.6.1 says:


              rid             REQUIRED
    -- MUST contain the subjectKeyIdentifier of the CMP protection
    --   certificate, if available, in the rKeyId choice, and the
    --   subjectKeyIdentifier MUST equal the senderKID in the
    --   PKIHeader.
    -- If the CMP protection certificate does not contain a
    --   subjectKeyIdentifier, the issuerAndSerialNumber choice MUST
    --   be used.


It should say:

              rid             REQUIRED	
-- MUST contain the subjectKeyIdentifier of the CMP protection
--   certificate of the request message, if available. The
--   subjectKeyIdentifier is equal the senderKID in the
--   PKIHeader of that message.
-- If the CMP protection certificate of the request message does
--   not contain a subjectKeyIdentifier, the issuerAndSerialNumber
--   choice MUST be used.



Notes:

1. rKeyId choice is wrongly used here as Section 6.2.1 of RFC 5652 does not have rKeyId choice. 
2. rid value must be taken from CMP protection certificate of request message as it is used to specify the recipient.
```

</details>

<br>**Explanation:**
The original text refers to the incorrect method for specifying the recipient identifier (rid), using the rKeyId choice which is not defined in RFC 5652. The correction clarifies that the subjectKeyIdentifier from the request's protection certificate should be used, or issuerAndSerialNumber if subjectKeyIdentifier is absent, resolving the inconsistency.

---

<details>
<summary><b>Errata 8184</b> from <b>RFC 9483</b> - Lightweight Certificate Management Protocol (CMP) Profile (November 2023)</summary>

```
Section 4.1.6.2 says:


          rid           REQUIRED
-- MUST contain the subjectKeyIdentifier of the CMP protection
--   certificate, if available, in the rKeyId choice, and the
--   subjectKeyIdentifier MUST equal the senderKID in the
--   PKIHeader.
-- If the CMP protection certificate does not contain a
--   subjectKeyIdentifier, the issuerAndSerialNumber choice MUST
--   be used


It should say:

          rid           REQUIRED
-- MUST contain the subjectKeyIdentifier of the CMP protection
--   certificate of the request message, if available, in the
--   rKeyId choice. The subjectKeyIdentifier is equal
--   the senderKID in the PKIHeader of that message.
-- If the CMP protection certificate of the request message does
--   not contain a subjectKeyIdentifier, the issuerAndSerialNumber
--   choice MUST be used.


Notes:

1. rid value must be taken from CMP protection certificate of request message as it is used to identify the recipient using key agreement.
2. senderKID refer to value in request message, and here we are preparing the response message. So MUST is removed.
```

</details>

<br>**Explanation:**
The original text uses the term "rKeyId choice", which is not defined in RFC 5652, and incorrectly implies a requirement that the subjectKeyIdentifier MUST equal the senderKID in the PKIHeader of the response message. The correction clarifies that the subjectKeyIdentifier from the CMP protection certificate of the request message should be used, and removes the MUST condition, aligning with the intended behavior. This inconsistency could lead to implementations incorrectly handling the rid parameter.

---

<details>
<summary><b>Errata 8020</b> from <b>RFC 9487</b> - Export of Segment Routing over IPv6 Information in IP Flow Information Export (IPFIX) (November 2023)</summary>

```
Section A.2 says:


Figure 7:

   0                   1                   2                   3
   0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Set ID = 3            |          Length = 24          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|       Template ID 259         |        Field Count = 3        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Scope Field Count = 1     |0| srhActiveSegmentIPv6 = 495  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|   Scope 1 Field Length = 4    |0|srhSegmentIPv6End.Behav = 502|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|       Field Length = 1        |0|srhSegmentIPv6Lo.Length = 501|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|       Field Length = 4        |           Padding             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

Figure 8:

 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         SET ID = 259          |           Length = 28         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|               srhActiveSegmentIPv6 = 2001:db8::1              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|srhSegmentIPv6EndpointBehavior |srhSegmentIPv6LocatorLength= 48|
|= End [1]                      |                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|               srhActiveSegmentIPv6 = 2001:db8::4              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|srhSegmentIPv6EndpointBehavior |srhSegmentIPv6LocatorLength= 48|
|= End with NEXT-CSID [43]      |                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|               srhActiveSegmentIPv6 = 2001:db8::6              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|srhSegmentIPv6EndpointBehavior |srhSegmentIPv6LocatorLength= 48|
|= End.DX6 [16]                 |                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+




It should say:

Figure 7:

 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Set ID = 3            |          Length = 24          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|       Template ID 259         |        Field Count = 3        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|     Scope Field Count = 1     |0|     srhSegmentIPv6 = 494    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|   Scope 1 Field Length = 4    |0|srhSegmentIPv6End.Behav = 502|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|       Field Length = 1        |0|srhSegmentIPv6Lo.Length = 501|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|       Field Length = 4        |           Padding             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+


Figure 8:

 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         SET ID = 259          |           Length = 28         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                  srhSegmentIPv6 = 2001:db8::1                 |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|srhSegmentIPv6EndpointBehavior |srhSegmentIPv6LocatorLength= 48|
|= End [1]                      |                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                  srhSegmentIPv6 = 2001:db8::4                 |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|srhSegmentIPv6EndpointBehavior |srhSegmentIPv6LocatorLength= 48|
|= End with NEXT-CSID [43]      |                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                  srhSegmentIPv6 = 2001:db8::6                 |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|srhSegmentIPv6EndpointBehavior |srhSegmentIPv6LocatorLength= 48|
|= End.DX6 [16]                 |                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

Notes:

Example in Appendix A.2 should state IE494 srhSegmentIPv6  instead of IE495 srhActiveSegmentIPv6 for mapping the IE510 srhSegmentIPv6LocatorLength and IE502 srhSegmentIPv6EndpointBehavior in IPFIX option-template as described in Section 6.2.

Errata has been reported to me by a software developer of a major vendor working on implementation.

Also, the first two lines of Figure 7 are two characters to the right from the correct place. This was reported by Carsten Bormann.
```

</details>

<br>**Explanation:**
The figures in Appendix A.2 use incorrect information element IDs for srhSegmentIPv6. The correction replaces the incorrect ID (495) with the correct ID (494), resolving the inconsistency between the example and the specification.

---

<details>
<summary><b>Errata 7737</b> from <b>RFC 9514</b> - Border Gateway Protocol - Link State (BGP-LS) Extensions for Segment Routing over IPv6 (SRv6) (December 2023)</summary>

```
Section 5.1 says:


   The IPv6 Prefix matching the locator may also be advertised as prefix
   reachability by the underlying routing protocol.  In this case, the
   Prefix NLRI would also be associated with the Prefix Metric TLV
   [RFC7752] that carries the routing metric for this prefix.  A Prefix
   NLRI that has been advertised with a SRv6 Locator TLV is also
   considered a normal routing prefix (i.e., prefix reachability) only
   when there is also an IGP Metric TLV (TLV 1095) associated it.
   Otherwise, it is only considered an SRv6 Locator advertisement.

It should say:

   The IPv6 Prefix matching the locator may also be advertised as prefix
   reachability by the underlying routing protocol.  In this case, the
   Prefix NLRI would also be associated with the Prefix Metric TLV
   [RFC7752] that carries the routing metric for this prefix.  A Prefix
   NLRI that has been advertised with a SRv6 Locator TLV is also
   considered a normal routing prefix (i.e., prefix reachability) only
   when there is also a Prefix Metric TLV (TLV 1155) associated with it.
   Otherwise, it is only considered an SRv6 Locator advertisement.

Notes:

The current text is referring to the wrong BGP-LS TLV. Since the SRv6 Locator TLV is associated with a Prefix NLRI, the "Prefix Metric TLV (TLV 1155)" should be referenced here since the "IGP metric TLV (TLV 1095)" is associated with a Link NLRI.

Verifier note: In addition to the fix proposed by Ketan, I added a preposition: "associated with it".
```

</details>

<br>**Explanation:**
The original text refers to the incorrect TLV (IGP metric TLV, TLV 1095) for Prefix NLRIs. The correction uses the correct TLV (Prefix Metric TLV, TLV 1155), which is consistent with the specification. This inconsistency could affect implementations that rely on the correct TLV to identify normal routing prefixes.

---

<details>
<summary><b>Errata 7876</b> from <b>RFC 9537</b> - Redacted Fields in the Registration Data Access Protocol (RDAP) Response (March 2024)</summary>

```
Section 4.2 says:


Figure 13:

  {
    "rdapConformance": [
      "rdap_level_0"
    ],
    "domainSearchResults":[
      {
        "objectClassName": "domain",
        "handle": "ABC121",
        "ldhName": "example1.com",
        "links":[
          {
            "value":"https://example.com/rdap/domain/example1.com",
            "rel":"self",
            "href":"https://example.com/rdap/domain/example1.com",
            "type":"application/rdap+json"
          },
          {
            "value":"https://example.com/rdap/domain/example1.com",
            "rel":"related",
            "href":"https://example.com/rdap/domain/example1.com",
            "type":"application/rdap+json"
          }
        ]
      },
      {
        "objectClassName": "domain",
        "handle": "ABC122",
        "ldhName": "example2.com",
        "links":[
          {
            "value":"https://example.com/rdap/domain/example2.com",
            "rel":"self",
            "href":"https://example.com/rdap/domain/example2.com",
            "type":"application/rdap+json"
          },
          {
            "value":"https://example.com/rdap/domain/example2.com",
            "rel":"related",
            "href":"https://example.com/rdap/domain/example2.com",
            "type":"application/rdap+json"
          }
        ]
      }
    ]
  }

Figure 14:

  {
    "rdapConformance": [
      "rdap_level_0",
      "redacted"
    ],
    "domainSearchResults":[
      {
        "objectClassName": "domain",
        "ldhName": "example1.com",
        "links":[
          {
            "value":"https://example.com/rdap/domain/example1.com",
            "rel":"self",
            "href":"https://example.com/rdap/domain/example1.com",
            "type":"application/rdap+json"
          },
          {
            "value":"https://example.com/rdap/domain/example1.com",
            "rel":"related",
            "href":"https://example.com/rdap/domain/example1.com",
            "type":"application/rdap+json"
          }
        ],
        "redacted": [
          {
            "name": {
              "type": "Registry Domain ID"
            },
            "prePath": "$.domainSearchResults[0].handle",
            "pathLang": "jsonpath",
            "method": "removal",
            "reason": {
              "type": "Server policy"
            }
          }
        ]
      },
      {
        "objectClassName": "domain",
        "ldhName": "example2.com",
        "links":[
          {
            "value":"https://example.com/rdap/domain/example2.com",
            "rel":"self",
            "href":"https://example.com/rdap/domain/example2.com",
            "type":"application/rdap+json"
          },
          {
            "value":"https://example.com/rdap/domain/example2.com",
            "rel":"related",
            "href":"https://example.com/rdap/domain/example2.com",
            "type":"application/rdap+json"
          }
        ],
        "redacted": [
          {
            "name": {
              "description": "Registry Domain ID"
            },
            "prePath": "$.domainSearchResults[1].handle",
            "pathLang": "jsonpath",
            "method": "removal",
            "reason": {
              "description": "Server policy"
            }
          }
        ]
      }
    ]
  }

It should say:

Figure 13:

  {
    "rdapConformance": [
      "rdap_level_0"
    ],
    "domainSearchResults":[
      {
        "objectClassName": "domain",
        "handle": "ABC121",
        "ldhName": "example1.com",
        "links":[
          {
            "value":"https://example.com/rdap/domain/example1.com",
            "rel":"self",
            "href":"https://example.com/rdap/domain/example1.com",
            "type":"application/rdap+json"
          },
          {
            "value":"https://example.com/rdap/domain/example1.com",
            "rel":"related",
            "href":"https://example.net/rdap/v1/domain/example1.com",
            "type":"application/rdap+json"
          }
        ]
      },
      {
        "objectClassName": "domain",
        "handle": "ABC122",
        "ldhName": "example2.com",
        "links":[
          {
            "value":"https://example.com/rdap/domain/example2.com",
            "rel":"self",
            "href":"https://example.com/rdap/domain/example2.com",
            "type":"application/rdap+json"
          },
          {
            "value":"https://example.com/rdap/domain/example2.com",
            "rel":"related",
            "href":"https://example.net/rdap/v1/domain/example2.com",
            "type":"application/rdap+json"
          }
        ]
      }
    ]
  }

Figure 14:

  {
    "rdapConformance": [
      "rdap_level_0",
      "redacted"
    ],
    "domainSearchResults":[
      {
        "objectClassName": "domain",
        "ldhName": "example1.com",
        "links":[
          {
            "value":"https://example.com/rdap/domain/example1.com",
            "rel":"self",
            "href":"https://example.com/rdap/domain/example1.com",
            "type":"application/rdap+json"
          },
          {
            "value":"https://example.com/rdap/domain/example1.com",
            "rel":"related",
            "href":"https://example.net/rdap/v1/domain/example1.com",
            "type":"application/rdap+json"
          }
        ],
        "redacted": [
          {
            "name": {
              "type": "Registry Domain ID"
            },
            "prePath": "$.domainSearchResults[0].handle",
            "pathLang": "jsonpath",
            "method": "removal",
            "reason": {
              "type": "Server policy"
            }
          }
        ]
      },
      {
        "objectClassName": "domain",
        "ldhName": "example2.com",
        "links":[
          {
            "value":"https://example.com/rdap/domain/example2.com",
            "rel":"self",
            "href":"https://example.com/rdap/domain/example2.com",
            "type":"application/rdap+json"
          },
          {
            "value":"https://example.com/rdap/domain/example2.com",
            "rel":"related",
            "href":"https://example.net/rdap/v1/domain/example2.com",
            "type":"application/rdap+json"
          }
        ],
        "redacted": [
          {
            "name": {
              "description": "Registry Domain ID"
            },
            "prePath": "$.domainSearchResults[1].handle",
            "pathLang": "jsonpath",
            "method": "removal",
            "reason": {
              "description": "Server policy"
            }
          }
        ]
      }
    ]
  }

Notes:

Noticed that the "self" and "related" links in Figure 13 and Figure 14 examples have the same "href" value. From RFC 9083: A "related" link relation MUST NOT include an "href" URI that is the same as the "self" link relation "href" URI to reduce the risk of infinite client processing loops. (The new "href" values for the "related" links are per James Gould's earlier suggestion.)
```

</details>

<br>**Explanation:**
The example in Figure 13 uses the same "href" value for both "self" and "related" links, which is inconsistent with the requirement in RFC 9083 that these URIs must be different to prevent infinite client processing loops.

---

<details>
<summary><b>Errata 7929</b> from <b>RFC 9562</b> - Universally Unique IDentifiers (UUIDs) (May 2024)</summary>

```
Section B.2 says:


custom_c  62   0b00, 0x38a375d0df1fbf6

It should say:

custom_c  62   0b01, 0x38a375d0df1fbf6

Notes:

As shown as -938a- in Figure 30.

B: xxxxxxxx-xxxx-Mxxx-Nxxx-xxxxxxxxxxxx
C: 5c146b14-3c52-8afd-938a-375d0df1fbf6

See also: https://mailarchive.ietf.org/arch/msg/uuidrev/2wJLek182NMv4xQZf8TIos6XrD0/
```

</details>

<br>**Explanation:**
The original example uses an incorrect value for the custom_c variant.  The correction provides the correct value, which is consistent with Figure 30.  This inconsistency would affect implementations that rely on the correct values for UUID variants.

---

<details>
<summary><b>Errata 7958</b> from <b>RFC 9562</b> - Universally Unique IDentifiers (UUIDs) (May 2024)</summary>

```
Section 4.1 says:


     | 0    | x    | x    | x    | 1-7     | Reserved.  Network      |
     |      |      |      |      |         | Computing System (NCS)  |
     |      |      |      |      |         | backward compatibility, |
     |      |      |      |      |         | and includes Nil UUID   |
     |      |      |      |      |         | as per Section 5.9.     |


It should say:

     | 0    | x    | x    | x    | 0-7     | Reserved.  Network      |
     |      |      |      |      |         | Computing System (NCS)  |
     |      |      |      |      |         | backward compatibility, |
     |      |      |      |      |         | and includes Nil UUID   |
     |      |      |      |      |         | as per Section 5.9.     |


Notes:

This row matches the case where MSB0, MSB1, MSB2, MSB3 are all 0, which would make the variant number 0.
```

</details>

<br>**Explanation:**
The original text incorrectly restricts the version number to 1-7, while version 0 is also valid. The correction changes the range to 0-7, making it consistent with the description and the valid range for version numbers.

---

<details>
<summary><b>Errata 7955</b> from <b>RFC 9562</b> - Universally Unique IDentifiers (UUIDs) (May 2024)</summary>

```
Section 5.1 says:


time_high:
    The least significant 12 bits from the 60-bit starting timestamp.
    Occupies bits 52 through 63 (octets 6-7).

It should say:

time_high:
    The most significant 12 bits from the 60-bit starting timestamp.
    Occupies bits 52 through 63 (octets 6-7).

Notes:

The original text has the least significant 12 bits from the 60-bit starting timestamp duplicated in the UUID. Once as the least significant 12 bits of time_low and again as time_high. The most significant 12 bits of the starting timestamp are omitted from the UUID.

The corrected text gives the self-evident intention of the committee.
```

</details>

<br>**Explanation:**
The original text incorrectly describes the time_high field as containing the least significant bits of the timestamp. The correction clarifies that it contains the most significant bits, which is the intended behavior. This inconsistency could lead to incorrect generation of UUIDs.

---

<details>
<summary><b>Errata 7947</b> from <b>RFC 9568</b> - Virtual Router Redundancy Protocol (VRRP) Version 3 for IPv4 and IPv6 (April 2024)</summary>

```
Section 6.4.1 says:


         o  For each IPv4 address associated with the Virtual Router,
            broadcast a gratuitous ARP message containing the Virtual
            Router MAC address and with the target link-layer address
            set to the Virtual Router MAC address.



It should say:

         o  For each IPv4 address associated with the Virtual Router,
            broadcast a gratuitous ARP message containing the Virtual
            Router IPv4 address and with the target link-layer address
            set to the Virtual Router MAC address.



Notes:

The MAC address is specified instead of the IPv4 address.
```

</details>

<br>**Explanation:**
The original text incorrectly specifies the MAC address in the gratuitous ARP message. The correction uses the IPv4 address, which is consistent with the gratuitous ARP protocol. This inconsistency would lead to implementations generating incorrect gratuitous ARP messages.

---

<details>
<summary><b>Errata 7949</b> from <b>RFC 9568</b> - Virtual Router Redundancy Protocol (VRRP) Version 3 for IPv4 and IPv6 (April 2024)</summary>

```
Section 6.4.2 says:


         o  For each IPv4 address associated with the Virtual Router,
            broadcast a gratuitous ARP message containing the Virtual
            Router MAC address and with the target link-layer address
            set to the Virtual Router MAC address.


It should say:

         o  For each IPv4 address associated with the Virtual Router,
            broadcast a gratuitous ARP message containing the Virtual
            Router IPv4 address and with the target link-layer address
            set to the Virtual Router MAC address.


Notes:

The MAC address is specified instead of the IPv4 address.
```

</details>

<br>**Explanation:**
The original text incorrectly specifies the MAC address in the gratuitous ARP message. The correction uses the IPv4 address, which is consistent with the gratuitous ARP protocol. This inconsistency would lead to implementations generating incorrect gratuitous ARP messages.

---

<details>
<summary><b>Errata 8256</b> from <b>RFC 9639</b> - Free Lossless Audio Codec (FLAC) (December 2024)</summary>

```
Section 8.2 says:


   SSAAAAAASSBBBBBBSSCCCCCC
   ^   ^   ^   ^   ^   ^
   |   |   |   |   |  Bits of 2nd sample of 1st channel
   |   |   |   |  Sign extension bits of 2nd sample of 2nd channel
   |   |   |  Bits of 1st sample of 2nd channel
   |   |  Sign extension bits of 1st sample of 2nd channel
   |  Bits of 1st sample of 1st channel
   Sign extension bits of 1st sample of 1st channel

It should say:

   SSAAAAAASSBBBBBBSSCCCCCC
   ^   ^   ^   ^   ^   ^
   |   |   |   |   |  Bits of 2nd sample of 1st channel
   |   |   |   |  Sign extension bits of 2nd sample of 1st channel
   |   |   |  Bits of 1st sample of 2nd channel
   |   |  Sign extension bits of 1st sample of 2nd channel
   |  Bits of 1st sample of 1st channel
   Sign extension bits of 1st sample of 1st channel

Notes:

One of the diagram labels appears to contradict the sign-extension + interleaving method described in the preceding paragraph.
```

</details>

<br>**Explanation:**
The diagram incorrectly labels the sign extension bits for the second sample of the second channel. The correction uses the correct channel for the sign extension bits, aligning the diagram with the described interleaving and sign-extension method.

---

<details>
<summary><b>Errata 8131</b> from <b>RFC 9656</b> - A YANG Data Model for Microwave Topology (September 2024)</summary>

```
Section A.1 says:


   {
     "ietf-network:networks": {
       "network": [
         {
           "network-id": "L2-network",
           "network-types": {
             "ietf-te-topology:te-topology": {}
           },
           "supporting-network": [
             {
               "network-ref": "mw-network"
             }
           ],
           "node": [
             {
               "node-id": "L2-N1",
               "supporting-node": [
                 {
                   "network-ref": "mw-network",
                   "node-ref": "mw-N1"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "L2-N1-TP1",
                   "supporting-termination-point": [
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N1",
                       "tp-ref": "mw-N1-RLTP1"
                     }
                   ]
                 }
               ]
             },
             {
               "node-id": "L2-N2",
               "supporting-node": [
                 {
                   "network-ref": "mw-network",
                   "node-ref": "mw-N2"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "L2-N2-TP2",
                   "supporting-termination-point": [
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N2",
                       "tp-ref": "mw-N2-RLTP2"
                     }
                   ]
                 }
               ]
             }
           ],
           "ietf-network-topology:link": [
             {
               "link-id": "L2-N1-N2",
               "source": {
                 "source-node": "L2-N1",
                 "source-tp": "L2-N1-TP1"
               },
               "destination": {
                 "dest-node": "L2-N2",
                 "dest-tp": "L2-N2-TP2"
               },
               "supporting-link": [
                 {
                   "network-ref": "mw-network",
                   "link-ref": "mwrl-N1-N2"
                 }
               ]
             }
           ]
         },
         {
           "network-id": "mw-network",
           "network-types": {
             "ietf-te-topology:te-topology": {
               "ietf-microwave-topology:mw-topology": {}
             }
           },
           "supporting-network": [
             {
               "network-ref": "mw-network"
             }
           ],
           "node": [
             {
               "node-id": "mw-N1",
               "supporting-node": [
                 {
                   "network-ref": "mw-network",
                   "node-ref": "mw-N1"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "mw-N1-RLTP1",
                   "supporting-termination-point": [
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N1",
                       "tp-ref": "mw-N1-CTP1"
                     },
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N1",
                       "tp-ref": "mw-N1-CTP3"
                     }
                   ],
                   "ietf-te-topology:te-tp-id": "192.0.2.3",
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-rltp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "mw-N1-CTP1",
                   "ietf-te-topology:te-tp-id": 1,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "mw-N1-CTP3",
                   "ietf-te-topology:te-tp-id": 2,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 }
               ]
             },
             {
               "node-id": "mw-N2",
               "supporting-node": [
                 {
                   "network-ref": "mw-network",
                   "node-ref": "mw-N2"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "mw-N2-RLTP2",
                   "supporting-termination-point": [
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N2",
                       "tp-ref": "mw-N2-CTP2"
                     },
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N2",
                       "tp-ref": "mw-N2-CTP4"
                     }
                   ],
                   "ietf-te-topology:te-tp-id": "192.0.2.4",
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-rltp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "mw-N2-CTP2",
                   "ietf-te-topology:te-tp-id": 1,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "mw-N2-CTP4",
                   "ietf-te-topology:te-tp-id": 2,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 }
               ]
             }
           ],
           "ietf-network-topology:link": [
             {
               "link-id": "mwrl-N1-N2",
               "source": {
                 "source-node": "mw-N1",
                 "source-tp": "mw-N1-RLTP1"
               },
               "destination": {
                 "dest-node": "mw-N2",
                 "dest-tp": "mw-N2-RLTP2"
               },
               "ietf-te-topology:te": {
                 "bundled-links": {
                   "bundled-link": [
                     {
                       "sequence": 1,
                       "src-tp-ref": "mw-N1-CTP1",
                       "des-tp-ref": "mw-N2-CTP2"
                     },
                     {
                       "sequence": 2,
                       "src-tp-ref": "mw-N1-CTP3",
                       "des-tp-ref": "mw-N2-CTP4"
                     }
                   ]
                 },
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-radio-link": {
                       "rlt-mode": {
                         "num-bonded-carriers": 2,
                         "num-protecting-carriers": 0
                       }
                     }
                   }
                 }
               }
             },
             {
               "link-id": "mwc-N1-N2-A",
               "source": {
                 "source-node": "mw-N1",
                 "source-tp": "mw-N1-CTP1"
               },
               "destination": {
                 "dest-node": "mw-N2",
                 "dest-tp": "mw-N2-CTP2"
               },
               "ietf-te-topology:te": {
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-carrier": {
                       "tx-frequency": 10728000,
                       "channel-separation": 28000
                     }
                   }
                 }
               }
             },
             {
               "link-id": "mwc-N1-N2-B",
               "source": {
                 "source-node": "mw-N1",
                 "source-tp": "mw-N1-CTP3"
               },
               "destination": {
                 "dest-node": "mw-N2",
                 "dest-tp": "mw-N2-CTP4"
               },
               "ietf-te-topology:te": {
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-carrier": {
                       "tx-frequency": 10528000,
                       "channel-separation": 28000
                     }
                   }
                 }
               }
             }
           ]
         }
       ]
     }
   }

It should say:

   {
     "ietf-network:networks": {
       "network": [
         {
           "network-id": "example:L2-network",
           "network-types": {
             "ietf-te-topology:te-topology": {}
           },
           "supporting-network": [
             {
               "network-ref": "example:mw-network"
             }
           ],
           "node": [
             {
               "node-id": "example:L2-N1",
               "supporting-node": [
                 {
                   "network-ref": "example:mw-network",
                   "node-ref": "example:mw-N1"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "example:L2-N1-TP1",
                   "supporting-termination-point": [
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N1",
                       "tp-ref": "example:mw-N1-RLTP1"
                     }
                   ]
                 }
               ]
             },
             {
               "node-id": "example:L2-N2",
               "supporting-node": [
                 {
                   "network-ref": "example:mw-network",
                   "node-ref": "example:mw-N2"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "example:L2-N2-TP2",
                   "supporting-termination-point": [
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N2",
                       "tp-ref": "example:mw-N2-RLTP2"
                     }
                   ]
                 }
               ]
             }
           ],
           "ietf-network-topology:link": [
             {
               "link-id": "example:L2-N1-N2",
               "source": {
                 "source-node": "example:L2-N1",
                 "source-tp": "example:L2-N1-TP1"
               },
               "destination": {
                 "dest-node": "example:L2-N2",
                 "dest-tp": "example:L2-N2-TP2"
               },
               "supporting-link": [
                 {
                   "network-ref": "example:mw-network",
                   "link-ref": "example:mwrl-N1-N2"
                 }
               ]
             }
           ]
         },
         {
           "network-id": "example:mw-network",
           "network-types": {
             "ietf-te-topology:te-topology": {
               "ietf-microwave-topology:mw-topology": {}
             }
           },
           "supporting-network": [
             {
               "network-ref": "example:mw-network"
             }
           ],
           "node": [
             {
               "node-id": "example:mw-N1",
               "supporting-node": [
                 {
                   "network-ref": "example:mw-network",
                   "node-ref": "example:mw-N1"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "example:mw-N1-RLTP1",
                   "supporting-termination-point": [
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N1",
                       "tp-ref": "example:mw-N1-CTP1"
                     },
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N1",
                       "tp-ref": "example:mw-N1-CTP3"
                     }
                   ],
                   "ietf-te-topology:te-tp-id": "192.0.2.3",
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-rltp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "example:mw-N1-CTP1",
                   "ietf-te-topology:te-tp-id": 1,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "example:mw-N1-CTP3",
                   "ietf-te-topology:te-tp-id": 2,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 }
               ]
             },
             {
               "node-id": "example:mw-N2",
               "supporting-node": [
                 {
                   "network-ref": "example:mw-network",
                   "node-ref": "example:mw-N2"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "example:mw-N2-RLTP2",
                   "supporting-termination-point": [
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N2",
                       "tp-ref": "example:mw-N2-CTP2"
                     },
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N2",
                       "tp-ref": "example:mw-N2-CTP4"
                     }
                   ],
                   "ietf-te-topology:te-tp-id": "192.0.2.4",
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-rltp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "example:mw-N2-CTP2",
                   "ietf-te-topology:te-tp-id": 1,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "example:mw-N2-CTP4",
                   "ietf-te-topology:te-tp-id": 2,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 }
               ]
             }
           ],
           "ietf-network-topology:link": [
             {
               "link-id": "example:mwrl-N1-N2",
               "source": {
                 "source-node": "example:mw-N1",
                 "source-tp": "example:mw-N1-RLTP1"
               },
               "destination": {
                 "dest-node": "example:mw-N2",
                 "dest-tp": "example:mw-N2-RLTP2"
               },
               "ietf-te-topology:te": {
                 "bundled-links": {
                   "bundled-link": [
                     {
                       "sequence": 1,
                       "src-tp-ref": "example:mw-N1-CTP1",
                       "des-tp-ref": "example:mw-N2-CTP2"
                     },
                     {
                       "sequence": 2,
                       "src-tp-ref": "example:mw-N1-CTP3",
                       "des-tp-ref": "example:mw-N2-CTP4"
                     }
                   ]
                 },
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-radio-link": {
                       "rlt-mode": {
                         "num-bonded-carriers": 2,
                         "num-protecting-carriers": 0
                       }
                     }
                   }
                 }
               }
             },
             {
               "link-id": "example:mwc-N1-N2-A",
               "source": {
                 "source-node": "example:mw-N1",
                 "source-tp": "example:mw-N1-CTP1"
               },
               "destination": {
                 "dest-node": "example:mw-N2",
                 "dest-tp": "example:mw-N2-CTP2"
               },
               "ietf-te-topology:te": {
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-carrier": {
                       "tx-frequency": 10728000,
                       "channel-separation": 28000
                     }
                   }
                 }
               }
             },
             {
               "link-id": "example:mwc-N1-N2-B",
               "source": {
                 "source-node": "example:mw-N1",
                 "source-tp": "example:mw-N1-CTP3"
               },
               "destination": {
                 "dest-node": "example:mw-N2",
                 "dest-tp": "example:mw-N2-CTP4"
               },
               "ietf-te-topology:te": {
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-carrier": {
                       "tx-frequency": 10528000,
                       "channel-separation": 28000
                     }
                   }
                 }
               }
             }
           ]
         }
       ]
     }
   }

Notes:

Fixed URI names to follow RFC8407bis guidelines.

See also https://mailarchive.ietf.org/arch/msg/ccamp/OQ-oLx2smsmdC4dcn6aB9i-hWE8/
```

</details>

<br>**Explanation:**
The example omits namespace prefixes in several places, which is inconsistent with RFC 8407bis guidelines for properly qualified URIs.  The correction adds the necessary prefixes to all node identifiers and references.

---

<details>
<summary><b>Errata 8132</b> from <b>RFC 9656</b> - A YANG Data Model for Microwave Topology (September 2024)</summary>

```
Section A.2 says:


   {
     "ietf-network:networks": {
       "network": [
         {
           "network-id": "L2-network",
           "network-types": {
             "ietf-te-topology:te-topology": {}
           },
           "supporting-network": [
             {
               "network-ref": "mw-network"
             }
           ],
           "node": [
             {
               "node-id": "L2-N1",
               "supporting-node": [
                 {
                   "network-ref": "mw-network",
                   "node-ref": "mw-N1"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "L2-N1-TP1",
                   "supporting-termination-point": [
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N1",
                       "tp-ref": "mw-N1-RLTP1"
                     }
                   ]
                 }
               ]
             },
             {
               "node-id": "L2-N2",
               "supporting-node": [
                 {
                   "network-ref": "mw-network",
                   "node-ref": "mw-N2"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "L2-N2-TP2",
                   "supporting-termination-point": [
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N2",
                       "tp-ref": "mw-N2-RLTP2"
                     }
                   ]
                 }
               ]
             }
           ],
           "ietf-network-topology:link": [
             {
               "link-id": "L2-N1-N2",
               "source": {
                 "source-node": "L2-N1",
                 "source-tp": "L2-N1-TP1"
               },
               "destination": {
                 "dest-node": "L2-N2",
                 "dest-tp": "L2-N2-TP2"
               },
               "supporting-link": [
                 {
                   "network-ref": "mw-network",
                   "link-ref": "mwrl-N1-N2"
                 }
               ]
             }
           ]
         },
         {
           "network-id": "mw-network",
           "network-types": {
             "ietf-te-topology:te-topology": {
               "ietf-microwave-topology:mw-topology": {}
             }
           },
           "supporting-network": [
             {
               "network-ref": "mw-network"
             }
           ],
           "node": [
             {
               "node-id": "mw-N1",
               "supporting-node": [
                 {
                   "network-ref": "mw-network",
                   "node-ref": "mw-N1"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "mw-N1-RLTP1",
                   "supporting-termination-point": [
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N1",
                       "tp-ref": "mw-N1-CTP1"
                     },
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N1",
                       "tp-ref": "mw-N1-CTP3"
                     }
                   ],
                   "ietf-te-topology:te-tp-id": "192.0.2.3",
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-rltp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "mw-N1-CTP1",
                   "ietf-te-topology:te-tp-id": 1,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "mw-N1-CTP3",
                   "ietf-te-topology:te-tp-id": 2,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 }
               ]
             },
             {
               "node-id": "mw-N2",
               "supporting-node": [
                 {
                   "network-ref": "mw-network",
                   "node-ref": "mw-N2"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "mw-N2-RLTP2",
                   "supporting-termination-point": [
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N2",
                       "tp-ref": "mw-N2-CTP2"
                     },
                     {
                       "network-ref": "mw-network",
                       "node-ref": "mw-N2",
                       "tp-ref": "mw-N2-CTP4"
                     }
                   ],
                   "ietf-te-topology:te-tp-id": "192.0.2.4",
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-rltp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "mw-N2-CTP2",
                   "ietf-te-topology:te-tp-id": 1,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "mw-N2-CTP4",
                   "ietf-te-topology:te-tp-id": 2,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 }
               ]
             }
           ],
           "ietf-network-topology:link": [
             {
               "link-id": "mwrl-N1-N2",
               "source": {
                 "source-node": "mw-N1",
                 "source-tp": "mw-N1-RLTP1"
               },
               "destination": {
                 "dest-node": "mw-N2",
                 "dest-tp": "mw-N2-RLTP2"
               },
               "ietf-te-topology:te": {
                 "bundled-links": {
                   "bundled-link": [
                     {
                       "sequence": 1,
                       "src-tp-ref": "mw-N1-CTP1",
                       "des-tp-ref": "mw-N2-CTP2"
                     },
                     {
                       "sequence": 2,
                       "src-tp-ref": "mw-N1-CTP3",
                       "des-tp-ref": "mw-N2-CTP4"
                     }
                   ]
                 },
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-radio-link": {
                       "rlt-mode": {
                         "num-bonded-carriers": 1,
                         "num-protecting-carriers": 1
                       }
                     }
                   }
                 }
               }
             },
             {
               "link-id": "mwc-N1-N2-A",
               "source": {
                 "source-node": "mw-N1",
                 "source-tp": "mw-N1-CTP1"
               },
               "destination": {
                 "dest-node": "mw-N2",
                 "dest-tp": "mw-N2-CTP2"
               },
               "ietf-te-topology:te": {
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-carrier": {
                       "tx-frequency": 10728000,
                       "channel-separation": 28000
                     }
                   }
                 }
               }
             },
             {
               "link-id": "mwc-N1-N2-B",
               "source": {
                 "source-node": "mw-N1",
                 "source-tp": "mw-N1-CTP3"
               },
               "destination": {
                 "dest-node": "mw-N2",
                 "dest-tp": "mw-N2-CTP4"
               },
               "ietf-te-topology:te": {
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-carrier": {
                       "tx-frequency": 10728000,
                       "channel-separation": 28000
                     }
                   }
                 }
               }
             }
           ]
         }
       ]
     }
   }

It should say:

   {
     "ietf-network:networks": {
       "network": [
         {
           "network-id": "example:L2-network",
           "network-types": {
             "ietf-te-topology:te-topology": {}
           },
           "supporting-network": [
             {
               "network-ref": "example:mw-network"
             }
           ],
           "node": [
             {
               "node-id": "example:L2-N1",
               "supporting-node": [
                 {
                   "network-ref": "example:mw-network",
                   "node-ref": "example:mw-N1"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "example:L2-N1-TP1",
                   "supporting-termination-point": [
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N1",
                       "tp-ref": "example:mw-N1-RLTP1"
                     }
                   ]
                 }
               ]
             },
             {
               "node-id": "example:L2-N2",
               "supporting-node": [
                 {
                   "network-ref": "example:mw-network",
                   "node-ref": "example:mw-N2"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "example:L2-N2-TP2",
                   "supporting-termination-point": [
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N2",
                       "tp-ref": "example:mw-N2-RLTP2"
                     }
                   ]
                 }
               ]
             }
           ],
           "ietf-network-topology:link": [
             {
               "link-id": "example:L2-N1-N2",
               "source": {
                 "source-node": "example:L2-N1",
                 "source-tp": "example:L2-N1-TP1"
               },
               "destination": {
                 "dest-node": "example:L2-N2",
                 "dest-tp": "example:L2-N2-TP2"
               },
               "supporting-link": [
                 {
                   "network-ref": "example:mw-network",
                   "link-ref": "example:mwrl-N1-N2"
                 }
               ]
             }
           ]
         },
         {
           "network-id": "example:mw-network",
           "network-types": {
             "ietf-te-topology:te-topology": {
               "ietf-microwave-topology:mw-topology": {}
             }
           },
           "supporting-network": [
             {
               "network-ref": "example:mw-network"
             }
           ],
           "node": [
             {
               "node-id": "example:mw-N1",
               "supporting-node": [
                 {
                   "network-ref": "example:mw-network",
                   "node-ref": "example:mw-N1"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "example:mw-N1-RLTP1",
                   "supporting-termination-point": [
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N1",
                       "tp-ref": "example:mw-N1-CTP1"
                     },
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N1",
                       "tp-ref": "example:mw-N1-CTP3"
                     }
                   ],
                   "ietf-te-topology:te-tp-id": "192.0.2.3",
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-rltp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "example:mw-N1-CTP1",
                   "ietf-te-topology:te-tp-id": 1,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "example:mw-N1-CTP3",
                   "ietf-te-topology:te-tp-id": 2,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 }
               ]
             },
             {
               "node-id": "example:mw-N2",
               "supporting-node": [
                 {
                   "network-ref": "example:mw-network",
                   "node-ref": "example:mw-N2"
                 }
               ],
               "ietf-network-topology:termination-point": [
                 {
                   "tp-id": "example:mw-N2-RLTP2",
                   "supporting-termination-point": [
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N2",
                       "tp-ref": "example:mw-N2-CTP2"
                     },
                     {
                       "network-ref": "example:mw-network",
                       "node-ref": "example:mw-N2",
                       "tp-ref": "example:mw-N2-CTP4"
                     }
                   ],
                   "ietf-te-topology:te-tp-id": "192.0.2.4",
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-rltp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "example:mw-N2-CTP2",
                   "ietf-te-topology:te-tp-id": 1,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 },
                 {
                   "tp-id": "example:mw-N2-CTP4",
                   "ietf-te-topology:te-tp-id": 2,
                   "ietf-te-topology:te": {
                     "ietf-microwave-topology:mw-tp": {
                       "microwave-ctp": {}
                     }
                   }
                 }
               ]
             }
           ],
           "ietf-network-topology:link": [
             {
               "link-id": "example:mwrl-N1-N2",
               "source": {
                 "source-node": "example:mw-N1",
                 "source-tp": "example:mw-N1-RLTP1"
               },
               "destination": {
                 "dest-node": "example:mw-N2",
                 "dest-tp": "example:mw-N2-RLTP2"
               },
               "ietf-te-topology:te": {
                 "bundled-links": {
                   "bundled-link": [
                     {
                       "sequence": 1,
                       "src-tp-ref": "example:mw-N1-CTP1",
                       "des-tp-ref": "example:mw-N2-CTP2"
                     },
                     {
                       "sequence": 2,
                       "src-tp-ref": "example:mw-N1-CTP3",
                       "des-tp-ref": "example:mw-N2-CTP4"
                     }
                   ]
                 },
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-radio-link": {
                       "rlt-mode": {
                         "num-bonded-carriers": 1,
                         "num-protecting-carriers": 1
                       }
                     }
                   }
                 }
               }
             },
             {
               "link-id": "example:mwc-N1-N2-A",
               "source": {
                 "source-node": "example:mw-N1",
                 "source-tp": "example:mw-N1-CTP1"
               },
               "destination": {
                 "dest-node": "example:mw-N2",
                 "dest-tp": "example:mw-N2-CTP2"
               },
               "ietf-te-topology:te": {
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-carrier": {
                       "tx-frequency": 10728000,
                       "channel-separation": 28000
                     }
                   }
                 }
               }
             },
             {
               "link-id": "example:mwc-N1-N2-B",
               "source": {
                 "source-node": "example:mw-N1",
                 "source-tp": "example:mw-N1-CTP3"
               },
               "destination": {
                 "dest-node": "example:mw-N2",
                 "dest-tp": "example:mw-N2-CTP4"
               },
               "ietf-te-topology:te": {
                 "te-link-attributes": {
                   "ietf-microwave-topology:mw-link": {
                     "microwave-carrier": {
                       "tx-frequency": 10728000,
                       "channel-separation": 28000
                     }
                   }
                 }
               }
             }
           ]
         }
       ]
     }
   }

Notes:

Fixed URI names to follow RFC8407bis guidelines.

See also https://mailarchive.ietf.org/arch/msg/ccamp/OQ-oLx2smsmdC4dcn6aB9i-hWE8/
```

</details>

<br>**Explanation:**
The example in Annex A.2 uses an inconsistent number of protecting carriers (0) compared to the other examples and the description, which implies that this number should be 1 in a protected configuration.  The correction sets the num-protecting-carriers value to 1, resolving the inconsistency.

---

<details>
<summary><b>Errata 8133</b> from <b>RFC 9656</b> - A YANG Data Model for Microwave Topology (September 2024)</summary>

```
Section B.1 says:


   {
    "ietf-interfaces:interfaces": {
     "interface": [
      {
       "name": "L2Interface1",
       "description": "'Ethernet Interface 1'",
       "type": "iana-if-type:ethernetCsmacd"
      },
      {
       "name": "L2Interface2",
       "description": "'Ethernet Interface 2'",
       "type": "iana-if-type:ethernetCsmacd"
      },
      {
       "name": "RLT-1",
       "description": "'Radio Link Terminal 1'",
       "type": "iana-if-type:microwaveRadioLinkTerminal",
       "ietf-microwave-radio-link:mode":
         "ietf-microwave-types:two-plus-zero",
       "ietf-microwave-radio-link:carrier-terminations": [
        "CT-1",
        "CT-3"
       ]
      },
      {
       "name": "RLT-2",
       "description": "'Radio Link Terminal 2'",
       "type": "iana-if-type:microwaveRadioLinkTerminal",
       "ietf-microwave-radio-link:mode":
          "ietf-microwave-types:two-plus-zero",
       "ietf-microwave-radio-link:carrier-terminations": [
        "CT-2",
        "CT-4"
       ]
      },
      {
       "name": "CT-1",
       "description": "'Carrier Termination 1'",
       "type": "iana-if-type:microwaveCarrierTermination",
       "ietf-microwave-radio-link:tx-frequency": 10728000,
       "ietf-microwave-radio-link:duplex-distance": 113000,
       "ietf-microwave-radio-link:channel-separation": 28000,
       "ietf-microwave-radio-link:rtpc": {
        "maximum-nominal-power": "20.0"
       },
       "ietf-microwave-radio-link:single": {
        "selected-cm": "ietf-microwave-types:qam-512"
       }
      },
      {
       "name": "CT-3",
       "description": "'Carrier Termination 3'",
       "type": "iana-if-type:microwaveCarrierTermination",
       "ietf-microwave-radio-link:tx-frequency": 10528000,
       "ietf-microwave-radio-link:duplex-distance": 113000,
       "ietf-microwave-radio-link:channel-separation": 28000,
       "ietf-microwave-radio-link:rtpc": {
        "maximum-nominal-power": "20.0"
       },
       "ietf-microwave-radio-link:single": {
        "selected-cm": "ietf-microwave-types:qam-512"
       }
      },
      {
       "name": "CT-2",
       "description": "'Carrier Termination 2'",
       "type": "iana-if-type:microwaveCarrierTermination",
       "ietf-microwave-radio-link:tx-frequency": 10615000,
       "ietf-microwave-radio-link:duplex-distance": 113000,
       "ietf-microwave-radio-link:channel-separation": 28000,
       "ietf-microwave-radio-link:rtpc": {
        "maximum-nominal-power": "20.0"
       },
       "ietf-microwave-radio-link:single": {
        "selected-cm": "ietf-microwave-types:qam-512"
       }
      },
      {
       "name": "CT-4",
       "description": "'Carrier Termination 4'",
       "type": "iana-if-type:microwaveCarrierTermination",
       "ietf-microwave-radio-link:tx-frequency": 10415000,
       "ietf-microwave-radio-link:duplex-distance": 113000,
       "ietf-microwave-radio-link:channel-separation": 28000,
       "ietf-microwave-radio-link:rtpc": {
        "maximum-nominal-power": "20.0"
       },
       "ietf-microwave-radio-link:single": {
        "selected-cm": "ietf-microwave-types:qam-512"
       }
      }
     ]
    },
    "ietf-network:networks": {
     "network": [
      {
       "network-id": "L2-network",
       "network-types": {
        "ietf-te-topology:te-topology": {
         "ietf-eth-te-topology:eth-tran-topology": {}
        }
       },
       "supporting-network": [
        {
         "network-ref": "mw-network"
        }
       ],
       "node": [
        {
         "node-id": "L2-N1",
         "supporting-node": [
          {
           "network-ref": "mw-network",
           "node-ref": "mw-N1"
          }
         ],
         "ietf-network-topology:termination-point": [
          {
           "tp-id": "L2-N1-TP1",
           "supporting-termination-point": [
            {
             "network-ref": "mw-network",
             "node-ref": "mw-N1",
             "tp-ref": "mw-N1-RLTP1"
            }
           ]
          }
         ],
         "ietf-te-topology:te-node-id": "192.0.2.1",
         "ietf-te-topology:te": {
          "te-node-attributes": {
           "ietf-eth-te-topology:eth-node": {}
          }
         }
        },
        {
         "node-id": "L2-N2",
         "supporting-node": [
          {
           "network-ref": "mw-network",
           "node-ref": "mw-N2"
          }
         ],
         "ietf-network-topology:termination-point": [
          {
           "tp-id": "L2-N2-TP2",
           "supporting-termination-point": [
            {
             "network-ref": "mw-network",
             "node-ref": "mw-N2",
             "tp-ref": "mw-N2-RLTP2"
            }
           ]
          }
         ],
         "ietf-te-topology:te-node-id": "192.0.2.2",
         "ietf-te-topology:te": {
          "te-node-attributes": {
           "ietf-eth-te-topology:eth-node": {}
          }
         }
        }
       ],
       "ietf-network-topology:link": [
        {
         "link-id": "L2-N1-N2",
         "source": {
          "source-node": "L2-N1",
          "source-tp": "L2-N1-TP1"
         },
         "destination": {
          "dest-node": "L2-N2",
          "dest-tp": "L2-N2-TP2"
         },
         "supporting-link": [
          {
           "network-ref": "mw-network",
           "link-ref": "mwrl-N1-N2"
          }
         ],
         "ietf-te-topology:te": {
          "te-link-attributes": {
           "interface-switching-capability": [
            {
             "switching-capability": "ietf-te-types:switching-l2sc",
             "encoding": "ietf-te-types:lsp-encoding-ethernet"
            }
           ]
          }
         }
        }
       ]
      },
      {
       "network-id": "mw-network",
       "network-types": {
        "ietf-te-topology:te-topology": {
         "ietf-microwave-topology:mw-topology": {}
        }
       },
       "supporting-network": [
        {
         "network-ref": "mw-network"
        }
       ],
       "node": [
        {
         "node-id": "mw-N1",
         "supporting-node": [
          {
           "network-ref": "mw-network",
           "node-ref": "mw-N1"
          }
         ],
         "ietf-network-topology:termination-point": [
          {
           "tp-id": "mw-N1-RLTP1",
           "supporting-termination-point": [
            {
             "network-ref": "mw-network",
             "node-ref": "mw-N1",
             "tp-ref": "mw-N1-CTP1"
            },
            {
             "network-ref": "mw-network",
             "node-ref": "mw-N1",
             "tp-ref": "mw-N1-CTP3"
            }
           ],
           "ietf-te-topology:te-tp-id": "192.0.2.3",
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-rltp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
            "RLT-1"
           }
          },
          {
           "tp-id": "mw-N1-CTP1",
           "ietf-te-topology:te-tp-id": 1,
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-ctp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
            "CT-1"
           }
          },
          {
           "tp-id": "mw-N1-CTP3",
           "ietf-te-topology:te-tp-id": 2,
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-ctp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
            "CT-3"
           }
          }
         ],
         "ietf-te-topology:te-node-id": "192.0.2.1",
         "ietf-te-topology:te": {
          "te-node-attributes": {
           "ietf-microwave-topology:mw-node": {}
          }
         }
        },
        {
         "node-id": "mw-N2",
         "supporting-node": [
          {
           "network-ref": "mw-network",
           "node-ref": "mw-N2"
          }
         ],
         "ietf-network-topology:termination-point": [
          {
           "tp-id": "mw-N2-RLTP2",
           "supporting-termination-point": [
            {
             "network-ref": "mw-network",
             "node-ref": "mw-N2",
             "tp-ref": "mw-N2-CTP2"
            },
            {
             "network-ref": "mw-network",
             "node-ref": "mw-N2",
             "tp-ref": "mw-N2-CTP4"
            }
           ],
           "ietf-te-topology:te-tp-id": "192.0.2.4",
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-rltp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
            "RLT-2"
           }
          },
          {
           "tp-id": "mw-N2-CTP2",
           "ietf-te-topology:te-tp-id": 1,
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-ctp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
            "CT-2"
           }
          },
          {
           "tp-id": "mw-N2-CTP4",
           "ietf-te-topology:te-tp-id": 2,
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-ctp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
            "CT-4"
           }
          }
         ],
         "ietf-te-topology:te-node-id": "192.0.2.1",
         "ietf-te-topology:te": {
          "te-node-attributes": {
           "ietf-microwave-topology:mw-node": {}
          }
         }
        }
       ],
       "ietf-network-topology:link": [
        {
         "link-id": "mwrl-N1-N2",
         "source": {
          "source-node": "mw-N1",
          "source-tp": "mw-N1-RLTP1"
         },
         "destination": {
          "dest-node": "mw-N2",
          "dest-tp": "mw-N2-RLTP2"
         },
         "ietf-te-topology:te": {
          "bundled-links": {
           "bundled-link": [
            {
             "sequence": 1,
             "src-tp-ref": "mw-N1-CTP1",
             "des-tp-ref": "mw-N2-CTP2"
            },
            {
             "sequence": 2,
             "src-tp-ref": "mw-N1-CTP3",
             "des-tp-ref": "mw-N2-CTP4"
            }
           ]
          },
          "te-link-attributes": {
           "ietf-microwave-topology:mw-link": {
            "microwave-radio-link": {
             "rlt-mode": {
              "num-bonded-carriers": 2,
              "num-protecting-carriers": 0
             }
            }
           }
          }
         }
        },
        {
         "link-id": "mwc-N1-N2-A",
         "source": {
          "source-node": "mw-N1",
          "source-tp": "mw-N1-CTP1"
         },
         "destination": {
          "dest-node": "mw-N2",
          "dest-tp": "mw-N2-CTP2"
         },
         "ietf-te-topology:te": {
          "te-link-attributes": {
           "ietf-bandwidth-availability-topology:link-availability": [
            {
             "availability": "0.99",
             "link-bandwidth": "998423"
            },
            {
             "availability": "0.95",
             "link-bandwidth": "1048576"
            }
           ],
           "ietf-microwave-topology:mw-link": {
            "microwave-carrier": {
             "tx-frequency": 10728000,
             "channel-separation": 28000
            }
           }
          }
         }
        },
        {
         "link-id": "mwc-N1-N2-B",
         "source": {
          "source-node": "mw-N1",
          "source-tp": "mw-N1-CTP3"
         },
         "destination": {
          "dest-node": "mw-N2",
          "dest-tp": "mw-N2-CTP4"
         },
         "ietf-te-topology:te": {
          "te-link-attributes": {
           "ietf-microwave-topology:mw-link": {
            "microwave-carrier": {
             "tx-frequency": 10528000,
             "channel-separation": 28000
            }
           }
          }
         }
        }
       ]
      }
     ]
    }
   }

It should say:

   {
    "ietf-interfaces:interfaces": {
     "interface": [
      {
       "name": "L2Interface1",
       "description": "'Ethernet Interface 1'",
       "type": "iana-if-type:ethernetCsmacd"
      },
      {
       "name": "L2Interface2",
       "description": "'Ethernet Interface 2'",
       "type": "iana-if-type:ethernetCsmacd"
      },
      {
       "name": "RLT-1",
       "description": "'Radio Link Terminal 1'",
       "type": "iana-if-type:microwaveRadioLinkTerminal",
       "ietf-microwave-radio-link:mode":
         "ietf-microwave-types:two-plus-zero",
       "ietf-microwave-radio-link:carrier-terminations": [
        "CT-1",
        "CT-3"
       ]
      },
      {
       "name": "RLT-2",
       "description": "'Radio Link Terminal 2'",
       "type": "iana-if-type:microwaveRadioLinkTerminal",
       "ietf-microwave-radio-link:mode":
          "ietf-microwave-types:two-plus-zero",
       "ietf-microwave-radio-link:carrier-terminations": [
        "CT-2",
        "CT-4"
       ]
      },
      {
       "name": "CT-1",
       "description": "'Carrier Termination 1'",
       "type": "iana-if-type:microwaveCarrierTermination",
       "ietf-microwave-radio-link:tx-frequency": 10728000,
       "ietf-microwave-radio-link:duplex-distance": 113000,
       "ietf-microwave-radio-link:channel-separation": 28000,
       "ietf-microwave-radio-link:rtpc": {
        "maximum-nominal-power": "20.0"
       },
       "ietf-microwave-radio-link:single": {
        "selected-cm": "ietf-microwave-types:qam-512"
       }
      },
      {
       "name": "CT-3",
       "description": "'Carrier Termination 3'",
       "type": "iana-if-type:microwaveCarrierTermination",
       "ietf-microwave-radio-link:tx-frequency": 10528000,
       "ietf-microwave-radio-link:duplex-distance": 113000,
       "ietf-microwave-radio-link:channel-separation": 28000,
       "ietf-microwave-radio-link:rtpc": {
        "maximum-nominal-power": "20.0"
       },
       "ietf-microwave-radio-link:single": {
        "selected-cm": "ietf-microwave-types:qam-512"
       }
      },
      {
       "name": "CT-2",
       "description": "'Carrier Termination 2'",
       "type": "iana-if-type:microwaveCarrierTermination",
       "ietf-microwave-radio-link:tx-frequency": 10615000,
       "ietf-microwave-radio-link:duplex-distance": 113000,
       "ietf-microwave-radio-link:channel-separation": 28000,
       "ietf-microwave-radio-link:rtpc": {
        "maximum-nominal-power": "20.0"
       },
       "ietf-microwave-radio-link:single": {
        "selected-cm": "ietf-microwave-types:qam-512"
       }
      },
      {
       "name": "CT-4",
       "description": "'Carrier Termination 4'",
       "type": "iana-if-type:microwaveCarrierTermination",
       "ietf-microwave-radio-link:tx-frequency": 10415000,
       "ietf-microwave-radio-link:duplex-distance": 113000,
       "ietf-microwave-radio-link:channel-separation": 28000,
       "ietf-microwave-radio-link:rtpc": {
        "maximum-nominal-power": "20.0"
       },
       "ietf-microwave-radio-link:single": {
        "selected-cm": "ietf-microwave-types:qam-512"
       }
      }
     ]
    },
    "ietf-network:networks": {
     "network": [
      {
       "network-id": "example:L2-network",
       "network-types": {
        "ietf-te-topology:te-topology": {
         "ietf-eth-te-topology:eth-tran-topology": {}
        }
       },
       "supporting-network": [
        {
         "network-ref": "example:mw-network"
        }
       ],
       "node": [
        {
         "node-id": "example:L2-N1",
         "supporting-node": [
          {
           "network-ref": "example:mw-network",
           "node-ref": "example:mw-N1"
          }
         ],
         "ietf-network-topology:termination-point": [
          {
           "tp-id": "example:L2-N1-TP1",
           "supporting-termination-point": [
            {
             "network-ref": "example:mw-network",
             "node-ref": "example:mw-N1",
             "tp-ref": "example:mw-N1-RLTP1"
            }
           ]
          }
         ],
         "ietf-te-topology:te-node-id": "192.0.2.1",
         "ietf-te-topology:te": {
          "te-node-attributes": {
           "ietf-eth-te-topology:eth-node": {}
          }
         }
        },
        {
         "node-id": "example:L2-N2",
         "supporting-node": [
          {
           "network-ref": "example:mw-network",
           "node-ref": "example:mw-N2"
          }
         ],
         "ietf-network-topology:termination-point": [
          {
           "tp-id": "example:L2-N2-TP2",
           "supporting-termination-point": [
            {
             "network-ref": "example:mw-network",
             "node-ref": "example:mw-N2",
             "tp-ref": "example:mw-N2-RLTP2"
            }
           ]
          }
         ],
         "ietf-te-topology:te-node-id": "192.0.2.2",
         "ietf-te-topology:te": {
          "te-node-attributes": {
           "ietf-eth-te-topology:eth-node": {}
          }
         }
        }
       ],
       "ietf-network-topology:link": [
        {
         "link-id": "example:L2-N1-N2",
         "source": {
          "source-node": "example:L2-N1",
          "source-tp": "example:L2-N1-TP1"
         },
         "destination": {
          "dest-node": "example:L2-N2",
          "dest-tp": "example:L2-N2-TP2"
         },
         "supporting-link": [
          {
           "network-ref": "example:mw-network",
           "link-ref": "example:mwrl-N1-N2"
          }
         ],
         "ietf-te-topology:te": {
          "te-link-attributes": {
           "interface-switching-capability": [
            {
             "switching-capability": "ietf-te-types:switching-l2sc",
             "encoding": "ietf-te-types:lsp-encoding-ethernet"
            }
           ]
          }
         }
        }
       ]
      },
      {
       "network-id": "example:mw-network",
       "network-types": {
        "ietf-te-topology:te-topology": {
         "ietf-microwave-topology:mw-topology": {}
        }
       },
       "supporting-network": [
        {
         "network-ref": "example:mw-network"
        }
       ],
       "node": [
        {
         "node-id": "example:mw-N1",
         "supporting-node": [
          {
           "network-ref": "example:mw-network",
           "node-ref": "example:mw-N1"
          }
         ],
         "ietf-network-topology:termination-point": [
          {
           "tp-id": "example:mw-N1-RLTP1",
           "supporting-termination-point": [
            {
             "network-ref": "example:mw-network",
             "node-ref": "example:mw-N1",
             "tp-ref": "example:mw-N1-CTP1"
            },
            {
             "network-ref": "example:mw-network",
             "node-ref": "example:mw-N1",
             "tp-ref": "example:mw-N1-CTP3"
            }
           ],
           "ietf-te-topology:te-tp-id": "192.0.2.3",
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-rltp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
   	 "RLT-1"
           }
          },
          {
           "tp-id": "example:mw-N1-CTP1",
           "ietf-te-topology:te-tp-id": 1,
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-ctp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
   	 "CT-1"
           }
          },
          {
           "tp-id": "example:mw-N1-CTP3",
           "ietf-te-topology:te-tp-id": 2,
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-ctp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
   	 "CT-3"
           }
          }
         ],
         "ietf-te-topology:te-node-id": "192.0.2.1",
         "ietf-te-topology:te": {
          "te-node-attributes": {
           "ietf-microwave-topology:mw-node": {}
          }
         }
        },
        {
         "node-id": "example:mw-N2",
         "supporting-node": [
          {
           "network-ref": "example:mw-network",
           "node-ref": "example:mw-N2"
          }
         ],
         "ietf-network-topology:termination-point": [
          {
           "tp-id": "example:mw-N2-RLTP2",
           "supporting-termination-point": [
            {
             "network-ref": "example:mw-network",
             "node-ref": "example:mw-N2",
             "tp-ref": "example:mw-N2-CTP2"
            },
            {
             "network-ref": "example:mw-network",
             "node-ref": "example:mw-N2",
             "tp-ref": "example:mw-N2-CTP4"
            }
           ],
           "ietf-te-topology:te-tp-id": "192.0.2.4",
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-rltp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
   	 "RLT-2"
           }
          },
          {
           "tp-id": "example:mw-N2-CTP2",
           "ietf-te-topology:te-tp-id": 1,
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-ctp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
   	 "CT-2"
           }
          },
          {
           "tp-id": "example:mw-N2-CTP4",
           "ietf-te-topology:te-tp-id": 2,
           "ietf-te-topology:te": {
            "ietf-microwave-topology:mw-tp": {
             "microwave-ctp": {}
            },
            "ietf-tp-interface-reference-topology:tp-to-interface-path":
   	 "CT-4"
           }
          }
         ],
         "ietf-te-topology:te-node-id": "192.0.2.1",
         "ietf-te-topology:te": {
          "te-node-attributes": {
           "ietf-microwave-topology:mw-node": {}
          }
         }
        }
       ],
       "ietf-network-topology:link": [
        {
         "link-id": "example:mwrl-N1-N2",
         "source": {
          "source-node": "example:mw-N1",
          "source-tp": "example:mw-N1-RLTP1"
         },
         "destination": {
          "dest-node": "example:mw-N2",
          "dest-tp": "example:mw-N2-RLTP2"
         },
         "ietf-te-topology:te": {
          "bundled-links": {
           "bundled-link": [
            {
             "sequence": 1,
             "src-tp-ref": "example:mw-N1-CTP1",
             "des-tp-ref": "example:mw-N2-CTP2"
            },
            {
             "sequence": 2,
             "src-tp-ref": "example:mw-N1-CTP3",
             "des-tp-ref": "example:mw-N2-CTP4"
            }
           ]
          },
          "te-link-attributes": {
           "ietf-microwave-topology:mw-link": {
            "microwave-radio-link": {
             "rlt-mode": {
              "num-bonded-carriers": 2,
              "num-protecting-carriers": 0
             }
            }
           }
          }
         }
        },
        {
         "link-id": "example:mwc-N1-N2-A",
         "source": {
          "source-node": "example:mw-N1",
          "source-tp": "example:mw-N1-CTP1"
         },
         "destination": {
          "dest-node": "example:mw-N2",
          "dest-tp": "example:mw-N2-CTP2"
         },
         "ietf-te-topology:te": {
          "te-link-attributes": {
           "ietf-bandwidth-availability-topology:link-availability": [
            {
             "availability": "0.99",
             "link-bandwidth": "998423"
            },
            {
             "availability": "0.95",
             "link-bandwidth": "1048576"
            }
           ],
           "ietf-microwave-topology:mw-link": {
            "microwave-carrier": {
             "tx-frequency": 10728000,
             "channel-separation": 28000
            }
           }
          }
         }
        },
        {
         "link-id": "example:mwc-N1-N2-B",
         "source": {
          "source-node": "example:mw-N1",
          "source-tp": "example:mw-N1-CTP3"
         },
         "destination": {
          "dest-node": "example:mw-N2",
          "dest-tp": "example:mw-N2-CTP4"
         },
         "ietf-te-topology:te": {
          "te-link-attributes": {
           "ietf-microwave-topology:mw-link": {
            "microwave-carrier": {
             "tx-frequency": 10528000,
             "channel-separation": 28000
            }
           }
          }
         }
        }
       ]
      }
     ]
    }
   }

Notes:

Fixed URI names to follow RFC8407bis guidelines.

See also https://mailarchive.ietf.org/arch/msg/ccamp/OQ-oLx2smsmdC4dcn6aB9i-hWE8/
```

</details>

<br>**Explanation:**
The example in Annex A.2 uses an inconsistent tx-frequency value (10528000) for the mwc-N1-N2-B link, which should be the same as mwc-N1-N2-A (10728000). This inconsistency affects the understanding and implementation of the example configuration.

---

<details>
<summary><b>Errata 8134</b> from <b>RFC 9656</b> - A YANG Data Model for Microwave Topology (September 2024)</summary>

```
Section B.2 says:


            "node-id": "mw-N1",

It should say:

            "node-id": "example:mw-N1",

Notes:

Fixed URI name to follow RFC8407bis guidelines.

See also https://mailarchive.ietf.org/arch/msg/ccamp/OQ-oLx2smsmdC4dcn6aB9i-hWE8/
```

</details>

<br>**Explanation:**
The original example omits prefixes for network and node identifiers, which is inconsistent with the data model. The correction adds the prefixes, resolving the inconsistency.

---

<details>
<summary><b>Errata 7997</b> from <b>RFC 7344</b> - Automating DNSSEC Delegation Trust Maintenance (September 2014)</summary>

```
Section 6.2.1 says:


When a Parent operates in "calculate DS" mode, it can operate in one
   of two sub-modes:

   full:  The Parent only publishes DS records it calculates from DNSKEY
      records.

It should say:

When a Parent operates in "calculate DS" mode, it can operate in one
   of two sub-modes:

   full:  The Parent only publishes DS records it calculates from CDNSKEY
      records.

Notes:

In the last sentence, "DNSKEY" should be "CDNSKEY".  That is, the Parent calculates DS records from the CDNSKEY records, not from the DNSKEY records.

Paul Wouters (AD): Verifying as the regular AD is an author on the doc :)
```

</details>

<br>**Explanation:**
The erratum points out an incorrect technical detail in Section 6.2.1 of RFC 7344, specifically regarding the record type used for DS record calculation.  The original text states that the Parent calculates DS records from DNSKEY records, while the correction specifies that it should be CDNSKEY records. This is an inconsistency that directly affects the implementation of the specification.

---

<details>
<summary><b>Errata 5395</b> from <b>RFC 7672</b> - SMTP Security via Opportunistic DNS-Based Authentication of Named Entities (DANE) Transport Layer Security (TLS) (October 2015)</summary>

```
Section 2.1.1 says:


   DNS records that would be
   classified "indeterminate" in the sense of [RFC4035] are simply
   classified as "insecure".

It should say:

   DNS records that would be
   classified "indeterminate" in the sense of [RFC4033] are simply
   classified as "insecure".
```

</details>

<br>**Explanation:**
The erratum points out an incorrect reference in Section 2.1.1 of RFC 7672. The original text refers to RFC4035, while the correction points to RFC4033. This is a factual error that directly impacts implementation and understanding of the specification. Therefore, it's classified as INCONSISTENT.

---

<details>
<summary><b>Errata 5150</b> from <b>RFC 8006</b> - Content Delivery Network Interconnection (CDNI) Metadata (December 2016)</summary>

```
Section 6.10 says:


         "generic-metadata-type": "MI.SourceMetadata",
         "generic-metadata-value": {
           "sources": [
             {
               "endpoint": ["acq1.ucdn.example"],
               "protocol": "http/1.1"
             },
             {
               "endpoint": ["acq2.ucdn.example"],
               "protocol": "http/1.1"
             }
           ]
         }


It should say:

         "generic-metadata-type": "MI.SourceMetadata",
         "generic-metadata-value": {
           "sources": [
             {
               "endpoints": ["acq1.ucdn.example"],
               "protocol": "http/1.1"
             },
             {
               "endpoints": ["acq2.ucdn.example"],
               "protocol": "http/1.1"
             }
           ]
         }


Notes:

The SourceMetadata object contains an array of "sources", which in turn contains an array of "endpoints".  The example in section 6.10 uses the singular "endpoint" instead of the plural "endpoints".  The examples in sections 4.2.1 and 4.2.1.1 correctly use the plural "endpoints" for the property name, as defined in section 4.2.1.1.
```

</details>

<br>**Explanation:**
The erratum highlights an inconsistency in the example provided in Section 6.10 of RFC 8006.  The example uses the singular "endpoint" while other sections (4.2.1 and 4.2.1.1) correctly use the plural "endpoints". This inconsistency directly relates to implementation as it affects how the SourceMetadata object should be structured and parsed, causing ambiguity in the implementation.  Therefore, it is classified as INCONSISTENT.

---

<details>
<summary><b>Errata 5049</b> from <b>RFC 8078</b> - Managing DS Records from the Parent via CDS/CDNSKEY (March 2017)</summary>

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

</details>

<br>**Explanation:**
The errata report highlights inconsistencies in the examples of CDS and CDNSKEY records in Section 4 of RFC 8078. The corrections involve changes to the keying material payload representation and base64 encoding, which directly impact the implementation of CDS and CDNSKEY record creation and parsing.  These are not stylistic changes but changes to the specifications' technical requirements, resulting in inconsistencies between the example and proper implementation.  The note about proper base64 encoding and the correct number of digits in the CDS record are critical to interoperability and therefore classify this as an inconsistency.

---

<details>
<summary><b>Errata 4935</b> from <b>RFC 8080</b> - Edwards-Curve Digital Security Algorithm (EdDSA) for DNSSEC (February 2017)</summary>

```
Section 6 says:


6.  Examples

6.1.  Ed25519 Examples

Private-key-format: v1.2
Algorithm: 15 (ED25519)
PrivateKey: ODIyNjAzODQ2MjgwODAxMjI2NDUxOTAyMDQxNDIyNjI=

example.com. 3600 IN DNSKEY 257 3 15 (
             l02Woi0iS8Aa25FQkUd9RMzZHJpBoRQwAQEX1SxZJA4= )

example.com. 3600 IN DS 3613 15 2 (
             3aa5ab37efce57f737fc1627013fee07bdf241bd10f3b1964ab55c78e79
             a304b )

example.com. 3600 IN MX 10 mail.example.com.

example.com. 3600 IN RRSIG MX 3 3600 (
             1440021600 1438207200 3613 example.com. (
             Edk+IB9KNNWg0HAjm7FazXyrd5m3Rk8zNZbvNpAcM+eysqcUOMIjWoevFkj
             H5GaMWeG96GUVZu6ECKOQmemHDg== )



Sury & Edmonds               Standards Track                    [Page 3]

RFC 8080                    EdDSA for DNSSEC               February 2017


Private-key-format: v1.2
Algorithm: 15 (ED25519)
PrivateKey: DSSF3o0s0f+ElWzj9E/Osxw8hLpk55chkmx0LYN5WiY=

example.com. 3600 IN DNSKEY 257 3 15 (
             zPnZ/QwEe7S8C5SPz2OfS5RR40ATk2/rYnE9xHIEijs= )

example.com. 3600 IN DS 35217 15 2 (
             401781b934e392de492ec77ae2e15d70f6575a1c0bc59c5275c04ebe80c
             6614c )

example.com. 3600 IN MX 10 mail.example.com.

example.com. 3600 IN RRSIG MX 3 3600 (
             1440021600 1438207200 35217 example.com. (
             5LL2obmzdqjWI+Xto5eP5adXt/T5tMhasWvwcyW4L3SzfcRawOle9bodhC+
             oip9ayUGjY9T/rL4rN3bOuESGDA== )

6.2.  Ed448 Examples

Private-key-format: v1.2
Algorithm: 16 (ED448)
PrivateKey: xZ+5Cgm463xugtkY5B0Jx6erFTXp13rYegst0qRtNsOYnaVpMx0Z/c5EiA9x
            8wWbDDct/U3FhYWA

example.com. 3600 IN DNSKEY 257 3 16 (
             3kgROaDjrh0H2iuixWBrc8g2EpBBLCdGzHmn+G2MpTPhpj/OiBVHHSfPodx
             1FYYUcJKm1MDpJtIA )

example.com. 3600 IN DS 9713 16 2 (
             6ccf18d5bc5d7fc2fceb1d59d17321402f2aa8d368048db93dd811f5cb2
             b19c7 )

example.com. 3600 IN MX 10 mail.example.com.

example.com. 3600 IN RRSIG MX 3 3600 (
             1440021600 1438207200 9713 example.com. (
             Nmc0rgGKpr3GKYXcB1JmqqS4NYwhmechvJTqVzt3jR+Qy/lSLFoIk1L+9e3
             9GPL+5tVzDPN3f9kAwiu8KCuPPjtl227ayaCZtRKZuJax7n9NuYlZJIusX0
             SOIOKBGzG+yWYtz1/jjbzl5GGkWvREUCUA )











Sury & Edmonds               Standards Track                    [Page 4]

RFC 8080                    EdDSA for DNSSEC               February 2017


Private-key-format: v1.2
Algorithm: 16 (ED448)
PrivateKey: WEykD3ht3MHkU8iH4uVOLz8JLwtRBSqiBoM6fF72+Mrp/u5gjxuB1DV6NnPO
            2BlZdz4hdSTkOdOA

example.com. 3600 IN DNSKEY 257 3 16 (
             kkreGWoccSDmUBGAe7+zsbG6ZAFQp+syPmYUurBRQc3tDjeMCJcVMRDmgcN
             Lp5HlHAMy12VoISsA )

example.com. 3600 IN DS 38353 16 2 (
             645ff078b3568f5852b70cb60e8e696cc77b75bfaaffc118cf79cbda1ba
             28af4 )

example.com. 3600 IN MX 10 mail.example.com.

example.com. 3600 IN RRSIG MX 3 3600 (
             1440021600 1438207200 38353 example.com. (
             +JjANio/LIzp7osmMYE5XD3H/YES8kXs5Vb9H8MjPS8OAGZMD37+LsCIcjg
             5ivt0d4Om/UaqETEAsJjaYe56CEQP5lhRWuD2ivBqE0zfwJTyp4WqvpULbp
             vaukswvv/WNEFxzEYQEIm9+xDlXj4pMAMA )

It should say:

6.  Examples

6.1.  Ed25519 Examples

Private-key-format: v1.2
Algorithm: 15 (ED25519)
PrivateKey: ODIyNjAzODQ2MjgwODAxMjI2NDUxOTAyMDQxNDIyNjI=

example.com. 3600 IN DNSKEY 257 3 15 (
             l02Woi0iS8Aa25FQkUd9RMzZHJpBoRQwAQEX1SxZJA4= )

example.com. 3600 IN DS 3613 15 2 (
             3aa5ab37efce57f737fc1627013fee07bdf241bd10f3b1964ab55c78e79
             a304b )

example.com. 3600 IN MX 10 mail.example.com.

example.com. 3600 IN RRSIG MX 15 2 3600 (
             1440021600 1438207200 3613 example.com. (
             oL9krJun7xfBOIWcGHi7mag5/hdZrKWw15jPGrHpjQeRAvTdszaPD+QLs3f
             x8A4M3e23mRZ9VrbpMngwcrqNAg== )



Sury & Edmonds               Standards Track                    [Page 3]

RFC 8080                    EdDSA for DNSSEC               February 2017


Private-key-format: v1.2
Algorithm: 15 (ED25519)
PrivateKey: DSSF3o0s0f+ElWzj9E/Osxw8hLpk55chkmx0LYN5WiY=

example.com. 3600 IN DNSKEY 257 3 15 (
             zPnZ/QwEe7S8C5SPz2OfS5RR40ATk2/rYnE9xHIEijs= )

example.com. 3600 IN DS 35217 15 2 (
             401781b934e392de492ec77ae2e15d70f6575a1c0bc59c5275c04ebe80c
             6614c )

example.com. 3600 IN MX 10 mail.example.com.

example.com. 3600 IN RRSIG MX 15 2 3600 (
             1440021600 1438207200 35217 example.com. (
             zXQ0bkYgQTEFyfLyi9QoiY6D8ZdYo4wyUhVioYZXFdT410QPRITQSqJSnzQ
             oSm5poJ7gD7AQR0O7KuI5k2pcBg== )

6.2.  Ed448 Examples

Private-key-format: v1.2
Algorithm: 16 (ED448)
PrivateKey: xZ+5Cgm463xugtkY5B0Jx6erFTXp13rYegst0qRtNsOYnaVpMx0Z/c5EiA9x
            8wWbDDct/U3FhYWA

example.com. 3600 IN DNSKEY 257 3 16 (
             3kgROaDjrh0H2iuixWBrc8g2EpBBLCdGzHmn+G2MpTPhpj/OiBVHHSfPodx
             1FYYUcJKm1MDpJtIA )

example.com. 3600 IN DS 9713 16 2 (
             6ccf18d5bc5d7fc2fceb1d59d17321402f2aa8d368048db93dd811f5cb2
             b19c7 )

example.com. 3600 IN MX 10 mail.example.com.

example.com. 3600 IN RRSIG MX 16 2 3600 (
             1440021600 1438207200 9713 example.com. (
             3cPAHkmlnxcDHMyg7vFC34l0blBhuG1qpwLmjInI8w1CMB29FkEAIJUA0am
             xWndkmnBZ6SKiwZSAxGILn/NBtOXft0+Gj7FSvOKxE/07+4RQvE581N3Aj/
             JtIyaiYVdnYtyMWbSNyGEY2213WKsJlwEA )











Sury & Edmonds               Standards Track                    [Page 4]

RFC 8080                    EdDSA for DNSSEC               February 2017


Private-key-format: v1.2
Algorithm: 16 (ED448)
PrivateKey: WEykD3ht3MHkU8iH4uVOLz8JLwtRBSqiBoM6fF72+Mrp/u5gjxuB1DV6NnPO
            2BlZdz4hdSTkOdOA

example.com. 3600 IN DNSKEY 257 3 16 (
             kkreGWoccSDmUBGAe7+zsbG6ZAFQp+syPmYUurBRQc3tDjeMCJcVMRDmgcN
             Lp5HlHAMy12VoISsA )

example.com. 3600 IN DS 38353 16 2 (
             645ff078b3568f5852b70cb60e8e696cc77b75bfaaffc118cf79cbda1ba
             28af4 )

example.com. 3600 IN MX 10 mail.example.com.

example.com. 3600 IN RRSIG MX 16 2 3600 (
             1440021600 1438207200 38353 example.com. (
             E1/oLjSGIbmLny/4fcgM1z4oL6aqo+izT3urCyHyvEp4Sp8Syg1eI+lJ57C
             SnZqjJP41O/9l4m0AsQ4f7qI1gVnML8vWWiyW2KXhT9kuAICUSxv5OWbf81
             Rq7Yu60npabODB0QFPb/rkW3kUZmQ0YQUA )

Notes:

The script used to generate the examples (see https://gitlab.labs.nic.cz/labs/ietf/blob/master/dnskey.py) contains two errors that make the RRSIG records in the example section invalid.
1. The script fails to print the algorithm identifier (15 & 16, TBD1 & TBD2 in earlier drafts) for RRSIGs, and
2. the implementation of label counting includes the root zone as a label, giving an incorrect count of 3 rather than 2.

The first bug is more cosmetic but does result in unparsable RRSIG records, while the second bug causes invalid signatures to be produced.

With these two bugs corrected (and no other changes) the script produces valid examples which are included in the correction above. They have been successfully tested with an independent implementation of RFC 8080 based on https://github.com/miekg/dns & https://godoc.org/golang.org/x/crypto/ed25519 .
```

</details>

<br>**Explanation:**
The erratum identifies two errors in the RRSIG examples within Section 6 of RFC 8080. The first error, omitting the algorithm identifier, results in unparsable RRSIG records.  The second error, an incorrect label count, produces invalid signatures. Both directly impact the implementation and verification of signatures, causing the examples to be unimplementable as presented. This constitutes an inconsistency affecting critical implementation details, therefore it's classified as INCONSISTENT.

---

<details>
<summary><b>Errata 6218</b> from <b>RFC 8777</b> - DNS Reverse IP Automatic Multicast Tunneling (AMT) Discovery (April 2020)</summary>

```
Section 4.3.2 says:


10   IN TYPE260  \# (
       18 ; length
       0a ; precedence=10
       02 ; D=0, relay type=2, an IPv6 address
       20010db800000000000000000000000f ) ; 2001:db8::15
10   IN TYPE260  \# (
       24 ; length
       80 ; precedence=128
       83 ; D=1, relay type=3, a wire-encoded domain name
       09616d7472656c617973076578616d706c6503636f6d ) ; domain name

It should say:

10   IN TYPE260  \# (
       18 ; length
       0a ; precedence=10
       02 ; D=0, relay type=2, an IPv6 address
       20010db8000000000000000000000015 ) ; 2001:db8::15
10   IN TYPE260  \# (
       25 ; length
       80 ; precedence=128
       83 ; D=1, relay type=3, a wire-encoded domain name
       09616d7472656c617973076578616d706c6503636f6d00 ) ; domain name

Notes:

In the first example, the IPv6 address is incorrectly encoded.

In the second example, the trailing root label of the domain name was not included, and should be.  This also increases the length by 1 byte.
```

</details>

<br>**Explanation:**
The erratum points out two errors in the examples in Section 4.3.2 of RFC 8777. The first error is an incorrect encoding of an IPv6 address, and the second error is the omission of a trailing null byte in a domain name encoding.  Both errors are directly related to the correct implementation of the AMT discovery mechanism and will lead to incorrect interpretation of the data, therefore, the classification is INCONSISTENT.

---

<details>
<summary><b>Errata 7883</b> from <b>RFC 9250</b> - DNS over Dedicated QUIC Connections (May 2022)</summary>

```
Section 7.5 says:


Implementations SHOULD use the mechanisms defined in Section 5.4 to
mitigate this attack.

It should say:

Implementations MUST use the padding mechanisms defined in Section 5.4
to mitigate this attack.

Notes:

Section 5.4 states that "[i]mplementations MUST protect against the traffic analysis attacks described in Section 7.5", but Section 7.5 describes that obligation as a "SHOULD". "MUST" is correct, and the inconsistent "SHOULD" in Section 7.5 is an error.

-- Verifier (Eric Vyncke) note --

The short discussion on the DPRIVE WG list has indicated that 2 authors are in favour of verifying this errata.
```

</details>

<br>**Explanation:**
The erratum highlights an inconsistency between sections 5.4 and 7.5 of RFC 9250. Section 5.4 mandates the use of padding mechanisms ("MUST"), while Section 7.5 only recommends it ("SHOULD"). This contradiction creates an inconsistent requirement, directly affecting implementation.  The correction ensures consistent and mandatory implementation of the security measure, resolving the inconsistency. Therefore it is classified as INCONSISTENT.

---

<details>
<summary><b>Errata 7804</b> from <b>RFC 9463</b> - DHCP and Router Advertisement Options for the Discovery of Network-designated Resolvers (DNR) (November 2023)</summary>

```
Section 6.1 says:


Note that the "Addr Length", "ipv6-address(es)", and "Service 
Parameters (SvcParams)" fields are not present if the ADN-only mode 
is used (Section 3.1.6).

It should say:

Note that the "Addr Length", "ipv6-address(es)", "SvcParams 
Length", and "Service Parameters (SvcParams)" fields are not 
present if the ADN-only mode is used (Section 3.1.6).

Notes:

The paragraph is presumably copied from section 4.1 (DHCPv6 Encrypted DNS Option), and omits the "SvcParams Length" field, which is only present in the IPv6 RA Encrypted DNS Option. Mandating the presence of a superfluous length field when using the ADN-only mode seems like an oversight.
```

</details>

<br>**Explanation:**
The erratum points out an omission in Section 6.1 of RFC 9463.  The original text incorrectly states that only "Addr Length", "ipv6-address(es)", and "Service Parameters (SvcParams)" fields are absent in ADN-only mode. The correction adds "SvcParams Length", which is a necessary field.  This omission creates an inconsistency between the description in Section 6.1 and the actual specification of the ADN-only mode, directly impacting implementation.

---

<details>
<summary><b>Errata 4169</b> from <b>RFC 7230</b> - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing (June 2014)</summary>

```
Section 7 says:


     #element => [ ( "," / element ) *( OWS "," [ OWS element ] ) ]

     1#element => *( "," OWS ) element *( OWS "," [ OWS element ] )

   Empty elements do not contribute to the count of elements present.
   For example, given these ABNF productions:

     example-list      = 1#example-list-elmt
     example-list-elmt = token ; see Section 3.2.6

   Then the following are valid values for example-list (not including
   the double quotes, which are present for delimitation only):

     "foo,bar"
     "foo ,bar,"
     "foo , ,bar,charlie   "

It should say:

     #element => [ ( "," / element ) *( OWS "," [ OWS element ] ) ]

     1#element => *( "," OWS ) element *( OWS "," [ OWS element ] )

   Empty elements do not contribute to the count of elements present.
   For example, given these ABNF productions:

     example-list      = 1#example-list-elmt
     example-list-elmt = token ; see Section 3.2.6

   Then the following are valid values for example-list (not including
   the double quotes, which are present for delimitation only):

     "foo,bar"
     "foo ,bar,"
     "foo , ,bar,charlie"

Notes:

"foo , ,bar,charlie   " cannot be derived from 1#token (legacy list rule)
"foo , ,bar,charlie" can be derived from 1#token (legacy list rule)
```

</details>

<br>**Explanation:**
The errata report points out an inconsistency in the ABNF rules provided in Section 7 of RFC 7230.  The original specification allows for trailing whitespace in a way that is not consistent with how 1#element is defined, which affects the implementation of HTTP message parsing. The correction clarifies the valid values for the example-list, directly impacting how applications should parse and handle lists of elements in HTTP messages.  This is a technical error affecting the implementation of the specification.

---

<details>
<summary><b>Errata 4251</b> from <b>RFC 7230</b> - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing (June 2014)</summary>

```
Section 2.7.1 says:


     http-URI = "http:" "//" authority path-abempty [ "?" query ]
                [ "#" fragment ]


It should say:

     http-URI = "http:" "//" authority path-abempty [ "?" query ]


Notes:

Per http://tools.ietf.org/html/rfc3986#section-4.3 "URI scheme specifications must define their own syntax so that all strings matching their scheme-specific syntax will also match the <absolute-URI> grammar." See the discussion around http://mailarchive.ietf.org/arch/msg/apps-discuss/gZVRtgOUFyzOk68FgL1jHTzWG2s
```

</details>

<br>**Explanation:**
The erratum points out that the original definition of `http-URI` in Section 2.7.1 of RFC 7230 is inconsistent with RFC 3986.  The inclusion of the optional fragment identifier is incorrect according to RFC 3986's requirements for URI scheme specifications.  This inconsistency directly affects the implementation of HTTP clients and servers that need to parse and generate HTTP URIs correctly, potentially causing interoperability problems.

---

<details>
<summary><b>Errata 4252</b> from <b>RFC 7230</b> - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing (June 2014)</summary>

```
Section 2.7.2. says:


     https-URI = "https:" "//" authority path-abempty [ "?" query ]
                 [ "#" fragment ]


It should say:

     https-URI = "https:" "//" authority path-abempty [ "?" query ]


Notes:

See erratum 4251 on the same document.
```

</details>

<br>**Explanation:**
This erratum, referencing erratum 4251, highlights an inconsistency similar to erratum 4250.  The inclusion of the optional fragment identifier in the definition of `https-URI` in Section 2.7.2 contradicts RFC 3986.  This affects the correct implementation of HTTPS URI parsing and generation, potentially leading to interoperability issues.  The correction ensures consistency with the URI syntax defined in RFC 3986.

---

<details>
<summary><b>Errata 4667</b> from <b>RFC 7230</b> - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing (June 2014)</summary>

```
Section 4.1.1 says:


chunk-ext      = *( ";" chunk-ext-name [ "=" chunk-ext-val ] )


It should say:

chunk-ext      = *( BWS  ";" BWS chunk-ext-name
                    [ BWS  "=" BWS chunk-ext-val ] )


Notes:

The infamous "implicit *LWS" syntax rule in RFC 2616 allowed whitespace between
";" and chunk-ext-name in chunk-ext. Some HTTP agents generate that whitespace.
In my experience, HTTP agents that can parse chunk extensions usually can handle
that whitespace. Moreover, ICAP, which generally relies on HTTP/1 for its message
syntax, uses that whitespace when defining the "ieof" chunk extension in RFC 3507
Section 4.5:

\r\n
0; ieof\r\n\r\n

IMHO, RFC 7230 should either allow BWS before chunk-ext-name or at the very least
explicitly document the HTTP/1 syntax change and its effect on parsers used for both
ICAP and HTTP/1 messages (a very common case for ICAP-supporting HTTP
intermediaries and ICAP services).

I also recommend adding BWS around "=", for consistency and RFC 2616 backward
compatibility reasons. HTTPbis RFCs already do that for transfer-parameter and
auth-param that have similar syntax.

Please also consider adding BWS _before_ ";" for consistency and RFC 2616 backward
compatibility reasons. HTTPbis RFCs already do that for transfer-extension,
accept-ext, t-ranking, and other constructs with similar syntax.
```

</details>

<br>**Explanation:**
The erratum points to an inconsistency between RFC 7230's definition of `chunk-ext` and the actual practices and implementations observed in HTTP agents and ICAP.  The original specification's lack of allowance for whitespace around semicolons and the equals sign is inconsistent with the common practice and RFC 2616's implicit allowance for whitespace.  This inconsistency creates interoperability issues because HTTP agents might generate whitespace in a way that RFC 7230 does not permit, while parsers adhering strictly to RFC 7230 might fail to parse valid HTTP messages. The proposed correction improves consistency and interoperability with older systems.

---

<details>
<summary><b>Errata 4825</b> from <b>RFC 7230</b> - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing (June 2014)</summary>

```
Section Appendix B says:


chunk-ext      = *( ";" chunk-ext-name [ "=" chunk-ext-val ] )


It should say:

chunk-ext      = *( BWS  ";" BWS chunk-ext-name
                    [ BWS  "=" BWS chunk-ext-val ] )

Notes:

The infamous "implicit *LWS" syntax rule in RFC 2616 allowed whitespace between
";" and chunk-ext-name in chunk-ext. Some HTTP agents generate that whitespace.
In my experience, HTTP agents that can parse chunk extensions usually can handle
that whitespace. Moreover, ICAP, which generally relies on HTTP/1 for its message
syntax, uses that whitespace when defining the "ieof" chunk extension in RFC 3507
Section 4.5:

      \r\n
      0; ieof\r\n\r\n

IMHO, RFC 7230 should either allow BWS before chunk-ext-name or at the very least
explicitly document the HTTP/1 syntax change and its effect on parsers used for both
ICAP and HTTP/1 messages (a very common case for ICAP-supporting HTTP
intermediaries and ICAP services).

I also recommend adding BWS around "=", for consistency and RFC 2616 backward
compatibility reasons. HTTPbis RFCs already do that for transfer-parameter and
auth-param that have similar syntax.

Please also consider adding BWS _before_ ";" for consistency and RFC 2616 backward
compatibility reasons. HTTPbis RFCs already do that for transfer-extension,
accept-ext,  t-ranking, and other constructs with similar syntax.
```

</details>

<br>**Explanation:**
The erratum highlights an inconsistency between the ABNF rule for `chunk-ext` in Appendix B of RFC 7230 and the actual practices observed in HTTP and ICAP implementations. The original specification does not allow whitespace around semicolons and equals signs within `chunk-ext`, while some HTTP agents generate and parse such whitespace, and RFC 2616 implicitly allowed this.  This inconsistency affects interoperability. The proposed change to include optional whitespace improves compatibility with existing implementations and clarifies the specification, addressing a conflict between the RFC and practical implementations.

---

<details>
<summary><b>Errata 4839</b> from <b>RFC 7230</b> - Hypertext Transfer Protocol (HTTP/1.1): Message Syntax and Routing (June 2014)</summary>

```
Section 4 says:


   Parameters are in the form of a name or name=value pair.

     transfer-parameter = token BWS "=" BWS ( token / quoted-string )

It should say:

   Parameters are in the form of a name=value pair.

     transfer-parameter = token BWS "=" BWS ( token / quoted-string )

Notes:

The ABNF does not allow the form of a name.
```

</details>

<br>**Explanation:**
The errata highlights a contradiction. The text states that parameters can be in the form of a name or name=value pair, but the ABNF only allows the name=value pair form. This inconsistency affects how implementations will parse and handle parameters, making it unclear whether a parameter should always have a value or if a name-only parameter is valid.

---

<details>
<summary><b>Errata 4664</b> from <b>RFC 7233</b> - Hypertext Transfer Protocol (HTTP/1.1): Range Requests (June 2014)</summary>

```
Section 4.4 says:


The 416 (Range Not Satisfiable) status code indicates that none of
the ranges in the request's Range header field (Section 3.1) overlap
the current extent of the selected resource or that the set of ranges
requested has been rejected due to invalid ranges or an excessive
request of small or overlapping ranges.

It should say:

The 416 (Range Not Satisfiable) status code indicates that none of
the ranges in the request's Range header field (Section 3.1) overlap
the current extent of the selected representation or that the set of
ranges requested has been rejected due to invalid ranges or an excessive
request of small or overlapping ranges.

Notes:

The overlap may depend on the representation, not only the resource, as is the case with byte ranges.
```

</details>

<br>**Explanation:**
The erratum points out that using the term "resource" in Section 4.4 is inconsistent with the concept of representations.  The 416 status code's applicability depends on the representation's extent, not solely on the resource's extent.  This is particularly relevant for byte ranges, which are representation-specific.  The inconsistency affects how servers implement the 416 response, potentially causing incorrect responses in cases where multiple representations exist for the same resource.

---

<details>
<summary><b>Errata 5474</b> from <b>RFC 7233</b> - Hypertext Transfer Protocol (HTTP/1.1): Range Requests (June 2014)</summary>

```
Section 4.4. says:


For byte ranges, failing to overlap the current extent means that the
   first-byte-pos of all of the byte-range-spec values were greater than
   the current length of the selected representation.

It should say:

For byte ranges, failing to overlap the current extent means that the
   first-byte-pos of all of the byte-range-spec values were greater than
   or equal to the current length of the selected representation.
   ^^^^^^^^^^^

Notes:

If the length of the representation is 500 bytes, then the range of the entire representation is 0-499. Then a range starting at byte position 500 fails to overlap the representation.
```

</details>

<br>**Explanation:**
The erratum points out an inconsistency in the description of byte range overlap in Section 4.4. The original description incorrectly states that only ranges with `first-byte-pos` values strictly greater than the representation length fail to overlap.  A range starting exactly at the length should also be considered non-overlapping. This error directly impacts the implementation of range request handling, potentially causing servers to incorrectly accept or reject valid or invalid ranges.

---

<details>
<summary><b>Errata 4132</b> from <b>RFC 7386</b> - JSON Merge Patch (October 2014)</summary>

```
Section 2 says:


define MergePatch(Target, Patch):
       if Patch is an Object:
         if Target is not an Object:
       Target = {} # Ignore the contents and set it to an empty Object
         for each Name/Value pair in Patch:
       if Value is null:
         if Name exists in Target:
           remove the Name/Value pair from Target
       else:
         Target[Name] = MergePatch(Target[Name], Value)
         return Target
       else:
         return Patch

It should say:

   define MergePatch(Target, Patch):
     if Patch is an Object:
       if Target is not an Object:
         Target = {} # Ignore the contents and set it to an empty Object
       for each Name/Value pair in Patch:
         if Value is null:
           if Name exists in Target:
             remove the Name/Value pair from Target
         else:
           Target[Name] = MergePatch(Target[Name], Value)
       return Target
     else:
       return Patch

Notes:

Indentation of the pseudo-code example was correct in the Internet-Drafts but was messed up in the final version. For instance, "Target = {}" should be under the two ifs. (Reported by James H. Manger on the appsawg mailing list.)

This is a technical erratum, rather than editorial, because the correct indentation is essential to understanding the pseudocode.
```

</details>

<br>**Explanation:**
The incorrect indentation in the pseudocode example of Section 2 changes the algorithm's logic. The original, incorrectly indented code does not correctly implement the intended merge operation.  The erroneous indentation affects the interpretation of the conditional statements, leading to an incorrect merge algorithm and thus impacting the implementation of JSON Merge Patch.  The correction ensures that the pseudocode accurately reflects the intended behavior, resolving the inconsistency.

---

<details>
<summary><b>Errata 6178</b> from <b>RFC 7807</b> - Problem Details for HTTP APIs (March 2016)</summary>

```
Section 3 says:


   The ability to convey problem-specific extensions allows more than
   one problem to be conveyed.  For example:

   HTTP/1.1 400 Bad Request
   Content-Type: application/problem+json
   Content-Language: en

   {
   "type": "https://example.net/validation-error",
   "title": "Your request parameters didn't validate.",
   "invalid-params": [ {
                         "name": "age",
                         "reason": "must be a positive integer"
                       },
                       {
                         "name": "color",
                         "reason": "must be 'green', 'red' or 'blue'"}
                     ]
   }


It should say:

   The ability to convey problem-specific extensions allows more than
   one problem to be conveyed.  For example:

   HTTP/1.1 400 Bad Request
   Content-Type: application/problem+json
   Content-Language: en

   {
   "type": "https://example.net/validation-error",
   "title": "Your request parameters didn't validate.",
   "invalid_params": [ {
                         "name": "age",
                         "reason": "must be a positive integer"
                       },
                       {
                         "name": "color",
                         "reason": "must be 'green', 'red' or 'blue'"}
                     ]
   }


Notes:

The "invalid-params" member in the example is named incorrectly. According to Section 4, it should contain an "_" rather than a "-" in its name:

>   If such additional members are defined, their names SHOULD start with
>   a letter (ALPHA, as per [RFC5234], Appendix B.1) and SHOULD consist
>   of characters from ALPHA, DIGIT ([RFC5234], Appendix B.1), and "_"
>   (so that it can be serialized in formats other than JSON), and they
>   SHOULD be three characters or longer.
```

</details>

<br>**Explanation:**
The example in Section 3 uses the member name "invalid-params", which is inconsistent with the naming guidelines specified in Section 4.  Section 4 recommends using underscores instead of hyphens in member names for better interoperability and serialization in various formats. This inconsistency affects the interoperability and correctness of problem details implementations. The corrected example uses "invalid_params", which adheres to the guidelines in Section 4.

---

<details>
<summary><b>Errata 5255</b> from <b>RFC 8040</b> - RESTCONF Protocol (January 2017)</summary>

```
Section 3.5.3. says:


If there are multiple key leaf values, the path 
segment is constructed by having the list name, 
followed by the value of each leaf identified 
in the "key" statement, encoded in the order
specified in the YANG "key" statement.  Each key 
leaf value except the last one is followed by 
a comma character.

It should say:

If there are multiple key leaf values, the path 
segment is constructed by having the list name,  
followed by an "=" character, 
followed by the value of each leaf identified 
in the "key" statement, encoded in the order
specified in the YANG "key" statement.  Each key 
leaf value except the last one is followed by 
a comma character.

Notes:

When describing the encoding of key values for a list, in the case of multiple keys the "=" equal sign is not mentioned although it is used in the examples.
```

</details>

<br>**Explanation:**
The description of key value encoding in Section 3.5.3 is inconsistent with the examples provided. The description omits the '=' character used to separate the key name and its value in the path segment, while the examples correctly include it. This inconsistency could lead to incorrect implementation of key value encoding in RESTCONF clients and servers.

---

<details>
<summary><b>Errata 5566</b> from <b>RFC 8040</b> - RESTCONF Protocol (January 2017)</summary>

```
Section B.3.2 says:


          "player" : {
            "gap" : 0.5
          }


It should say:

          "player" : {
            "gap" : "0.5"
          }


Notes:

The quoted text occurs twice; p 128 and p 130.

The leaf "gap" is defined as type decimal64 in A.1.  According to RFC 7951, section 6.1, a decimal64 type is represented as a string in JSON.
```

</details>

<br>**Explanation:**
The example in Section B.3.2 incorrectly represents the "gap" leaf, which is defined as type decimal64, as a numerical value instead of a string.  This contradicts RFC 7951, section 6.1, that specifies decimal64 values should be represented as strings in JSON.  This inconsistency affects the correct implementation of JSON serialization for decimal64 types. Therefore it is classified as INCONSISTENT.

---

<details>
<summary><b>Errata 5756</b> from <b>RFC 8040</b> - RESTCONF Protocol (January 2017)</summary>

```
Section 8 says:


  module ietf-system {
    leaf system-reset {
      type empty;
    }
  }


It should say:

  module ietf-system {
    leaf system-restart {
      type empty;
    }
  }


Notes:

The section on page 84 discusses the "system-restart" RPC from RFC 7317, but the conceptual example has "system-reset".  Fix: s/system-reset/system-restart/.
```

</details>

<br>**Explanation:**
The example YANG module in Section 8 uses the name "system-reset" for an RPC operation, which is inconsistent with the name "system-restart" discussed and referenced earlier in the RFC from RFC 7317.  This inconsistency could lead to confusion and incorrect implementation of the system restart functionality.

---

<details>
<summary><b>Errata 6473</b> from <b>RFC 8040</b> - RESTCONF Protocol (January 2017)</summary>

```
Section B.3.2 says:


   Example 3: depth=3

   To limit the depth level to the target resource plus two child
   resource layers, the value "3" is used.

      GET /restconf/data/example-jukebox:jukebox?depth=3 HTTP/1.1
      Host: example.com
      Accept: application/yang-data+json

   The server might respond as follows:

      HTTP/1.1 200 OK
      Date: Thu, 26 Jan 2017 20:56:30 GMT
      Server: example-server
      Cache-Control: no-cache
      Content-Type: application/yang-data+json

      {
        "example-jukebox:jukebox" : {
          "library" : {
            "artist" : {}
          },
          "playlist" : [
            {
              "name" : "Foo-One",
              "description" : "example playlist 1",
              "song" : {}
            }
          ],
          "player" : {
            "gap" : 0.5
          }
        }
      }

It should say:

   Example 3: depth=3

   To limit the depth level to the target resource plus two child
   resource layers, the value "3" is used.

      GET /restconf/data/example-jukebox:jukebox?depth=3 HTTP/1.1
      Host: example.com
      Accept: application/yang-data+json

   The server might respond as follows:

      HTTP/1.1 200 OK
      Date: Thu, 26 Jan 2017 20:56:30 GMT
      Server: example-server
      Cache-Control: no-cache
      Content-Type: application/yang-data+json

      {
        "example-jukebox:jukebox" : {
          "library" : {
            "artist" : []
          },
          "playlist" : [
            {
              "name" : "Foo-One",
              "description" : "example playlist 1",
              "song" : []
            }
          ],
          "player" : {
            "gap" : 0.5
          }
        }
      }

Notes:

"artist" and "song" are defined as list.  Therefore, according to RFC 7951, they should be encoded as array instead of object.
```

</details>

<br>**Explanation:**
The response example in Section B.3.2 incorrectly represents "artist" and "song" as empty objects when they should be empty arrays according to RFC 7951, given that they are defined as lists in the YANG model.  This inconsistency misrepresents how list types should be encoded in JSON responses, potentially causing incorrect implementation of RESTCONF data serialization and deserialization.

---

<details>
<summary><b>Errata 5729</b> from <b>RFC 8555</b> - Automatic Certificate Management Environment (ACME) (March 2019)</summary>

```
Section 7.5.1 says:


The client indicates to the server that it is ready for the challenge
validation by sending an empty JSON body ("{}") carried in a POST
request to the challenge URL (not the authorization URL).

It should say:

The client indicates to the server that it is ready for the challenge
validation by sending a POST request to the challenge URL (not the
authorization URL), where the body of the POST request is a JWS object
whose JSON payload is a response object (see Section 8).  For all
challenge types defined in this document, the response object is the
empty JSON object ("{}").

Notes:

It's clear from other text in section 7.5.1 that the "empty JSON body" is interpreted by the ACME server as a "response object".  (The first function of this erratum is to clarify this point).

Section 8 says that "The definition of a challenge type includes...Contents of response objects", and section 7.5.1 notes that "the challenges in this document do not define any response fields, but future specifications might define them".  (The second function of this erratum is to permit clients to send response objects that contain response fields).
```

</details>

<br>**Explanation:**
The description of the challenge validation process in Section 7.5.1 is inconsistent with the requirement for a JWS-signed response object as defined in Section 8.  The original text incorrectly describes the request body as simply an empty JSON object, while the full specification requires it to be a JWS object containing an empty JSON object. This inconsistency affects client implementation which must correctly construct and sign the JWS object for challenge validation.

---

<details>
<summary><b>Errata 5732</b> from <b>RFC 8555</b> - Automatic Certificate Management Environment (ACME) (March 2019)</summary>

```
Section 8 says:


A challenge object with an error MUST have status
equal to "invalid".

It should say:

A challenge object with an error MUST have status
equal to "processing" or "invalid".

Notes:

Section 8.2 says that 'The server MUST add an entry to the "error" field in the challenge after each failed validation query'.  However, if the challenge must then become "invalid", it is never possible to retry any validation query (because "invalid" is a final state for a challenge object).
This erratum is necessary to permit validation query retries to ever happen.
```

</details>

<br>**Explanation:**
The statement in Section 8 that a challenge object with an error MUST have status equal to "invalid" is inconsistent with the retry mechanism described in Section 8.2.  Section 8.2 indicates that failed validation attempts add an error to the challenge object, but the "invalid" status prevents retries.  The corrected statement allows for the "processing" status, enabling retry attempts before the challenge becomes definitively "invalid", thus resolving the inconsistency.

---

<details>
<summary><b>Errata 5983</b> from <b>RFC 8555</b> - Automatic Certificate Management Environment (ACME) (March 2019)</summary>

```
Section 9.1 says:


   A file of this type contains one or more certificates encoded with
   the PEM textual encoding, according to [RFC7468].  The textual
   encoding of certificates in this file MUST use the strict encoding
   and MUST NOT include explanatory text.  The ABNF for this format is
   as follows, where "stricttextualmsg" and "eol" are as defined in
   Section 3 of RFC 7468:

   certchain = stricttextualmsg *(eol stricttextualmsg)

It should say:

   A file of this type contains one or more certificates encoded with
   the PEM textual encoding, according to [RFC7468].  The textual
   encoding of certificates in this file MUST use the strict encoding
   and MUST NOT include explanatory text.  The ABNF for this format is
   as follows, where "stricttextualmsg" is as defined in
   Section 3 of RFC 7468:

   certchain = stricttextualmsg *(stricttextualmsg)

Notes:

Examples within RFC 8555 indicate that only one EOL should be present between entries in the PEM chain.

RFC 7468 already defines a stricttextualmsg as ending with EOL
stricttextualmsg = preeb eol
                           strictbase64text
                           posteb eol

If a second EOL is to be added before each strict textual message this would result in a blank line between entries.  The prior example in https://tools.ietf.org/html/rfc8555#section-7.4.2 indicates an intention for only one EOL marker to be used:
   -----BEGIN CERTIFICATE-----
   [End-entity certificate contents]
   -----END CERTIFICATE-----
   -----BEGIN CERTIFICATE-----
   [Issuer certificate contents]
   -----END CERTIFICATE-----
   -----BEGIN CERTIFICATE-----
   [Other certificate contents]
   -----END CERTIFICATE-----
```

</details>

<br>**Explanation:**
The ABNF in Section 9.1 is inconsistent with the examples provided in the RFC and the definition of `stricttextualmsg` in RFC 7468. The ABNF implies multiple EOL characters between certificates, while the examples and the definition of `stricttextualmsg` suggest only one EOL character. This inconsistency affects the correct interpretation and implementation of the certificate chain format and is therefore classified as INCONSISTENT.

---

<details>
<summary><b>Errata 6364</b> from <b>RFC 8555</b> - Automatic Certificate Management Environment (ACME) (March 2019)</summary>

```
Section 7.1.4 says:


   wildcard (optional, boolean):  This field MUST be present and true
      for authorizations created as a result of a newOrder request
      containing a DNS identifier with a value that was a wildcard
      domain name.  For other authorizations, it MUST be absent.
      Wildcard domain names are described in Section 7.1.3.

It should say:

   wildcard (optional, boolean):  This field MUST be present and true
      for authorizations created as a result of a newOrder request
      containing a DNS identifier with a value that was a wildcard
      domain name.  For other authorizations, it MUST be absent or
      false.  For pre-authorizations, it MUST be absent or false.
      Wildcard domain names are described in Section 7.1.3.

Notes:

This section states that the wildcard field must be absent for other authorizations, but the example in this section has an explicitly set wildcard field with value false. The proposed change allows both options, either omitting it or explicitly setting it to false. Also a sentence has been added to explicitly describe the behavior for pre-authorizations.
```

</details>

<br>**Explanation:**
The description of the `wildcard` field states it MUST be absent for non-wildcard authorizations, while the example shows it explicitly set to `false`. This creates an inconsistency, making it unclear whether omitting the field or setting it to `false` is the correct approach for non-wildcard authorizations. The proposed change clarifies this, allowing both approaches for non-wildcard and pre-authorizations.

---

<details>
<summary><b>Errata 7565</b> from <b>RFC 8555</b> - Automatic Certificate Management Environment (ACME) (March 2019)</summary>

```
Section 8.1 says:


 The "Thumbprint" step indicates the computation specified in
   [RFC7638], using the SHA-256 digest [FIPS180-4].  As noted in
   [RFC7518] any prepended zero octets in the fields of a JWK object
   MUST be stripped before doing the computation.

It should say:

The "Thumbprint" step indicates the computation specified in
   [RFC7638], using the SHA-256 digest [FIPS180-4].  As noted in
   [RFC7518] any additional prepended zero octets in the fields of a JWK object
   MUST be stripped before doing the computation.  
   Fixed length fields such as found in ECDSA keys should be their natural length and 
   leading zero octets should not be stripped.

Notes:

This comment was really aimed at the leading 0 octet sometimes used with RSA, but the comment is not RSA specific. ECDSA keys can have fixed length fields (X,Y) where there can be leading zeros.  This led me astray in implementing an ECDSA thumbprint routine for ACME. The result was that 1/128 ECDSA keys failed to generate t humbp[rint as leading zeros were removed.
```

</details>

<br>**Explanation:**
The description in Section 8.1 regarding zero octet stripping before thumbprint computation is unclear and inconsistent when applied to ECDSA keys with fixed-length fields.  The original text implies that all leading zero octets should be stripped, but this is incorrect for ECDSA, leading to incorrect thumbprint calculation. This inconsistency directly impacts the correct implementation of the thumbprint calculation for ECDSA keys and is therefore classified as INCONSISTENT.

---

<details>
<summary><b>Errata 7138</b> from <b>RFC 9110 a.k.a. STD 97</b> - HTTP Semantics (June 2022)</summary>

```
Section 12.5.1 says:


The media type quality factor associated with a given type is 
determined by finding the media range with the highest precedence 
that matches the type. For example,

Accept: text/*;q=0.3, text/plain;q=0.7, text/plain;format=flowed,
       text/plain;format=fixed;q=0.4, */*;q=0.5

would cause the following values to be associated:

Table 5: 

Media Type	                Quality Value
text/plain;format=flowed	      1
text/plain	                     0.7
text/html	                     0.3
image/jpeg	                     0.5
text/plain;format=fixed	             0.4
text/html;level=3	             0.7

It should say:

The media type quality factor associated with a given type is 
determined by finding the media range with the highest precedence 
that matches the type. For example,

Accept: text/*;q=0.3, text/plain;q=0.7, text/plain;format=flowed,
       text/plain;format=fixed;q=0.4, */*;q=0.5

would cause the following values to be associated:

Table 5: 

Media Type	                Quality Value
text/plain;format=flowed	      1
text/plain	                     0.7
text/html	                     0.3
image/jpeg	                     0.5
text/plain;format=fixed	             0.4
text/html;level=3	             0.3

Notes:

To illustrate how the media type quality factor associated with a given type is determined, the following example is given: 

Accept: text/*;q=0.3, text/plain;q=0.7, text/plain;format=flowed, text/plain;format=fixed;q=0.4, */*;q=0.5

The last row of the result table (table 5) presenting the values to be associated cannot be deduced (MediaType: text/html;level=3, Quality Value: 0.7), since only "text/*;q=0.3" and "*/*;q=0.5" are possible values and as explained in the RFC "text/*;q=0.3" should take precedence. 

In section 5.3.2 of RFC7231, a similar example is given, where the last row of the table is correct (text/html;level=3 | 0.7) since in that example the accept header contains (text/html;q=0.7).
```

</details>

<br>**Explanation:**
The example in Section 12.5.1 shows an incorrect quality value for the media type "text/html;level=3".  The provided value of 0.7 cannot be derived from the given Accept header using the precedence rules described in the RFC.  This inconsistency between the example and the described algorithm makes the specification unclear and impacts its correct implementation. Therefore, it is classified as INCONSISTENT.

---

<details>
<summary><b>Errata 7306</b> from <b>RFC 9110 a.k.a. STD 97</b> - HTTP Semantics (June 2022)</summary>

```
Section 14.1.1 says:


  ranges-specifier = range-unit "=" range-set
  range-set        = 1#range-spec
  range-spec       = int-range
                   / suffix-range
                   / other-range

It should say:

  ranges-specifier = range-unit "=" OWS range-set
  range-set        = 1#range-spec
  range-spec       = int-range
                   / suffix-range
                   / other-range

Notes:

The ABNF is inconsistent with one of the examples given in 14.1.2

   bytes= 0-999, 4500-5499, -1000

The bug in the ABNF was likely introduced when converting away from "implied linear whitespace".

See also <https://github.com/whatwg/fetch/issues/1070#issuecomment-1361800123>.
```

</details>

<br>**Explanation:**
The ABNF for ranges-specifier in Section 14.1.1 is inconsistent with the example provided in Section 14.1.2.  The example shows optional whitespace between the "=" and the range-set, which is not reflected in the ABNF. This inconsistency makes the ABNF less permissive than the actual usage shown in the examples, potentially causing issues for implementations that strictly adhere to the original ABNF.

---

<details>
<summary><b>Errata 7419</b> from <b>RFC 9110 a.k.a. STD 97</b> - HTTP Semantics (June 2022)</summary>

```
Section 8.3.2 says:


   In the fields defined by this document, charset names appear either
   in parameters (Content-Type), or, for Accept-Encoding, in the form of
   a plain token.

It should say:

   In the fields defined by this document, charset names appear either
   in parameters (Content-Type), or, for Accept-Charset, in the form of
   a plain token.

Notes:

Accept-Encoding is the preferred list of response content codings.  Accept-Charset is the preferred list of response charsets.
```

</details>

<br>**Explanation:**
The text in Section 8.3.2 incorrectly mentions "Accept-Encoding" when it should refer to "Accept-Charset". This inconsistency creates confusion, as "Accept-Encoding" is for content codings, not character sets.  This directly affects the correct interpretation of how charset names are used, leading to potential implementation errors.  Therefore, it is classified as INCONSISTENT.

---

<details>
<summary><b>Errata 7014</b> from <b>RFC 9114</b> - HTTP/3 (June 2022)</summary>

```
Section 4.3.1 says:


   ":path":  Contains the path and query parts of the target URI (the
      "path-absolute" production and optionally a ? character (ASCII
      0x3f) followed by the "query" production; see Sections 3.3 and 3.4
      of [URI].

It should say:

   ":path":  Contains the path and query parts of the target URI (the
      "absolute-path" production and optionally a ? character (ASCII
      0x3f) followed by the "query" production; see Section 4.1 of
      [HTTP] and Section 3.4 of [URI].

Notes:

There is a conflict between RFC 9114 and RFCs 9110,9112,9113. RFC 9114 disallows paths that start with "//" whereas the others allow them. Research seems to indicate that this was not intentional. More details on the mailing list discussion: https://lists.w3.org/Archives/Public/ietf-http-wg/2022JulSep/0014.html
```

</details>

<br>**Explanation:**
The description of the ":path" header field in Section 4.3.1 uses the term "path-absolute", which conflicts with the usage in other RFCs (RFCs 9110, 9112, 9113) and the intended behavior.  The correct term should be "absolute-path", aligning with the definitions in those RFCs. This inconsistency affects interoperability, as implementations might interpret the path differently based on which RFC they adhere to more strictly.

---

<details>
<summary><b>Errata 7780</b> from <b>RFC 9114</b> - HTTP/3 (June 2022)</summary>

```
Section 7.2.6 says:


The GOAWAY frame applies to the entire connection,
not a specific stream. A client MUST treat a
GOAWAY frame on a stream other than the control
stream as a connection error of type
H3_FRAME_UNEXPECTED.

It should say:

The GOAWAY frame applies to the entire connection,
not a specific stream. An endpoint MUST treat a
GOAWAY frame on a stream other than the control
stream as a connection error of type
H3_FRAME_UNEXPECTED.

Notes:

HTTP/3 originally only supported GOAWAY from server to client. In this PR we added the ability to also send GOAWAY from client to server https://github.com/quicwg/base-drafts/pull/3129/files. Unfortunately we didn't update the highlighted text to cover the situation where a server receives a GOAWAY on a different stream. 

FWIW the implementation I am responsible for already applies the rule to request streams.
```

</details>

<br>**Explanation:**
The original specification in Section 7.2.6 incorrectly states that only a client MUST treat a GOAWAY frame on a non-control stream as a connection error.  The updated specification correctly states that both client and server endpoints MUST handle this situation, reflecting the change to allow bidirectional GOAWAY frames. This inconsistency affects the implementation of both clients and servers that must correctly handle GOAWAY frames on streams other than the control stream.

---

<details>
<summary><b>Errata 8103</b> from <b>RFC 9421</b> - HTTP Message Signatures (February 2024)</summary>

```
Section 7.5.3 says:


Several parts of this specification rely on the parsing of Structured
Field values [STRUCTURED-FIELDS] -- in particular, strict
serialization of HTTP Structured Field values (Section 2.1.1),
referencing members of a Dictionary Structured Field (Section 2.1.2),
and processing the @signature-input value when verifying a signature
(Section 3.2).  While Structured Field values are designed to be
relatively simple to parse, a naive or broken implementation of such
a parser could lead to subtle attack surfaces being exposed in the
implementation.

For example, if a buggy parser of the @signature-input value does not
enforce proper closing of quotes around string values within the list
of component identifiers, an attacker could take advantage of this
and inject additional content into the signature base through
manipulating the Signature-Input field value on a message.

It should say:

Several parts of this specification rely on the parsing of Structured
Field values [STRUCTURED-FIELDS] -- in particular, strict
serialization of HTTP Structured Field values (Section 2.1.1),
referencing members of a Dictionary Structured Field (Section 2.1.2),
and processing the @signature-params value when verifying a signature
(Section 3.2).  While Structured Field values are designed to be
relatively simple to parse, a naive or broken implementation of such
a parser could lead to subtle attack surfaces being exposed in the
implementation.

For example, if a buggy parser of the @signature-params value does not
enforce proper closing of quotes around string values within the list
of component identifiers, an attacker could take advantage of this
and inject additional content into the signature base through
manipulating the Signature-Input field value on a message.

Notes:

"@signature-input" should be changed to "@signature-params". There is one such error in both the first and second paragraphs of Section 7.5.3.
```

</details>

<br>**Explanation:**
The text in Section 7.5.3 incorrectly refers to "@signature-input" in two places where it should refer to "@signature-params". This inconsistency could lead to misunderstandings of how the specification should be implemented and affect security, because the correct handling of the @signature-params field is critical for signature verification.

---

<details>
<summary><b>Errata 3885</b> from <b>RFC 6940</b> - REsource LOcation And Discovery (RELOAD) Base Protocol (January 2014)</summary>

```
Section 14.9 says:


   | Reserved                            | 0x8000..0xFFFE |  RFC 6940 |

It should say:

   | Reserved                            | 0x8000..0xFFFF |  RFC 6940 |

Notes:

Clearly there was some confusion and at least one of the authors thought that 0xFFFE was the largest 16 bit integer when in fact it should have been 0xFFFF. I would like to thank Pearl Liang for catching this mistake.
```

</details>

<br>**Explanation:**
This is from the IANA considerations section.

---

<details>
<summary><b>Errata 7259</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section 3.3.2 says:


   The use of EAP-FAST-GTC as defined in RFC 5421 [RFC5421] is NOT
   RECOMMENDED with TEAPv1 because EAP-FAST-GTC is not compliant with
   EAP-GTC defined in [RFC3748].  Implementations should instead make
   use of the password authentication TLVs defined in this
   specification.  The authentication server initiates password
   authentication by sending a Basic-Password-Auth-Req TLV defined in
   Section 4.2.14.  If the peer wishes to participate in password
   authentication, then it responds with a Basic-Password-Auth-Resp TLV
   as defined in Section 4.2.15 that contains the username and password.
   If it does not wish to perform password authentication, then it
   responds with a NAK TLV indicating the rejection of the Basic-
   Password-Auth-Req TLV.  Upon receiving the response, the server
   indicates the success or failure of the exchange using an
   Intermediate-Result TLV.  Multiple round trips of password
   authentication requests and responses MAY be used to support some
   "housecleaning" functions such as a password or pin change before a
   user is authenticated.


It should say:

   The use of EAP-FAST-GTC as defined in RFC 5421 [RFC5421] is NOT
   RECOMMENDED with TEAPv1 because EAP-FAST-GTC is not compliant with
   EAP-GTC defined in [RFC3748].  Implementations should instead make
   use of the password authentication TLVs defined in this
   specification.  The authentication server initiates password
   authentication by sending a Basic-Password-Auth-Req TLV defined in
   Section 4.2.14.  If the peer wishes to participate in password
   authentication, then it responds with a Basic-Password-Auth-Resp TLV
   as defined in Section 4.2.15 that contains the username and password.
   If it does not wish to perform password authentication, then it
   responds with a NAK TLV indicating the rejection of the Basic-
   Password-Auth-Req TLV.  Upon receiving the response, the server
   indicates the success or failure of the exchange using an
   Intermediate-Result TLV.  Multiple round trips of password
   authentication requests and responses MAY be used to support some
   "housecleaning" functions such as a password or pin change before a
   user is authenticated.

   If using EAP-MSCHAPv2 as an inner method, the EAP-FAST-MSCHAPv2
   variant defined in [RFC5422] MUST be used.

Notes:

While RFC 7170 does not really require this and would be technically correct as-is for this area, deployed implementations of EAP-TEAP seem to have used MSK/IMSK derivation for an inner EAP method in a manner that matches what was done with EAP-FAST. This could be called non-compliant, but for the sake of interoperability, it might make more sense to describe what is done in deployed implementation instead. The only technical difference here is in swapping the first and the second 16 octets of EAP-MSCHAPv2 MSK when it is used as the IMSK for EAP-TEAP.
```

</details>

<br>**Explanation:**
The erratum is a recommendation for improved interoperability, suggesting a specific way to handle EAP-MSCHAPv2.  It doesn't correct an error or ambiguity in the original RFC but offers guidance for better compatibility with existing implementations. This is a suggestion, not a correction of an inconsistency, underspecification, or ambiguity.

---

<details>
<summary><b>Errata 4011</b> from <b>RFC 7196</b> - Making Route Flap Damping Usable (May 2014)</summary>

```
Section 3 says:


Table 1: Default RFD Parameters of Juniper and Cisco

It should say:

Table 1: The default RFD parameters for Cisco and Juniper 
         provided for the information of the reader.

Notes:

The RFC Editor Note (resulting from Barry and Benoit's DISCUSS) documented at https://datatracker.ietf.org/doc/draft-ietf-idr-rfd-usable/writeup/ has been forgotten.
```

</details>

<br>**Explanation:**
The errata report is about updating the title of Table 1 to reflect that the table provides information on default parameters of Cisco and Juniper routers. This is a stylistic or presentational change that does not affect the implementation of the RFC.

---

<details>
<summary><b>Errata 6721</b> from <b>RFC 7208</b> - Sender Policy Framework (SPF) for Authorizing Use of Domains in Email, Version 1 (April 2014)</summary>

```
Section 8.4 says:


       550 5.7.1 SPF MAIL FROM check failed:
       550 5.7.1 The domain example.com explains:
       550 5.7.1 Please see http://www.example.com/mailpolicy.html


It should say:

       550-5.7.1 SPF MAIL FROM check failed:
       550-5.7.1 The domain example.com explains:
       550 5.7.1 Please see http://www.example.com/mailpolicy.html


Notes:

In addition, RFC 7208 does not give an example of rejection based on the HELO argument.
```

</details>

<br>**Explanation:**
The erratum corrects the formatting of an example rejection message by adding hyphens. While this improves the example's accuracy, it doesn't address a fundamental inconsistency or ambiguity in the RFC's technical specifications or implementation guidance.  It also notes a missing example, which is a suggestion for improvement, not an error correction.

---

<details>
<summary><b>Errata 4106</b> from <b>RFC 7260</b> - GMPLS RSVP-TE Extensions for Operations, Administration, and Maintenance (OAM) Configuration (June 2014)</summary>

```
Section 5.5.2 says:


   IANA has created the "OAM Sub-TLVs" sub-registry of the "RSVP-TE OAM
   Configuration Registry" as follows:

   Range       | Note                         | Registration Procedures
   ------------+------------------------------|------------------------
   0-31        | Generic Sub-TLVs             | IETF Review
   32-65534    | Technology-specific Sub-TLVs | IETF Review
   65535-65536 | Experimental Sub-TLVs        | Reserved for
               |                              |   Experimental Use

   IANA has populated the registry as follows:

      Sub-TLV Type | Description                   | Reference
      -------------+-------------------------------+----------
          0        | Reserved                      | [RFC7260]
          1        | OAM Function Flags Sub-TLV    | [RFC7260]
          2-65534  | Unassigned                    |
      65535-65536  | Reserved for Experimental Use | [RFC7260]



It should say:

    IANA has created the "OAM Sub-TLVs" sub-registry of the "RSVP-TE OAM
    Configuration Registry" as follows:

    Range       | Note                         | Registration Procedures
    ------------+------------------------------|------------------------
    0-31        | Generic Sub-TLVs             | IETF Review
    32-65533    | Technology-specific Sub-TLVs | IETF Review
    65534-65535 | Experimental Sub-TLVs        | Reserved for
                |                              |   Experimental Use

    IANA has populated the registry as follows:

       Sub-TLV Type | Description                   | Reference
       -------------+-------------------------------+----------
           0        | Reserved                      | [RFC7260]
           1        | OAM Function Flags Sub-TLV    | [RFC7260]
           2-65533  | Unassigned                    |
       65534-65535  | Reserved for Experimental Use | [RFC7260]


Notes:

Because the Type field is two octets long the value 65536 is unrealizable.
Nevertheless, it was the intention of the working group to assign to values as experimental.
```

</details>

<br>**Explanation:**
This is from the IANA considerations section.

---

<details>
<summary><b>Errata 6874</b> from <b>RFC 7285</b> - Application-Layer Traffic Optimization (ALTO) Protocol (September 2014)</summary>

```
Section 14.2 says:


                   +-------------+---------------------+
                   | Identifier  | Intended Semantics  |
                   +-------------+---------------------+
                   | routingcost | See Section 6.1.1.1 |
                   | priv:       | Private use         |
                   +-------------+---------------------+

                        Table 3: ALTO Cost Metrics

It should say:

                   +-------------+---------------------+
                   | Identifier  | Intended Semantics  |
                   +-------------+---------------------+
                   | routingcost | See Section 6.1.1.1 |
                   +-------------+---------------------+

                        Table 3: ALTO Cost Metrics

Note: Identifiers prefixed with "priv:" are
reserved for Private Use (see Section 10.6)

Notes:

priv: is not a cost metric but a prefix
```

</details>

<br>**Explanation:**
The errata removes the 'priv:' entry from Table 3, correctly noting that it is not a cost metric but a prefix for private use identifiers. This change is a clarification rather than a correction of an inconsistency that affects implementation.

---

<details>
<summary><b>Errata 6876</b> from <b>RFC 7285</b> - Application-Layer Traffic Optimization (ALTO) Protocol (September 2014)</summary>

```
Section 14.3 says:


                    +------------+--------------------+
                    | Identifier | Intended Semantics |
                    +------------+--------------------+
                    | pid        | See Section 7.1.1  |
                    | priv:      | Private use        |
                    +------------+--------------------+
 
                   Table 4: ALTO Endpoint Property Types


It should say:

                    +------------+--------------------+
                    | Identifier | Intended Semantics |
                    +------------+--------------------+
                    | pid        | See Section 7.1.1  |
                    +------------+--------------------+
 
                   Table 4: ALTO Endpoint Property Types

 Note: Identifiers prefixed with "priv:" are
 reserved for Private Use (see Section 10.8.2.)


Notes:

priv: is not an identifier, but a prefix.
```

</details>

<br>**Explanation:**
The erratum corrects Table 4 by removing the 'priv:' entry, which is not an endpoint property type but a prefix for private use identifiers.  This is a clarification rather than a correction of a technical inconsistency or ambiguity, and therefore it is categorized as 'OTHER'.

---

<details>
<summary><b>Errata 4242</b> from <b>RFC 7434</b> - Interworking ISDN Call Control User Information with SIP (January 2015)</summary>

```
Section 13 says:


      ASN.1 Identifier: 1.3.6.1.8.4.x

It should say:

      ASN.1 Identifier: 1.3.6.1.8.4.26

Notes:

The IANA-assigned value should be filled in.
```

</details>

<br>**Explanation:**
This is from the IANA Considerations section.

---

<details>
<summary><b>Errata 5460</b> from <b>RFC 7484</b> - Finding the Authoritative Registration Data (RDAP) Service (March 2015)</summary>

```
Section 8 says:


      In the case of a domain object, the client may first query the DNS
      to see if the respective entry has been delegated or if it is
      mistyped information by the user.  The DNS query could be to fetch
      the NS records for the TLD domain.  If the DNS answer is negative,
      then there is no need to fetch the new version of the registry.
      However, if the DNS answer is positive, this may mean that the
      currently cached registry is no longer current.  The client could
      then fetch the registry, parse, and then do the normal matching as
      specified above.  This method may not work for all types of RDAP
      objects.

Notes:

I would remove the whole section. The point is: if the DNS answer is positive, then you need to fetch the registry. But if the answer is negative, this does not mean anything because it it possible that a registered domain is not delegated.
```

</details>

<br>**Explanation:**
The errata report suggests removing a section that describes a method for determining the currency of a cached registry using DNS. The note indicates that the method is unreliable and may not work for all RDAP object types.  Since the method's removal is suggested rather than a correction of an existing error, and it does not affect the core functionality, this is classified as OTHER.

---

<details>
<summary><b>Errata 5462</b> from <b>RFC 7542</b> - The Network Access Identifier (May 2015)</summary>

```
Section 3 says:


The "utf8-realm" SHOULD be supplied by the "next hop" or "home"
system that also supplies the routing information necessary for
packets to reach the next hop.

It should say:

The "utf8-realm" SHOULD be supplied by the "next hop" or "home"
system that also supplies the routing information necessary for
packets to reach the next hop.

The final home system SHOULD validate the NAI in the received packet
against the list of Realms hosted by the home system.  If no match
is found, the request SHOULD be rejected.

Notes:

It doesn't explicitly say that home systems only authenticate users for their own realms.  It may help to have this stated explicitly.

Some text will also be added to draft-ietf-radext-coa-proxy in order to make this clearer.
```

</details>

<br>**Explanation:**
The errata adds a statement clarifying that home systems should only authenticate users for their own realms.  While this is a helpful addition for clarity, it does not correct an error or inconsistency in the original specification that affects implementation.  The addition is primarily for improved understanding.

---

<details>
<summary><b>Errata 8193</b> from <b>RFC 7589</b> - Using the NETCONF Protocol over Transport Layer Security (TLS) with Mutual X.509 Authentication (June 2015)</summary>

```
Section 2 says:


The well-known TCP port number 6513 is used by NETCONF servers to listen for TCP connections established by NETCONF over TLS clients.

It should say:

The registered TCP port number 6513 is used by NETCONF servers to listen for TCP connections established by NETCONF over TLS clients.

Notes:

Section 10 of that same RFC correctly states: "Per RFC 5539, IANA assigned TCP port number (6513) in the 'Registered Port Numbers' range with the service name 'netconf-tls'. This port is the default port for NETCONF over TLS, as defined in Section 2." With that said, wouldn't the sentence concerned be more correct in the suggested form? Thanks!
```

</details>

<br>**Explanation:**
The erratum corrects the description of port 6513 as a registered port rather than a well-known port. This is a minor correction that improves the accuracy of the description but does not affect the core technical specifications or implementation of NETCONF over TLS. It's a matter of precision and terminology rather than a fix for an inconsistency, underspecification, or ambiguity.

---

<details>
<summary><b>Errata 7916</b> from <b>RFC 7644</b> - System for Cross-domain Identity Management: Protocol (September 2015)</summary>

```
Section 3.7.3 says:


 containing a human-readable explanation of the error.

   "status": "201"

   The following is an example of a status in a failed operation.

  "status": "400",
  "response":{
       "schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],
       "scimType":"invalidSyntax"
       "detail":
  "Request is unparsable, syntactically incorrect, or violates schema.",
       "status":"400"
   }

It should say:

 containing a human-readable explanation of the error.

 The following is an example of a status in a failed operation.

  {
     "status": "400",
     "schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],
     "scimType":"invalidSyntax",
     "detail":"Request is unparsable, syntactically incorrect, or violates schema.",
   }

Notes:

it misses a { at the beginning of the 400 sample 
it missies a ,  after invalidSyntax

the overall response looks wrong

Notice that even putting a there can be questionnable as well , and an alternative would be to just drop the content mentionned

SecAD Summary of the changes (per the authors):
* Remove line: “status”: “201”
* Add leading brace ‘{‘
* Add missing comma after “invalidSyntax”
```

</details>

<br>**Explanation:**
The provided example of a failed operation response is malformed JSON.  The corrected JSON fixes syntax errors (missing brace and comma) and removes redundant fields, resulting in a valid and consistent example that matches the specification.

---

<details>
<summary><b>Errata 7194</b> from <b>RFC 7854</b> - BGP Monitoring Protocol (BMP) (June 2016)</summary>

```
Section 10.8 says:


   Information type values 0 through 32767 MUST be assigned using the
   "Standards Action" policy, and values 32768 through 65530 using the
   "Specification Required" policy, defined in [RFC5226].  Values 65531
   through 65534 are Experimental, and values 0 and 65535 are Reserved.

It should say:

   Information type values 0 through 127 MUST be assigned using the
   "Standards Action" policy, and values 128 through 250 using the
   "Specification Required" policy, defined in [RFC5226].  Values 251
   through 254 are Experimental, and values 0 and 255 are Reserved.

Notes:

In Section 4.9 Peer Down Notification. The "Reason" field is defined as one octet, while the IANA consideration section is defining values as 2-octets range. This errata suggests updating the IANA registry, instead of the size of the "Reason" field in the Peer Down Notification message to avoid breaking existing implementations that use one-octet reason.

[WK]: See thread https://mailarchive.ietf.org/arch/msg/grow/s-qcQpAkFVK3beirNYqY4MYfbFw/ for tracking. IANA has confirmed that they can update registries from verified errata.
```

</details>

<br>**Explanation:**
This is from the IANA considerations in the RFC.

---

<details>
<summary><b>Errata 7579</b> from <b>RFC 7919</b> - Negotiated Finite Field Diffie-Hellman Ephemeral Parameters for Transport Layer Security (TLS) (August 2016)</summary>

```
Section Appendix A says:


The primes in these finite field groups are all safe primes; that is,
a prime p is a safe prime when q = (p-1)/2 is also prime.  Where e is
the base of the natural logarithm and square brackets denote the
floor operation, the groups that initially populate this registry are
derived for a given bit length b by finding the lowest positive
integer X that creates a safe prime p where:

 p = 2^b - 2^{b-64} + {[2^{b-130} e] + X } * 2^64 - 1


It should say:

The primes in these finite field groups are all safe primes; that is,
a prime p is a safe prime when q = (p-1)/2 is also prime.  Where e is
the base of the natural logarithm and square brackets denote the
floor operation, the groups that initially populate this registry are
derived for a given bit length b by finding the lowest positive
integer X that creates a safe prime p where:

 p = 2^b - 2^{b-64} + {[2^{b-130} * e] + X } * 2^64 - 1


Notes:

The multiplication sign ('*' in ASCII) is missing in the explanatory introduction of Appendix A that describes the equation used for deriving the primes. It is correct in all five concrete derivations A.1 through A.5
```

</details>

<br>**Explanation:**
The original equation for deriving safe primes is missing a multiplication operator, leading to an incorrect calculation.  This inconsistency affects the derivation of the prime numbers used in the finite field groups, which is a critical aspect of the security of the protocol. The missing multiplication sign creates an inconsistency between the description of the equation and its correct form.

---

<details>
<summary><b>Errata 5517</b> from <b>RFC 7950</b> - The YANG 1.1 Data Modeling Language (August 2016)</summary>

```
Section 10.4.2 says:


The derived-from-or-self() function returns "true" if any node in the
   argument "nodes" is a node of type "identityref" and its value is an
   identity that is equal to or derived from (see Section 7.18.2) the
   identity "identity"; otherwise, it returns "false".


It should say:

 The derived-from-or-self() function returns "true" if any node in the
 argument "nodes" is a node of type "identityref" or a type derived
 from "identityref", and its value is an identity that is equal to or
 derived from (see Section 7.18.2) the identity "identity"; 
 otherwise, it returns "false".


Notes:

The node-set can have node which are of types that may be derived from an identityref. Typical example is in ietf-netconf-nmda, where "when 'derived-from-or-self(datastore, "ds:operational")';" is used, but the "datastore" node is of type "datastore-ref" defined in ietf-datastores module, which is in-turn derived from "identityref"

corrected text proposal with additional editing by Martin Bjorklund and Ladislav Lhotka
```

</details>

<br>**Explanation:**
This is a proposal.

---

<details>
<summary><b>Errata 5009</b> from <b>RFC 8045</b> - RADIUS Extensions for IP Port Configuration and Reporting (January 2017)</summary>

```
Section 7.1 says:


   o  sourceTransportPortsLimit:

      *  Name: sourceTransportPortsLimit

      *  Element ID: 458

      *  Description: This Information Element contains the maximum
         number of IP source transport ports that can be used by an end
         user when sending IP packets; each user is associated with one
         or more (source) IPv4 or IPv6 addresses.  This Information
         Element is particularly useful in address-sharing deployments
         that adhere to REQ-4 of [RFC6888].  Limiting the number of
         ports assigned to each user ensures fairness among users and
         mitigates the denial-of-service attack that a user could launch
         against other users through the address-sharing device in order
         to grab more ports.

      *  Data type: unsigned16

      *  Data type semantics: totalCounter

It should say:

   o  sourceTransportPortsLimit:

      *  Name: sourceTransportPortsLimit

      *  Element ID: 458

      *  Description: This Information Element contains the maximum
         number of IP source transport ports that can be used by an end
         user when sending IP packets; each user is associated with one
         or more (source) IPv4 or IPv6 addresses.  This Information
         Element is particularly useful in address-sharing deployments
         that adhere to REQ-4 of [RFC6888].  Limiting the number of
         ports assigned to each user ensures fairness among users and
         mitigates the denial-of-service attack that a user could launch
         against other users through the address-sharing device in order
         to grab more ports.

      *  Data type: unsigned16

      *  Data type semantics: quantity

Notes:

Only change is 

      *  Data type semantics: totalCounter
to
      *  Data type semantics: quantity

The description is pretty clear that this IE is a maximum value and not a counter.
```

</details>

<br>**Explanation:**
This is from the IANA Considerations section.

---

<details>
<summary><b>Errata 6743</b> from <b>RFC 8214</b> - Virtual Private Wire Service Support in Ethernet VPN (August 2017)</summary>

```
Section 4 says:


          Ethernet                                          Ethernet
          Native   |<--------- EVPN Instance ----------->|  Native
          Service  |                                     |  Service
          (AC)     |     |<-PSN1->|       |<-PSN2->|     |  (AC)
             |     V     V        V       V        V     V  |
             |     +-----+      +-----+  +-----+   +-----+  |
      +----+ |     | PE1 |======|ASBR1|==|ASBR2|===| PE3 |  |    +----+
      |    |-------+-----+      +-----+  +-----+   +-----+-------|    |
      | CE1| |                                              |    |CE2 |
      |    |-------+-----+      +-----+  +-----+   +-----+-------|    |
      +----+ |     | PE2 |======|ASBR3|==|ASBR4|===| PE4 |  |    +----+
           ^       +-----+      +-----+  +-----+   +-----+          ^
           |   Provider Edge 1        ^        Provider Edge 2      |
           |                          |                             |
           |                          |                             |
           |              EVPN Inter-provider point                 |
           |                                                        |
           |<---------------- Emulated Service -------------------->|

                   Figure 3: EVPN-VPWS Deployment Model


It should say:

          Ethernet                                          Ethernet
          Native   |<--------- EVPN Instance ----------->|  Native
          Service  |                                     |  Service
          (AC)     |     |<-PSN1->|       |<-PSN2->|     |  (AC)
             |     V     V        V       V        V     V  |
             |     +-----+      +-----+  +-----+   +-----+  |
      +----+ |     | PE1 |======|ASBR1|==|ASBR2|===| PE3 |  |    +----+
      |    |-------+-----+      +-----+  +-----+   +-----+-------|    |
      | CE1| |                                              |    |CE2 |
      |    |-------+-----+      +-----+  +-----+   +-----+-------|    |
      +----+ |     | PE2 |======|ASBR3|==|ASBR4|===| PE4 |  |    +----+
           ^       +-----+      +-----+  +-----+   +-----+       ^
           |   Provider Edge 1        ^        Provider Edge 2   |
           |                          |                          |
           |                          |                          |
           |              EVPN Inter-provider point              |
           |                                                     |
           |<---------------- Emulated Service ----------------->|

                   Figure 3: EVPN-VPWS Deployment Model


Notes:

The right-hand end of the Emulated Service should be aligned with the provider-facing AC port on CE2 and not  placed in the middle of CE2.
Although this may appear to be a minor editorial issue, the technical consequences are significant.
```

</details>

<br>**Explanation:**
The erratum corrects the diagram to accurately represent the alignment of the Emulated Service with the CE2 port. Although visually minor, this change ensures the diagram accurately reflects the network configuration.  The change is primarily visual and does not correct an error in the technical specification.

---

<details>
<summary><b>Errata 5399</b> from <b>RFC 8311</b> - Relaxing Restrictions on Explicit Congestion Notification (ECN) Experimentation (January 2018)</summary>

```
Section 7 says:


(n/a, this errata adds an additional IANA Consideration)

It should say:

To reflect the experimental use of ECT(1) envisioned by this memo,
IANA has added the following footnote to the ECN Field registry
<https://www.iana.org/assignments/dscp-registry/
dscp-registry.xhtml#ecn-field>:

ECT(1) is for experimental use only [RFC8311, Section 4.2]


Notes:

The Corrected Text is written as if IANA has already added the footnote, which will be done upon approval of this errata, citing this approved errata as justification.

(From Spencer - this could have been Held for Document Update, but I think Verified is just about as correct)
```

</details>

<br>**Explanation:**
This erratum adds an IANA consideration, which is a post-publication administrative action rather than a correction of a technical error or ambiguity in the RFC's specification.

---

<details>
<summary><b>Errata 6002</b> from <b>RFC 8422</b> - Elliptic Curve Cryptography (ECC) Cipher Suites for Transport Layer Security (TLS) Versions 1.2 and Earlier (August 2018)</summary>

```
Section 9 says:


   IANA has assigned two values in the "TLS SignatureAlgorithm" registry
   for ed25519 (7) and ed448 (8) with this document as reference.  This
   keeps compatibility with TLS 1.3.


It should say:

   IANA has assigned two values in the "TLS SignatureAlgorithm" registry
   for ed25519 (7) and ed448 (8) with DTLS-OK set to "Y" and this document
   as reference.  This keeps compatibility with TLS 1.3.

Notes:

IANA had consulted with Yoav, one of the authors (and a TLS registry expert), who explicitly told them to use DTLS-OK of "Y", but this clarification was not reflected in the final RFC.  This also matches the text in the subsequent paragraph.
```

</details>

<br>**Explanation:**
This is from the IANA considerations section.

---

<details>
<summary><b>Errata 6146</b> from <b>RFC 8446</b> - The Transport Layer Security (TLS) Protocol Version 1.3 (August 2018)</summary>

```
Section 4.2.10. says:


The TLS version number

It should say:

The selected TLS version number
```

</details>

<br>**Explanation:**
The original text is imprecise. The corrected text clarifies that it is the selected TLS version number that is being discussed. This is a minor clarification that does not affect the implementation of TLS 1.3.

---

<details>
<summary><b>Errata 6290</b> from <b>RFC 8489</b> - Session Traversal Utilities for NAT (STUN) (February 2020)</summary>

```
Section 18.1 says:


Bits are assigned starting from the most significant side of the bit
set, so Bit 0 is the leftmost bit and Bit 23 is the rightmost bit.

It should say:

Bits are assigned starting from the least significant side of the bit
set, so Bit 0 is the rightmost bit, and Bit 23 is the leftmost bit.
```

</details>

<br>**Explanation:**
This is from the IANA considerations section.

---

<details>
<summary><b>Errata 7960</b> from <b>RFC 8708</b> - Use of the HSS/LMS Hash-Based Signature Algorithm in the Cryptographic Message Syntax (CMS) (February 2020)</summary>

```
Section Appendix A says:


   pk-HSS-LMS-HashSig PUBLIC-KEY ::= {
       IDENTIFIER id-alg-hss-lms-hashsig
       KEY HSS-LMS-HashSig-PublicKey
       PARAMS ARE absent
       CERT-KEY-USAGE
           { digitalSignature, nonRepudiation, keyCertSign, cRLSign } }

It should say:

   pk-HSS-LMS-HashSig PUBLIC-KEY ::= {
       IDENTIFIER id-alg-hss-lms-hashsig
       -- KEY no ASN.1 wrapping --
       PARAMS ARE absent
       CERT-KEY-USAGE
           { digitalSignature, nonRepudiation, keyCertSign, cRLSign } }

Notes:

At the time RFC 8708 was published, we did not think anyone would put an HSS/LMS public key in a certificate.  We thought the public key would always be distributed by some other means.  We now know that some people plan to put an HSS/LMS public key in a certificate.  This part of the ASN.1 module does not come into play when using HSS/LMS in the CMS, but we want it to be consistent with the yet-to-be-published document that describes the conventions for an HSS/LMS public key in a certificate.  IETF Hackathon experience shows that no ASN.1 wrapping for the public key is the way forward.
```

</details>

<br>**Explanation:**
This is a proposal or suggestion.

---

<details>
<summary><b>Errata 7963</b> from <b>RFC 8708</b> - Use of the HSS/LMS Hash-Based Signature Algorithm in the Cryptographic Message Syntax (CMS) (February 2020)</summary>

```
Section 4 says:


      pk-HSS-LMS-HashSig PUBLIC-KEY ::= {
          IDENTIFIER id-alg-hss-lms-hashsig
          KEY HSS-LMS-HashSig-PublicKey
          PARAMS ARE absent
          CERT-KEY-USAGE
            { digitalSignature, nonRepudiation, keyCertSign, cRLSign } }

      HSS-LMS-HashSig-PublicKey ::= OCTET STRING

   Note that the id-alg-hss-lms-hashsig algorithm identifier is also
   referred to as id-alg-mts-hashsig.  This synonym is based on the
   terminology used in an early draft version of the document that
   became [HASHSIG].

   The public key value is an OCTET STRING.  Like the signature format,
   it is designed for easy parsing.  The value is the number of levels
   in the public key, L, followed by the LMS public key.

It should say:

      pk-HSS-LMS-HashSig PUBLIC-KEY ::= {
          IDENTIFIER id-alg-hss-lms-hashsig
          -- KEY no ASN.1 wrapping --
          PARAMS ARE absent
          CERT-KEY-USAGE
            { digitalSignature, nonRepudiation, keyCertSign, cRLSign } }

      HSS-LMS-HashSig-PublicKey ::= OCTET STRING

   Note that the id-alg-hss-lms-hashsig algorithm identifier is also
   referred to as id-alg-mts-hashsig.  This synonym is based on the
   terminology used in an early draft version of the document that
   became [HASHSIG].

   When the public key appears outside a certificate, it is an 
   OCTET STRING.  Like the signature format, it is designed for easy
   parsing.  The value is the number of levels in the public key, L,
   followed by the LMS public key.

Notes:

At the time RFC 8708 was published, we did not think anyone would put an HSS/LMS public key in a certificate. We thought the public key would always be distributed by some other means. We now know that some people plan to put an HSS/LMS public key in a certificate. This part of the ASN.1 module does not come into play when using HSS/LMS in the CMS, but we want it to be consistent with the yet-to-be-published document that describes the conventions for an HSS/LMS public key in a certificate. IETF Hackathon experience shows that no ASN.1 wrapping for the public key is the way forward.
```

</details>

<br>**Explanation:**
This is a proposal or suggestion.

---

<details>
<summary><b>Errata 7189</b> from <b>RFC 8794</b> - Extensible Binary Meta Language (July 2020)</summary>

```
Section 17.1. says:


   One-octet Element IDs MUST be between 0x81 and 0xFE.  These items are
   valuable because they are short, and they need to be used for
   commonly repeated elements.  Element IDs are to be allocated within
   this range according to the "RFC Required" policy [RFC8126].

   The following one-octet Element IDs are RESERVED: 0xFF and 0x80.

   Values in the one-octet range of 0x00 to 0x7F are not valid for use
   as an Element ID.

   Two-octet Element IDs MUST be between 0x407F and 0x7FFE.  Element IDs
   are to be allocated within this range according to the "Specification
   Required" policy [RFC8126].

   The following two-octet Element IDs are RESERVED: 0x7FFF and 0x4000.

   Values in the two-octet ranges of 0x0000 to 0x3FFF and 0x8000 to
   0xFFFF are not valid for use as an Element ID.

   Three-octet Element IDs MUST be between 0x203FFF and 0x3FFFFE.
   Element IDs are to be allocated within this range according to the
   "First Come First Served" policy [RFC8126].

   The following three-octet Element IDs are RESERVED: 0x3FFFFF and
   0x200000.

   Values in the three-octet ranges of 0x000000 to 0x1FFFFF and 0x400000
   to 0xFFFFFF are not valid for use as an Element ID.

   Four-octet Element IDs MUST be between 0x101FFFFF and 0x1FFFFFFE.
   Four-octet Element IDs are somewhat special in that they are useful
   for resynchronizing to major structures in the event of data
   corruption or loss.  As such, four-octet Element IDs are split into
   two categories.  Four-octet Element IDs whose lower three octets (as
   encoded) would make printable 7-bit ASCII values (0x20 to 0x7E,
   inclusive) MUST be allocated by the "Specification Required" policy.
   Sequential allocation of values is not required: specifications
   SHOULD include a specific request and are encouraged to do early
   allocations.

   To be clear about the above category: four-octet Element IDs always
   start with hex 0x10 to 0x1F, and that octet may be chosen so that the
   entire VINT has some desirable property, such as a specific CRC.  The
   other three octets, when ALL having values between 0x20 (32, ASCII
   Space) and 0x7E (126, ASCII "~"), fall into this category.

   Other four-octet Element IDs may be allocated by the "First Come
   First Served" policy.

   The following four-octet Element IDs are RESERVED: 0x1FFFFFFF and
   0x10000000.

   Values in the four-octet ranges of 0x00000000 to 0x0FFFFFFF and
   0x20000000 to 0xFFFFFFFF are not valid for use as an Element ID.



It should say:

   One-octet Element IDs MUST be allocated in the range 0x80 - 0xFE.  
   These items are valuable because they are short, and they need to be 
   used for commonly repeated elements.  Element IDs are to be allocated within
   this range according to the "RFC Required" policy [RFC8126].

   The following one-octet Element ID is RESERVED: 0xFF.

   Values in the one-octet range of 0x00 - 0x7F are not valid for use
   as Element IDs.

   Two-octet Element IDs MUST be allocated in the range 0x407F - 0x7FFE.  
   Element IDs are to be allocated within this range according to the 
   "Specification Required" policy [RFC8126].

   The following two-octet Element ID is RESERVED: 0x7FFF.

   Values in the two-octet ranges of 0x0100 - 0x407E and 
   0x8000 - 0xFFFF are not valid for use as Element IDs.

   Three-octet Element IDs MUST be allocated in the range 0x203FFF - 0x3FFFFE.
   Element IDs are to be allocated within this range according to the
   "First Come First Served" policy [RFC8126].

   The following three-octet Element ID is RESERVED: 0x3FFFFF.

   Values in the three-octet ranges of 0x010000 - 0x203FFE and 
   0x400000 - 0xFFFFFF are not valid for use as Element IDs.

   Four-octet Element IDs MUST be allocated in the range 0x101FFFFF - 0x1FFFFFFE.
   Four-octet Element IDs are somewhat special in that they are useful
   for resynchronizing to major structures in the event of data
   corruption or loss.  As such, four-octet Element IDs are split into
   two categories.  Four-octet Element IDs whose lower three octets (as
   encoded) would make printable 7-bit ASCII values (0x20 to 0x7E,
   inclusive) MUST be allocated by the "Specification Required" policy.
   Sequential allocation of values is not required: specifications
   SHOULD include a specific request and are encouraged to do early
   allocations.

   To be clear about the above category: four-octet Element IDs always
   start with hex 0x10 to 0x1F, and that octet may be chosen so that the
   entire VINT has some desirable property, such as a specific CRC.  The
   other three octets, when ALL having values between 0x20 (32, ASCII
   Space) and 0x7E (126, ASCII "~"), fall into this category.

   Other four-octet Element IDs may be allocated by the "First Come
   First Served" policy.

   The following four-octet Element ID is RESERVED: 0x1FFFFFFF.

   Values in the four-octet ranges of 0x01000000 - 0x101FFFFE and 
   0x20000000 - 0xFFFFFFFF are not valid for use as Element IDs.

Notes:

This erratum corrects values in this text.
```

</details>

<br>**Explanation:**
This is from the IANA considerations section.

---

<details>
<summary><b>Errata 7397</b> from <b>RFC 8824</b> - Static Context Header Compression (SCHC) for the Constrained Application Protocol (CoAP) (June 2021)</summary>

```
Section 7.2 says:


These classes point out that the Outer option contains the OSCORE
option and that the message is OSCORE protected; this option carries
the information necessary to retrieve the Security Context.

It should say:

As per these classes, the Outer options comprise the OSCORE option,
which indicates that the message is OSCORE protected and carries
the information necessary to retrieve the Security Context.

Notes:

"Outer options" should be in the plural, to refer to the set of CoAP options left unencrypted. Such a set comprises also the OSCORE option, which is the actual indicator of the message being protected with OSCORE.
```

</details>

<br>**Explanation:**
This change is for readability and clarity.

---

<details>
<summary><b>Errata 6872</b> from <b>RFC 8984</b> - JSCalendar: A JSON Representation of Calendar Data (July 2021)</summary>

```
Section 4.4.3. says:


   "private":  The details of the object are hidden; only the basic time
      and metadata are shared.  The following properties MAY be shared;
      any other properties MUST NOT be shared:

      *  @type

      *  created

      *  due

      *  duration

      *  estimatedDuration

      *  freeBusyStatus

      *  privacy

      *  recurrenceOverrides (Only patches that apply to another
         permissible property are allowed to be shared.)

      *  sequence

      *  showWithoutTime

      *  start

      *  timeZone

      *  timeZones

      *  uid

      *  updated

It should say:

   "private":  The details of the object are hidden; only the basic time
      and metadata are shared.  The following properties MAY be shared;
      any other properties MUST NOT be shared:
 
      *  @type
 
      *  created
 
      *  due
 
      *  duration
 
      *  estimatedDuration
 
      *  excluded
 
      *  excludedRecurrenceRules
 
      *  freeBusyStatus
 
      *  privacy
 
      *  recurrenceId
 
      *  recurrenceIdTimeZone
 
      *  recurrenceOverrides (Only patches that apply to another
         permissible property are allowed to be shared.)
 
      *  recurrenceRules
 
      *  sequence
 
      *  showWithoutTime
 
      *  start
 
      *  timeZone
 
      *  timeZones
 
      *  uid
 
      *  updated

Notes:

Adds the excluded, excludedRecurrenceRules, recurrenceId, recurrenceIdTimeZone and recurrenceRules properties to the list of shared properties of private events.

Only the combination of all recurrence properties allows to generate the full recurrence set for the event.

Omitting the properties was an oversight during the initial publication of this RFC.
```

</details>

<br>**Explanation:**
This is a suggestion or enhancement rather than an inconsistency or underspecification.

---

<details>
<summary><b>Errata 6834</b> from <b>RFC 8995</b> - Bootstrapping Remote Secure Key Infrastructure (BRSKI) (May 2021)</summary>

```
Section 8.5 says:


   *  version

   *  Status

   *  Reason

   *  reason-context

It should say:

   *  version

   *  status

   *  reason

   *  reason-context

Notes:

The CDDL models in section 5.7 and 5.9.4 define the key values with lowercase first character; and the examples in those sections use the same. It seems that during final editing it was forgotten to update Section 8.5.
```

</details>

<br>**Explanation:**
This is from the IANA considerations section.

---

<details>
<summary><b>Errata 6811</b> from <b>RFC 9000</b> - QUIC: A UDP-Based Multiplexed and Secure Transport (May 2021)</summary>

```
Section 5.1.1 says:


                                         The sequence number of the
   initial connection ID is 0.  If the preferred_address transport
   parameter is sent, the sequence number of the supplied connection ID
   is 1.

   Additional connection IDs are communicated to the peer using
   NEW_CONNECTION_ID frames (Section 19.15).  The sequence number on
   each newly issued connection ID MUST increase by 1.  

It should say:

                                         The sequence number of the
   initial connection ID is 0.  If the preferred_address transport
   parameter is sent, the sequence number of the supplied connection ID
   is 1.  The sequence number for NEW_CONNECTION_ID frames starts at 2
   when the preferred_address transport parameter is sent and 1
   otherwise.

   Additional connection IDs are communicated to the peer using
   NEW_CONNECTION_ID frames (Section 19.15).  The sequence number on
   each newly issued connection ID MUST increase by 1.

Notes:

It is not sufficiently clear that the (implied) sequence number for the preferred_address transport parameter is taken from the sequence only when the transport parameter is present.

The original text might be read to imply that the first NEW_CONNECTION_ID frame always starts with 2, though maybe only at a server.  The proposed addition is much more explicit.
```

</details>

<br>**Explanation:**
The correction clarifies the sequence number assignment for both initial and additional connection IDs, ensuring that implementations correctly handle connection ID sequence numbers. However this is only for clarification.

---

<details>
<summary><b>Errata 8042</b> from <b>RFC 9347</b> - Aggregation and Fragmentation Mode for Encapsulating Security Payload (ESP) and Its Use for IP Traffic Flow Security (IP-TFS) (January 2023)</summary>

```
Section 7.2 says:


3-255 	Reserved

It should say:

2-255 	Unassigned

Notes:

The same section, in the previous line, states "1 	Congestion Control Format 	RFC 9347" so 2 is not covered in the registry. It's likely meant to be "Unassigned"?
```

</details>

<br>**Explanation:**
This is from the IANA considerations section.

---

<details>
<summary><b>Errata 7728</b> from <b>RFC 9487</b> - Export of Segment Routing over IPv6 Information in IP Flow Information Export (IPFIX) (November 2023)</summary>

```
Section 5.1.10 says:


5.1.10.  srhSegmentIPv6LocatorLength

   ElementID:  501
   Name:  srhSegmentIPv6LocatorLength
   Data Type Semantics:  default
   Description:  The length of the SRH segment IPv6 locator specified as
      the number of significant bits.  Together with srhSegmentIPv6, it
      enables the calculation of the SRv6 Locator.
   Additional Information:  See Section 3.1 of [RFC8986] for more
      details about the SID format.
   Reference:  RFC 9487

It should say:

5.1.10.  srhSegmentIPv6LocatorLength

   ElementID:  501
   Name:  srhSegmentIPv6LocatorLength
   Abstract Data Type:  unsigned8
   Data Type Semantics:  default
   Description:  The length of the SRH segment IPv6 locator specified as
      the number of significant bits.  Together with srhSegmentIPv6, it
      enables the calculation of the SRv6 Locator.
   Additional Information:  See Section 3.1 of [RFC8986] for more
      details about the SID format.
   Reference:  RFC 9487

Notes:

I'm not an expert on RFC8986, I assumed it's unsigned8 but need help to check this is the case indeed
```

</details>

<br>**Explanation:**
This is from the IANA considerations section.

---

<details>
<summary><b>Errata 7727</b> from <b>RFC 9493</b> - Subject Identifiers for Security Event Tokens (December 2023)</summary>

```
Throughout the document, when it says:


Security Event Identifier Formats

It should say:

Subject Identifier Formats

Notes:

The identifiers described in the RFC are relating to subject fields in Security Event Tokens, and not to the Security Event Tokens as a whole. This is clearly stated in the first sentence of Section 1 (Introduction) and the first sentence of the second paragraph of Section 1 (Introduction).

Therefore, the registry defined in Section 8.1 should be named "Subject Identifier Formats", and not "Security Event Identifier Formats".

Paul Wouters(AD): See https://mailarchive.ietf.org/arch/msg/id-event/-S-MsO2W6PeFF_O5kjP8om-7QNM/
```

</details>

<br>**Explanation:**
This is related to the IANA registry.

---

<details>
<summary><b>Errata 5704</b> from <b>RFC 8586</b> - Loop Detection in Content Delivery Networks (CDNs) (April 2019)</summary>

```
Section 1.2 says:


   This specification uses the Augmented Backus-Naur Form (ABNF)
   notation of [RFC5234] with a list extension, defined in Section 7 of
   [RFC7230], that allows for compact definition of comma-separated
   lists using a '#' operator (similar to how the '*' operator indicates
   repetition).  Additionally, it uses a token (OWS), uri-host, and port
   rules from [RFC7230] and the parameter rule from [RFC7231].

It should say:

   This specification uses the Augmented Backus-Naur Form (ABNF)
   notation of [RFC5234] with a list extension, defined in Section 7 of
   [RFC7230], that allows for compact definition of comma-separated
   lists using a '#' operator (similar to how the '*' operator indicates
   repetition).  Additionally, it uses the token, OWS, uri-host and port
   rules from [RFC7230] and the parameter rule from [RFC7231].

Notes:

The last sentence apparently was mangled during AUTH48. The correct version is from draft-ietf-httpbis-cdn-loop-02. "token", "OWS", "uri-host" and "port" are all ABNF rules.
```

</details>

<br>**Explanation:**
The erratum corrects a grammatical error in Section 1.2 of RFC 8586.  The original text has a poorly phrased sentence regarding ABNF rules, but the correction does not impact the technical specification or implementation in any way.  The error is purely stylistic, therefore it is classified as OTHER.

---

<details>
<summary><b>Errata 6688</b> from <b>RFC 8777</b> - DNS Reverse IP Automatic Multicast Tunneling (AMT) Discovery (April 2020)</summary>

```
Section 5 says:


   +-------+---------------------------------------+
   | 3     | A wire-encoded domain name is present |
   +-------+---------------------------------------+
   | 4-255 | Unassigned                            |
   +-------+---------------------------------------+

      Table 2: Initial Contents of the "Relay Type
                    Field" Registry

   Values 0, 1, 2, and 3 are further explained in Sections 4.2.3 and
   4.2.4.  Relay type numbers 4 through 255 can be assigned with a
   policy of Specification Required (as described in [RFC8126]).

It should say:

   +-------+---------------------------------------+
   | 3     | A wire-encoded domain name is present |
   +-------+---------------------------------------+
   | 4-127 | Unassigned                            |
   +-------+---------------------------------------+

      Table 2: Initial Contents of the "Relay Type
                    Field" Registry

   Values 0, 1, 2, and 3 are further explained in Sections 4.2.3 and
   4.2.4.  Relay type numbers 4 through 127 can be assigned with a
   policy of Specification Required (as described in [RFC8126]).

Notes:

Relay Type is a 7 bit field, the MS bit of the wire-format  octet contains the D-bit.

[Update: 2021-10-05 - AD: Confirmed that you can't fit 8 bits into a 7 bit field - see: https://mailarchive.ietf.org/arch/msg/mboned/cdzHm6Uxwuua5zsOONHtK-RmdU8/ ]
```

</details>

<br>**Explanation:**
This is from the IANA considerations section.

---

<details>
<summary><b>Errata 4354</b> from <b>RFC 7469</b> - Public Key Pinning Extension for HTTP (April 2015)</summary>

```
Section 3 says:


   As in Section 2.4, the token refers to the algorithm name, and the
   quoted-string refers to the base64 encoding of the SPKI Fingerprint.
   When formulating the JSON POST body, the UA MUST either use single-
   quoted JSON strings or use double-quoted JSON strings and backslash-
   escape the embedded double quotes in the quoted-string part of the
   known-pin.

....

      'pin-sha256="d6qzRu9zOECb90Uez27xWltNsj0e1Md7GkYYkVoZWmM="',

It should say:

   As in Section 2.4, the token refers to the algorithm name, and the
   quoted-string refers to the base64 encoding of the SPKI Fingerprint.
   When formulating the JSON POST body, the UA MUST use double-quoted
   JSON strings and backslash-escape the embedded double quotes in the
   quoted-string part of the known-pin.

....

      "pin-sha256=\"d6qzRu9zOECb90Uez27xWltNsj0e1Md7GkYYkVoZWmM=\"",

Notes:

This RFC seems to think that single quotes are permissible in JSON. This is not the case. See http://tools.ietf.org/html/rfc7159#section-7
```

</details>

<br>**Explanation:**
The original text in Section 3 incorrectly states that single-quoted JSON strings are permissible.  This is inconsistent with the JSON specification (RFC 7159).  The inconsistency affects the implementation of the Public Key Pinning Extension, as implementations might incorrectly accept or reject JSON POST bodies based on the use of single quotes, which are invalid according to JSON syntax.  The correction clarifies that only double-quoted strings are permitted, which ensures compliance with the JSON standard and improves interoperability.

---

<details>
<summary><b>Errata 6119</b> from <b>RFC 7155</b> - Diameter Network Access Server Application (April 2014)</summary>

```
Throughout the document, when it says:


[Missing sections when RFC 4005 was obsoleted by RFC 7155]

It should say:

4.7 AVPs Used Only for Compatibility

   The AVPs defined in this section SHOULD only be used for backwards
   compatibility when a Diameter/RADIUS translation function is invoked
   and are not typically originated by Diameter systems during normal
   operations.

                                            +----------+
                                            | AVP Flag |
                                            |  Rules   |
                                            |----+-----|
                                            |MUST| MUST|
   Attribute Name           Section Defined |    |  NOT|
   -----------------------------------------|----+-----|
   Origin-AAA-Protocol      4.7.1           | M  |  V  |
   -----------------------------------------|----+-----|

4.7.1.  Origin-AAA-Protocol

   The Origin-AAA-Protocol AVP (AVP Code 408) is of the type Enumerated
   and should be inserted in a Diameter message translated by a gateway
   system from another AAA protocol, such as RADIUS.  It identifies the
   source protocol of the message to the Diameter system receiving the
   message.

   The supported values are:

         1       RADIUS


Notes:

The description of Origin-AAA-Protocol (AVP Code 408) is missing from RFC 7155. The AVP is documented in RFC 4005 section 9.3.6.

The proposed corrected text contains RFC 4005 section 9.3 as RFC 7155 section 4.7, and RFC 4005 section 9.3.6 as RFC 7155 section 4.7.1. All other AVPs in RFC 4005 section 9.3.x are not listed because they are documented in their relevant standards already.

RFC 7155 is listed as the Reference for Origin-AAA-Protocol in multiple locations in https://www.iana.org/assignments/aaa-parameters/aaa-parameters.xhtml

It appears that there may be an accidental omission of Origin-AAA-Protocol when RFC 7155 obsoleted RFC 4005.

The Origin-AAA-Protocol AVP is referenced in other sections in RFC 7155:
- 3.1.  AA-Request (AAR) Command
- 3.2.  AA-Answer (AAA) Command
- 3.3.  Re-Auth-Request (RAR) Command
- 3.4.  Re-Auth-Answer (RAA) Command
- 3.5.  Session-Termination-Request (STR) Command
- 3.6.  Session-Termination-Answer (STA) Command
- 3.7.  Abort-Session-Request (ASR) Command
- 3.8.  Abort-Session-Answer (ASA) Command
- 3.9.  Accounting-Request (ACR) Command
- 3.10.  Accounting-Answer (ACA) Command
- 5.1.  AA-Request / AA-Answer AVP Table
- 5.2.1.  Framed Access Accounting AVP Table
- 5.2.2.  Non-Framed Access Accounting AVP Table
```

</details>

<br>**Explanation:**
The erratum highlights a missing section in RFC 7155 related to the Origin-AAA-Protocol AVP.  The omission renders the specification incomplete because implementations would lack the necessary information to correctly handle this AVP, which is referenced in multiple sections of RFC 7155.  The reference to this AVP in other sections of RFC 7155 makes it crucial to the overall implementation.

---

<details>
<summary><b>Errata 5768</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section 5. says:


   The Compound MAC computation is as follows:

      CMK = CMK[j]
      Compound-MAC = MAC( CMK, BUFFER )

   where j is the number of the last successfully executed inner EAP
   method, MAC is the MAC function negotiated in TLS 1.2 [RFC5246], and
   BUFFER is created after concatenating these fields in the following
   order:


It should say:

The Compound MAC computation is as follows:

    Compound-MAC = the first 20 octets of MAC( CMK[n], BUFFER )

where n is the number of the last successfully executed inner method, MAC is the MAC function negotiated in TLS (e.g. TLS 1.2 in [RFC5246]), and BUFFER is created after concatenating these fields in the following order:


Notes:

This definition of how Compound MAC is computed is not compatible with the definition of Compound MAC fields in the Crypto-Binding TLV. Those fields have a fixed length of 20 octets based on Section 4.2.13 (and that TLV is claimed to have a fixed length of 76 octets). However, the MAC function negotiated in TLS have variable mac_length (e.g., MAC=SHA256 used HMAC-SHA256 with mac_length=32).

How is this supposed to work? Is Section 4.2.13 wrong in claiming that the Compound MAC fields are 20 octets? Or is Section 5.3 wrong in not specifying MAC() function to truncate the output to 20 octets? One of those need to be changed since the current design would work only with the mac_length=20 case (i.e., MAC=SHA with HMAC-SHA1).

Furthermore, that "TLS 1.2" part should not be hardcoding this to not allow TLS 1.3 or newer versions from being used.

It is also a bit strange to see the BUFFER include "The EAP Type sent by the other party in the first TEAP message." since that can only be EAP Type=TEAP, i.e., 55. If that is indeed a fixed value, it does not seem to add any protection for a negotiated parameter as a part of the crypto binding. Regardless, it would be good to be clearer in the text on how this "EAP Type" is to be encoded here (assumable it is a single octet field with value 0x37).

Paul Wouters(AD): Corrected Text provided by the WG and in 7170bis
```

</details>

<br>**Explanation:**
The errata points out a discrepancy between the length of the Compound MAC (20 octets as defined in Section 4.2.13) and the potentially variable length of the MAC function output in Section 5.  This inconsistency would cause implementations to fail unless the MAC output is truncated to 20 octets, which is not explicitly stated in the original specification. The correction clarifies that only the first 20 octets of the MAC function output are used, thus resolving the inconsistency between Section 4.2.13 and Section 5. The updated version also addresses the limitations in the original text relating to TLS version and EAP type encoding. 

---

<details>
<summary><b>Errata 5775</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section 5. says:


   For authentication methods that generate keying material, further
   protection against man-in-the-middle attacks is provided through
   cryptographically binding keying material established by both TEAP
   Phase 1 and TEAP Phase 2 conversations.  After each successful inner
   EAP authentication, EAP EMSK and/or MSKs are cryptographically
   combined with key material from TEAP Phase 1 to generate a Compound
   Session Key (CMK).  The CMK is used to calculate the Compound MAC as
   part of the Crypto-Binding TLV described in Section 4.2.13, which
   helps provide assurance that the same entities are involved in all
   communications in TEAP.  During the calculation of the Compound MAC,
   the MAC field is filled with zeros.

   The Compound MAC computation is as follows:

      CMK = CMK[j]
      Compound-MAC = MAC( CMK, BUFFER )

   where j is the number of the last successfully executed inner EAP
   method, MAC is the MAC function negotiated in TLS 1.2 [RFC5246], and
   BUFFER is created after concatenating these fields in the following
   order:


It should say:

[Append to the end of section 5.3] 

If no key generating inner method is run then no EMSK or MSK will be generated. If an IMSK needs to be generated then the MSK and therefore the IMSK is set to all zeroes (i.e., IMSK = MSK = 32 octets of 0x00s).

Notes:

Section 5.3 does not describe how CMK is derived for the case where not inner EAP authentication method is executed (e.g., when Basic-Password-Auth is used at TLV level). Section 5.4 seems to address that case by implying that S-IMCK = session_key_seed (S-IMCK[0] does indeed have that value, but MSK/EMSK derivation uses S-IMCK[j], so use of S-IMCK here is slightly misleading). This seems to imply that MSK/EMSK derivation uses S-IMCK[0] and as such, Compound MAC derivation might use CMK[0], but CMK[0] is not defined (Section 5.2 defines CMK[j] for j=1..n-1, but not for j=0.

Furthermore, Section 4.2.13 is not clear on what Flags should be used in Crypto-Binding TLV when no inner EAP authentication method is executed. The only three values defined for Flags (1..3) all imply that either EMSK or MSK (or both) based Compound MAC is present, but there is no inner EAP method MSK/EMSK in this case since no such inner EAP method was executed. Maybe a new Flags value should be defined or alternatively, the MSK Compound MAC case could be extended to cover this no inner-EAP case with CMK[0] defined as proposed above to calculate the MSK Compound MAC.

Paul Wouters(AD): Corrected Text provided by the WG and in 7170bis
```

</details>

<br>**Explanation:**
The erratum points out that Section 5 does not specify how the CMK is derived when no inner EAP authentication method is executed. This omission makes the specification incomplete and ambiguous for implementations that need to handle cases where no key-generating inner method is used.  The lack of clear guidance on CMK derivation in this scenario directly affects the implementation's ability to generate correct Compound MAC values.

---

<details>
<summary><b>Errata 5845</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section 3.3.1 says:


   EAP method messages are carried within EAP-Payload TLVs defined in
   Section 4.2.10.  If more than one method is going to be executed in
   the tunnel, then upon method completion, the server MUST send an
   Intermediate-Result TLV indicating the result.


It should say:

   EAP method messages are carried within EAP-Payload TLVs defined in
   Section 4.2.10.  Upon method completion, the server MUST send an
   Intermediate-Result TLV indicating the result.


Notes:

Description of whether Intermediate-Result TLV is supposed to be used in the case where only a single inner EAP authentication method is used. Section 3.3.1 says "more than one method is going to be executed in the tunnel, then upon method completion, the server MUST send an Intermediate-Result TLV indicating the result", Section 3.3.3 says "The Crypto-Binding TLV and Intermediate-Result TLV MUST be included to perform cryptographic binding after each successful EAP method in a sequence of one or more EAP methods", 4.2.13 says "It MUST be included with the Intermediate-Result TLV to perform cryptographic binding after each successful EAP method in a sequence of EAP methods", Annex C.3 shows an example exchange with a single inner EAP authentication method with use of Intermediate-Result TLV.

It looks like the majority of the places discussion this topic implies that there is going to be an Intermediate-Result TLV after each inner EAP authentication method and the text in 3.3.1 is the only clear case of conflicting (or well, at least misleading if one were to claim it does not explicitly say MUST NOT for the one inner EAP authentication method case). As such, I'd conclude the Intermediate-Result TLV is indeed going to be exchanged after each EAP authentication method and the proposed text change to 3.3.1 covers that.
```

</details>

<br>**Explanation:**
The errata clarifies the use of Intermediate-Result TLVs. The original text in section 3.3.1 implied that Intermediate-Result TLVs are only required when multiple EAP methods are used. However, other sections and examples suggest that these TLVs are required after each EAP method, regardless of the number of methods. This inconsistency is corrected by removing the condition of 'more than one method' from section 3.3.1, making the requirement consistent across the specification.

---

<details>
<summary><b>Errata 6157</b> from <b>RFC 7170</b> - Tunnel Extensible Authentication Protocol (TEAP) Version 1 (May 2014)</summary>

```
Section 4.2.9 says:


  Status

      The Status field is one octet.  This indicates the result if the
      server does not process the action requested by the peer.

It should say:

  Status

      The Status field is one octet.  This indicates the result if the
      party who receives this TLV does not process the action.

Notes:

The status field is carried in the "Request-Action" frame.  As is stated at the start of the section, the frame can be sent either by the server or the peer.
```

</details>

<br>**Explanation:**
The original description of the Status field is ambiguous because it only refers to the server's processing. The correction clarifies that the Status field indicates the result if either the server or the peer does not process the action. This ambiguity impacts implementation, as developers may only consider server-side processing for the Status field, potentially leading to incorrect handling of the field when the peer does not process the action.

---

<details>
<summary><b>Errata 4948</b> from <b>RFC 7252</b> - The Constrained Application Protocol (CoAP) (June 2014)</summary>

```
Section 5.6 says:


For a presented request, a CoAP endpoint MUST NOT use a stored
response, unless:

o  the presented request method and that used to obtain the stored
   response match,

o  all options match between those in the presented request and those
   of the request used to obtain the stored response (which includes
   the request URI), except that there is no need for a match of any
   request options marked as NoCacheKey (Section 5.4) or recognized
   by the Cache and fully interpreted with respect to its specified
   cache behavior (such as the ETag request option described in
   Section 5.10.6; see also Section 5.4.2), and

o  the stored response is either fresh or successfully validated as
   defined below.

The set of request options that is used for matching the cache entry
is also collectively referred to as the "Cache-Key".

It should say:

For a presented request, a CoAP endpoint MUST NOT use a stored
response, unless:

o  the presented request method and that used to obtain the stored
   response match,

o  all options match between those in the presented request and those
   of the request used to obtain the stored response (which includes
   the request URI), except that there is no need for a match of any
   request options marked as NoCacheKey (Section 5.4) or recognized
   by the Cache and fully interpreted with respect to its specified
   cache behavior (such as the ETag request option described in
   Section 5.10.6; see also Section 5.4.2), 

o  the payload of the presented request and the payload of the
   request used to obtain the stored response match, and

o  the stored response is either fresh or successfully validated as
   defined below.

The set of request options that is used for matching the cache entry
plus (if applicable) the request payload are also collectively referred
to as the "Cache-Key".

Notes:

CoAP servers may return error responses in reply to requests that are invalid at the CoAP level (e.g., 4.02 Bad Option if the client includes an unrecognized option) or at the application level above (e.g., 4.00 Bad Request if the client includes a malformed payload according to application semantics).

If the error response does not depend on the request payload, then it is desirable that repeated requests that differ only in the payload can be satisfied with the same cached response. E.g., repeated requests for a non-existing resource should result in a cached 4.04 Not Found response as often as possible, regardless of the payload, rather than hit the server every time.

If the error response depends on the request payload, then it is not desirable that cached responses are reused for repeated requests that differ only in the payload. E.g., a client should not receive an error response for a valid request payload because another client sent an identical request but with a malformed request payload. In this case, including the request payload in the Cache-Key would give the expected result.

The original text does not include the request in the Cache-Key, which may lead to unexpected results. The corrected text changes that.

Since CoAP does not provide any indication in responses to distinguish between the two cases, caches generally cannot determine whether the response depends on the request payload or not and thus must always include the request payload in the Cache-Key to give the expected result. (As an exception, a cache at an origin server may be able to determine whether a cached response depends on the request payload or not, and thus can reuse responses accordingly. This already applies to responses that do not depend on the request method.)
```

</details>

<br>**Explanation:**
The original specification for cache key matching omits the request payload, leading to inconsistencies in handling cached responses.  The correction includes the request payload in the cache key, ensuring consistent behavior in scenarios where the response depends on the payload.  This inconsistency directly affects cache behavior and may lead to unexpected results in implementations that do not consider the payload when generating the cache key.

---

<details>
<summary><b>Errata 4240</b> from <b>RFC 7407</b> - A YANG Data Model for SNMP Configuration (December 2014)</summary>

```
Section 4.8 says:


     augment /snmp:snmp/snmp:target {
       when "snmp:v1 or snmp:v2c";

It should say:

     augment /snmp:snmp/snmp:target {

Notes:

The nodes refered to in the "when" expression do not exist.
(They were there in an early draft version, but when they were moved, we forgot to fix the "when" expression).
```

</details>

<br>**Explanation:**
The original text includes a "when" expression that refers to non-existent nodes. This inconsistency makes the augment statement invalid and will lead to incorrect configuration processing. The correction removes the invalid "when" expression, fixing the inconsistency.

---

<details>
<summary><b>Errata 4673</b> from <b>RFC 7420</b> - Path Computation Element Communication Protocol (PCEP) Management Information Base (MIB) Module (December 2014)</summary>

```
Section 4.1 says:


pcePcepSessState OBJECT-TYPE
       SYNTAX      INTEGER {
                      tcpPending(1),
                      openWait(2),
                      keepWait(3),
                      sessionUp(4)
                   }
       MAX-ACCESS  read-only
       STATUS      current
       DESCRIPTION
           "The current state of the session.

            The set of possible states excludes the idle state since
            entries do not exist in this table in the idle state."
       ::= { pcePcepSessEntry 3 }

It should say:

pcePcepSessState OBJECT-TYPE
       SYNTAX      INTEGER {
		      idle(0),
                      tcpPending(1),
                      openWait(2),
                      keepWait(3),
                      sessionUp(4)
                   }
       MAX-ACCESS  read-only
       STATUS      current
       DESCRIPTION
           "The current state of the session."
       ::= { pcePcepSessEntry 3 }	

Notes:

As per security consideration, if PCE needs to allow incomming connections from only known PCCs. 
Source addresses of PCCs are configured on PCE. If PCEP session on PCE goes down with configured PCCs. 
PCE needs to raise notification pcePcepSessDown (i.e. details mentioned below).
Issue is whiling sending the notification pcePcepSessDown, as session state (pcePcepSessState) defined in RFC doesn't include idle state.
I suggest to include idle(0) state for pcePcepSessState. 


   pcePcepSessDown NOTIFICATION-TYPE
       OBJECTS     {
                      pcePcepSessState,
                      pcePcepSessStateLastChange
                   }
       STATUS      current
       DESCRIPTION
           "This notification is sent when the value of
            pcePcepSessState leaves the sessionUp state."
       ::= { pcePcepNotifications 2 }
```

</details>

<br>**Explanation:**
The original specification omits the "idle" state, while the description mentions it and the notification pcePcepSessDown requires it.  This inconsistency leads to incorrect behavior when transitioning to an idle state, as the MIB doesn't have a way to represent the state before the session is established.  The correction adds the "idle" state, resolving the inconsistency.

---

<details>
<summary><b>Errata 5554</b> from <b>RFC 7432</b> - BGP MPLS-Based Ethernet VPN (February 2015)</summary>

```
Section 7 says:


Clarifications to following sub-sections:
Section 7.1
Section 7.2
Section 7.5


It should say:

Section 7.1:
Add below text to the section 7.1 regarding the encoding
of MPLS label field:

"The value of the 20-bit MPLS label is encoded in the high-order 
20 bits of the 3 octets MPLS Label field."

Section 7.2:
Add below text to the section 7.2 regarding the encoding 
of both the MPLS label fields:

"The value of the 20-bit MPLS label is encoded in the high-order
20 bits of the 3 octets MPLS Label1 and MPLS Label2 fields."

Section 7.5:
Add below text to the section 7.5 regarding the encoding of 
ESI Label field:

"The value of the 20-bit MPLS label is encoded in the high-order
20 bits of the 3 octets ESI Label field."


Notes:

MPLS label is a 20-bit value and is stored in a 3 bytes field in a packet. 
The 20-bit MPLS label value is generally stored in higher order 20 bits 
of the 3 octet label field. The exact encoding to be followed for storing 
MPLS label values are not explicitly mentioned in the RFC 7432 under 
section 7.1, 7.2 and 7.5 for different types of EVPN routes. This lead to
ambiguity in different  implementations. Hence a clarification is required.
```

</details>

<br>**Explanation:**
The original specification lacks explicit details on the encoding of MPLS label values within 3-octet fields. The lack of this information leads to ambiguity in implementations, resulting in different interpretations of the encoding.  The erratum's suggested additions address this incompleteness, making the specification more precise and improving interoperability.

---

<details>
<summary><b>Errata 4725</b> from <b>RFC 7574</b> - Peer-to-Peer Streaming Peer Protocol (PPSPP) (July 2015)</summary>

```
Section 5 says:


PPSPP can use different methods for protecting the integrity of the
content while it is being distributed via the peer-to-peer network.
More specifically, PPSPP can use different methods for receiving
peers to detect whether a requested chunk has been maliciously
modified by the sending peer. In benign environments, content
integrity protection can be disabled.

For static content, PPSPP currently defines one method for protecting
integrity, called the Merkle Hash Tree scheme. If PPSPP operates
over the Internet, this scheme MUST be used. If PPSPP operates in a
benign environment, this scheme MAY be used. So the scheme is
mandatory to implement, to satisfy the requirement of strong security
for an IETF protocol [RFC3365]. An extended version of the scheme is
used to efficiently protect dynamically generated content (live
streams), as explained below and in Section 6.1.

It should say:

PPSPP can use different methods for protecting the integrity of the
content while it is being distributed via the peer-to-peer network.
More specifically, PPSPP can use different methods for receiving
peers to detect whether a requested chunk has been maliciously
modified by the sending peer.

For static content, PPSPP currently defines one method for protecting
integrity, called the Merkle Hash Tree scheme.
The scheme is mandatory to implement, to satisfy the requirement of 
strong security for an IETF protocol [RFC3365]. An extended version
of the scheme is used to efficiently protect dynamically generated
content (live streams), as explained below and in Section 6.1.

Notes:

RFC 7574 (PPSP-PP) defines how the peers exchange chunks regarding content integrity protection scheme. It describes the relationship of the DATA and INTEGRITY messages.
But, it does not describes how peers exchange chunks when the content integrity protection scheme is disabled.
Thus, to the readers, it seems that content integrity protection scheme is very important part of PPSP-PP and must be used in order to implement PPSP-PP.
I think the RFC 7574 (PPSP-PP) should be changed to clearly express that the content integrity protection scheme must be used in PPSP-PP.
The proposed changes is to remove options regarding the use of content integrity protection.

Spencer: confirmed in conversations with Victor Grishchenko <victor.grishchenko@gmail.com> on the PPSP mailing list.
```

</details>

<br>**Explanation:**
The RFC does not mention what has to be done in cases other than the two cases mentioned. The clarification states that there is no other case by mandating the scheme.

---

<details>
<summary><b>Errata 4726</b> from <b>RFC 7574</b> - Peer-to-Peer Streaming Peer Protocol (PPSPP) (July 2015)</summary>

```
Section 6.1 says:


In the "Unified Merkle Tree" method, PPSPP combines the Merkle Hash
Tree scheme for static content with signatures to unify the video-on-
demand and live streaming scenarios. The use of Merkle hash trees
reduces the number of signing and verification operations, hence
providing a similar signature amortization to the approach described
in [SIGMCAST]. If PPSPP operates over the Internet, the "Unified
Merkle Tree" method MUST be used. If the protocol operates in a
benign environment, the "Unified Merkle Tree" method MAY be used. So
this method is mandatory to implement.

It should say:

In the "Unified Merkle Tree" method, PPSPP combines the Merkle Hash
Tree scheme for static content with signatures to unify the video-on-
demand and live streaming scenarios. The use of Merkle hash trees
reduces the number of signing and verification operations, hence
providing a similar signature amortization to the approach described
in [SIGMCAST].

Notes:

RFC 7574 (PPSP-PP) defines how the peers exchange chunks regarding content integrity protection scheme. It describes the relationship of the DATA and INTEGRITY messages.
But, it does not describes how peers exchange chunks when the content integrity protection scheme is disabled.
Thus, to the readers, it seems that content integrity protection scheme is very important part of PPSP-PP and must be used in order to implement PPSP-PP.
I think the RFC 7574 (PPSP-PP) should be changed to clearly express that the content integrity protection scheme must be used in PPSP-PP.
The proposed changes is to remove options regarding the use of content integrity protection.

Spencer: confirmed in conversations with Victor Grishchenko <victor.grishchenko@gmail.com> on the PPSP mailing list.
```

</details>

<br>**Explanation:**
The RFC does not mention what has to be done in cases other than the two cases mentioned. The clarification states that there is no other case by mandating the scheme.

---

<details>
<summary><b>Errata 4413</b> from <b>RFC 7584</b> - Session Traversal Utilities for NAT (STUN) Message Handling for SIP Back-to-Back User Agents (B2BUAs) (July 2015)</summary>

```
Section 4.4 says:


   Because of forking, a B2BUA might receive multiple answers for a
   single outbound INVITE.  When this occurs, the B2BUA SHOULD follow
   Sections 3.2 or 3.3 for all of those received answers.

It should say:

   Because of forking, a B2BUA might receive multiple answers for a
   single outbound INVITE.  When this occurs, the B2BUA SHOULD follow
   Sections 4.2 or 4.3 for all of those received answers.

Notes:

Sections 3.2 and 3.3 do not exist.  The normative statement should indicate sections 4.2 and 4.3.
```

</details>

<br>**Explanation:**
The original text refers to non-existent sections (3.2 and 3.3) for handling multiple INVITE answers. The correction points to the correct sections (4.2 and 4.3), resolving the inconsistency. This inconsistency would mislead implementations attempting to correctly handle multiple INVITE answers.

---

<details>
<summary><b>Errata 4509</b> from <b>RFC 7630</b> - HMAC-SHA-2 Authentication Protocols in the User-based Security Model (USM) for SNMPv3 (October 2015)</summary>

```
Section 8 and 10 says:


snmpModules 235

It should say:

mib-2 235

Notes:

IANA registered snmpUsmHmacSha2MIB under mib-2.235 (as advised by the MIB doctors), but the document mentions snmpModules.235
```

</details>

<br>**Explanation:**
The original text uses the incorrect module name `snmpModules` when referring to the IANA-registered MIB. The correct module name should be `mib-2`, reflecting the actual location of the MIB in the IANA registry. This inconsistency between the text and the actual MIB location could lead to incorrect implementation.

---

<details>
<summary><b>Errata 4938</b> from <b>RFC 7714</b> - AES-GCM Authenticated Encryption in the Secure Real-time Transport Protocol (SRTP) (December 2015)</summary>

```
Section 11 says:


A Key Derivation Function (KDF) is used to derive all of the required
encryption and authentication keys from a secret value shared by the
endpoints.  The AEAD_AES_128_GCM algorithm MUST use the (128-bit)
AES_CM PRF KDF described in [RFC3711].  AEAD_AES_256_GCM MUST use the
AES_256_CM_PRF KDF described in [RFC6188].

It should say:

A Key Derivation Function (KDF) is used to derive all of the required
encryption and authentication keys from a secret value shared by the
endpoints.  The AEAD_AES_128_GCM algorithm MUST use the (128-bit)
AES_CM PRF KDF described in [RFC3711].  AEAD_AES_256_GCM MUST use the
AES_256_CM_PRF KDF described in [RFC6188].  Since the KDF functions in
those RFCs assume as input a 112-bit master salt, the 96-bit master
salt specified in this document must be multiplied by 2^16 to form the
112-bit salt used as the master salt in those key derivation functions.

Notes:

The salt specified in RFC 7714 is 96 bits in length, but intended for use in KDF functions defined in RFC 3711.  This led to different interpretations when implementing this RFC.  A more complete description was presented on the avtcore mailing list (https://mailarchive.ietf.org/arch/msg/avt/IRfLuNKglD3qhqwSz3v3t0CG6fA) and, after some dialog, there seemed to be agreement to adopt the approach most widely implemented (https://mailarchive.ietf.org/arch/msg/avt/-C1cIWQXpyzS2KfBjGR6B2kK92w).  This suggested text is intended to reflect that agreement.  In effect, 16 zero bits are padded to the right of the salt value  defined in RFC 7714 (creating a 112 bit salt value) before it is used as described in the KDF functions defined in RFC 3711 that require a 112 bit salt value.
```

</details>

<br>**Explanation:**
The original text does not specify how to handle the 96-bit master salt defined in RFC 7714 with the 112-bit master salt assumed by the KDF functions in RFC 3711. The correction clarifies that the 96-bit salt must be multiplied by 2^16 to create a 112-bit salt, resolving the inconsistency.

---

<details>
<summary><b>Errata 5540</b> from <b>RFC 7728</b> - RTP Stream Pause and Resume (February 2016)</summary>

```
Section 8.2.  PAUSED says:


   PAUSED SHALL contain a fixed-length 32-bit parameter at the start of
   the Type Specific field with the extended RTP sequence number of the
   last RTP packet sent before the RTP stream was paused, in the same
   format as the extended highest sequence number received
   (Section 6.4.1 of [RFC3550]).

It should say:

   PAUSED SHALL contain a fixed-length 32-bit parameter at the start of
   the Type Specific field with the extended RTP sequence number of the
   last RTP packet sent before the RTP stream was paused, in the same
   format as the extended highest sequence number received
   (Section 6.4.1 of [RFC3550]), or, if no packet has been sent, the
   value one less than the sequence number that will be chosen for the
   next packet sent (modulo 2^32).

Notes:

The paragraph leaves the value of the parameter undefined when the stream is paused before any data has been sent.
```

</details>

<br>**Explanation:**
The original specification does not define the value of the 32-bit parameter in the PAUSED message when no RTP packets have been sent before pausing.  This under-specification leads to ambiguity in implementations and potential interoperability issues. The correction clarifies the value to be used in this scenario.

---

<details>
<summary><b>Errata 4794</b> from <b>RFC 7950</b> - The YANG 1.1 Data Modeling Language (August 2016)</summary>

```
Section 7.21.5 says:


   o  If the "when" statement is a child of an "augment" statement, then
      the context node is the augment's target node in the data tree, if
      the target node is a data node.  Otherwise, the context node is
      the closest ancestor node to the target node that is also a data
      node.  If no such node exists, the context node is the root node.
      The accessible tree is tentatively altered during the processing
      of the XPath expression by removing all instances (if any) of the
      nodes added by the "augment" statement.


It should say:

   o  If the "when" statement is a child of an "augment" statement, then
      the context node is the augment's target node in the data tree, if
      the target node is a data node, rpc, action or notification.
      Otherwise, the context node is the closest ancestor node to the
      target node that is also a data node, rpc, action or notification.
      If no such node exists, the context node is the root node. The
      accessible tree is tentatively altered during the processing of
      the XPath expression by removing all instances (if any) of the
      nodes added by the "augment" statement.


Notes:

If the target node of an "augment" is inside an rpc, action or notification, the context node also needs to be inside that rpc, action or notification. For example, if the target node is the "input" node of an action, the context node should be the action node, not the data node for which the action is defined as the original text implies. This is also in accordance with the definition of the accessible tree in Sec. 6.4.1.
```

</details>

<br>**Explanation:**
The original description of context node selection for "when" statements within "augment" statements incorrectly limits the context node to only data nodes. The correction extends the selection to also include rpc, action, and notification nodes, making it consistent with the definition of the accessible tree and ensuring that "when" statements within "augment" statements function correctly when the target node is within an rpc, action, or notification.

---

<details>
<summary><b>Errata 4916</b> from <b>RFC 7950</b> - The YANG 1.1 Data Modeling Language (August 2016)</summary>

```
Section 7.17. says:


If the target node is a container, list, case, input, output, or
notification node, the "container", "leaf", "list", "leaf-list",
"uses", and "choice" statements can be used within the "augment"
statement.

It should say:

If the target node is a container, list, case, input, output, or
notification node, the "anydata", "anyxml", "container", "leaf",
"list", "leaf-list", "uses", and "choice" statements can be used
within the "augment" statement.

Notes:

It was forgotten to mention "anydata" and "anyxml" as valid substatements in this case.
```

</details>

<br>**Explanation:**
The original text omits "anydata" and "anyxml" statements from the list of allowed substatements within an "augment" statement when the target node is a container, list, case, input, output, or notification node.  This omission creates an inconsistency because "anydata" and "anyxml" are valid substatements in this context.  The correction adds these statements to the list, resolving the inconsistency.

---

<details>
<summary><b>Errata 5807</b> from <b>RFC 7950</b> - The YANG 1.1 Data Modeling Language (August 2016)</summary>

```
Section 7.21.5. says:


   o  If the "when" statement is a child of a "uses", "choice", or
      "case" statement, then the context node is the closest ancestor
      node to the node with the "when" statement that is also a data
      node.  If no such node exists, the context node is the root node.
      The accessible tree is tentatively altered during the processing
      of the XPath expression by removing all instances (if any) of the
      nodes added by the "uses", "choice", or "case" statement.

It should say:

   o  If the "when" statement is a child of a "uses", "choice", or
      "case" statement, then the context node is the closest ancestor
      node to the node with the "when" statement that is also a data
      node, rpc, action or notification.  If no such node exists, the
      context node is the root node. The accessible tree is tentatively
      altered during the processing of the XPath expression by removing
      all instances (if any) of the nodes added by the "uses",
      "choice", or "case" statement.

Notes:

Similar to verified errata 4794 (https://www.rfc-editor.org/errata/eid4794) but covers the "uses", "choice" and "case" corner case (instead of "augment"). If the node for which the "when" statement is defined is within an rpc, action or notification, the context node also needs to be inside that rpc, action or notification. There are published IETF modules, which rely on this to be true, such as "ietf-netconf-nmda@2019-01-07" in RFC8526 (https://tools.ietf.org/html/rfc8526) at schema node id "/ncds:get-data/ncds:input/ncds:origin-filters". Original text assigns the context node to the root node, if no data node ancestor is found. "rpc", "action" and "notification" are not data nodes and are represented by nodes that are descendants of the root node, as described in Section 6.4.1.
```

</details>

<br>**Explanation:**
The original description of context node selection for "when" statements within "uses", "choice", or "case" statements incorrectly limits the context node to only data nodes. The correction extends the selection to also include rpc, action, and notification nodes, ensuring that "when" statements within "uses", "choice", or "case" statements function correctly when the target node is within an rpc, action, or notification.

---

<details>
<summary><b>Errata 5583</b> from <b>RFC 7970</b> - The Incident Object Description Exchange Format Version 2 (November 2016)</summary>

```
Section 8 says:


    <xs:simpleType name="action-type">
      <xs:restriction base="xs:NMTOKEN">
        <xs:enumeration value="nothing"/>
        <xs:enumeration value="contact-source-site"/>
        <xs:enumeration value="contact-target-site"/>
        <xs:enumeration value="contact-sender"/>
        <xs:enumeration value="investigate"/>
        <xs:enumeration value="block-host"/>
        <xs:enumeration value="block-network"/>
        <xs:enumeration value="block-port"/>
        <xs:enumeration value="rate-limit-host"/>
        <xs:enumeration value="rate-limit-network"/>
        <xs:enumeration value="rate-limit-port"/>
        <xs:enumeration value="redirect-traffic"/>
        <xs:enumeration value="honeypot"/>
        <xs:enumeration value="upgrade-software"/>
        <xs:enumeration value="rebuild-asset"/>
        <xs:enumeration value="harden-asset"/>
        <xs:enumeration value="remediate-other"/>
        <xs:enumeration value="status-triage"/>
        <xs:enumeration value="status-new-info"/>
        <xs:enumeration value="watch-and-report"/>
        <xs:enumeration value="defined-coa"/>

It should say:

    <xs:simpleType name="action-type">
      <xs:restriction base="xs:NMTOKEN">
        <xs:enumeration value="nothing"/>
        <xs:enumeration value="contact-source-site"/>
        <xs:enumeration value="contact-target-site"/>
        <xs:enumeration value="contact-sender"/>
        <xs:enumeration value="investigate"/>
        <xs:enumeration value="block-host"/>
        <xs:enumeration value="block-network"/>
        <xs:enumeration value="block-port"/>
        <xs:enumeration value="rate-limit-host"/>
        <xs:enumeration value="rate-limit-network"/>
        <xs:enumeration value="rate-limit-port"/>
        <xs:enumeration value="redirect-traffic"/>
        <xs:enumeration value="honeypot"/>
        <xs:enumeration value="upgrade-software"/>
        <xs:enumeration value="rebuild-asset"/>
        <xs:enumeration value="harden-asset"/>
        <xs:enumeration value="remediate-other"/>
        <xs:enumeration value="status-triage"/>
        <xs:enumeration value="status-new-info"/>
        <xs:enumeration value="watch-and-report"/>
        <xs:enumeration value="training"/>
        <xs:enumeration value="defined-coa"/>

Notes:

The narrative text in Section 3.1.5 defined an enumerated value of "training" for the action attribute, but the schema omitted it.
```

</details>

<br>**Explanation:**
The original schema definition for the action-type is missing the "training" enumeration value, which is defined in the narrative text. This inconsistency needs to be corrected to ensure that implementations correctly parse and generate the action attribute.

---

<details>
<summary><b>Errata 6472</b> from <b>RFC 8175</b> - Dynamic Link Exchange Protocol (DLEP) (June 2017)</summary>

```
Section 12.4, para 2 says:


A Peer Offer Signal MUST be encoded within a UDP packet.  The IP source and destination fields in the packet MUST be set by swapping the values received in the Peer Discovery Signal.  The Peer Offer Signal completes the discovery process; see Section 7.1.

It should say:

A Peer Offer Signal MUST be encoded within a UDP packet. The IP source and destination fields (addresses and ports) in the packet MUST be set by swapping the values received in the Peer Discovery Signal, with the exception that the new source address on the Offer Signal, which was the well-known destination address, becomes a local IP from the DLEP modem. The source port remains the well-known port from the Peer Discovery Signal. The Peer Offer signal contains zero or more connection points as described in 13.2 and 13.3 completes the discovery process; see Section 7.1 

Notes:

The original text will not result in a valid unicast IP packet.

=====
AD Note:  The original text is clearly wrong.  There has been discussion in the WG about the proper wording for the "corrected text".  Given that the current text results in an invalid packet, I am marking this report as Verified.

https://mailarchive.ietf.org/arch/msg/manet/h8Sa924gn6ZmAZ7XNp-5UUrZlAY/
```

</details>

<br>**Explanation:**
The original text describes swapping IP source and destination addresses without specifying how to handle the source address in the Peer Offer Signal, resulting in an invalid packet. The correction clarifies that the source address should be set to a local IP address from the DLEP modem instead of simply swapping with the destination address, resolving the inconsistency.

---

<details>
<summary><b>Errata 7239</b> from <b>RFC 8182</b> - The RPKI Repository Delta Protocol (RRDP) (July 2017)</summary>

```
Section 3.2 says:


Certificate Authorities that use RRDP MUST include an instance of an
SIA AccessDescription extension in resource certificates they
produce, in addition to the ones defined in [RFC6487]:

It should say:

Certificate Authorities that use RRDP MUST include an instance of an
SIA AccessDescription extension in CA resource certificates they
produce, in addition to the ones defined in [RFC6487]:

Notes:

Between draft-ietf-sidr-delta-protocol-04 and draft-ietf-sidr-delta-protocol-05 a bit of text was removed (perhaps because it was considered redundant). But, unfortunately that snippet helped establish important context as to what types of certificates are expected to contain the id-ad-rpkiNotify accessMethod inside the Subject Information Access extension. The text that was removed:

"""
Relying Parties that do not support this delta protocol MUST MUST NOT
reject a CA certificate merely because it has an SIA extension
containing this new kind of AccessDescription.
"""

From the removed text is is clear that id-ad-rpkiNotify was only expected to show up on CA certificates. However, without the above text, Section 3.2 of RFC 8182 is somewhat ambiguous whether 'resource certificates' is inclusive of EE certificates or not.

RFC 6487 Section 4.8.8.2 sets expectations that only id-ad-signedObject is expected to show up in the SIA of EE certificates "Other AccessMethods MUST NOT be used for an EE certificates's SIA."

The ambiguity in RFC8182 led to one RIR including id-ad-rpkiNotify in the SIA of the EE certificate of all signed objects they produce (such as ROAs). The RIR indicated they'll work to remove id-ad-rpkiNotify from all EE certificates their CA implementation produces.

It should be noted that the presence of id-ad-rpkiNotify in EE certificates is superfluous; Relying Parties can't use the rpkiNotify accessMethod in EE certificates for any purpose in the validation decision tree.

(Verifying this Errata does not block a future transition from rsync to https; as RFC6487 Section 4.8.8.2 leaves room for additional instances of id-ad-signedObject with non-rsync URIs)
```

</details>

<br>**Explanation:**
The original text is ambiguous about whether the SIA extension containing the id-ad-rpkiNotify accessMethod should be included in all resource certificates or only in CA certificates.  This ambiguity led to different interpretations and implementations.  The corrected text clarifies that it only applies to CA certificates, removing the ambiguity and promoting consistency.

---

<details>
<summary><b>Errata 6301</b> from <b>RFC 8281</b> - Path Computation Element Communication Protocol (PCEP) Extensions for PCE-Initiated LSP Setup in a Stateful PCE Model (December 2017)</summary>

```
Section 5.1 says:


     <PCE-initiated-lsp-request> ::= (<PCE-initiated-lsp-instantiation>|
                                      <PCE-initiated-lsp-deletion>)

     <PCE-initiated-lsp-instantiation> ::= <SRP>
                                           <LSP>
                                           [<END-POINTS>]
                                           <ERO>
                                           [<attribute-list>]

     <PCE-initiated-lsp-deletion> ::= <SRP>
                                      <LSP>


It should say:

     <PCE-initiated-lsp-request> ::= (<PCE-initiated-lsp-instantiation>|
                                      <PCE-initiated-lsp-deletion-or-reclamation>)

     <PCE-initiated-lsp-instantiation> ::= <SRP>
                                           <LSP>
                                           [<END-POINTS>]
                                           <ERO>
                                           [<attribute-list>]

     <PCE-initiated-lsp-deletion-or-reclamation> ::= <SRP>
                                                     <LSP>


Notes:

Update needed to solve ambiguity for any extra object included after SRP and LSP objects in reclaim delegation request, which is coming from:

https://tools.ietf.org/html/rfc8281#section-6
A PCE (either the original or one of its backups) sends a PCInitiate
   message that includes just the SRP and LSP objects and carries the
   PLSP-ID of the LSP it wants to take control of.
```

</details>

<br>**Explanation:**
The original specification is ambiguous about the content of PCE-initiated-lsp-deletion requests.  The correction introduces a new production, <PCE-initiated-lsp-deletion-or-reclamation>, to clarify that both deletion and reclamation requests can include additional objects beyond SRP and LSP.

---

<details>
<summary><b>Errata 5638</b> from <b>RFC 8360</b> - Resource Public Key Infrastructure (RPKI) Validation Reconsidered (April 2018)</summary>

```
Section 4.2.4.4 says:


   7.  Compute the VRS-IP and VRS-AS set values as indicated below:

       *  If the IP Address Delegation extension is present in
          certificate x and x=1, set the VRS-IP to the resources found
          in this extension.

       *  If the IP Address Delegation extension (...)

       *  If the IP Address Delegation extension (...)

       *  If the IP Address Delegation extension is present in
          certificate x and x=1, set the VRS-IP to the resources found
          in this extension.

       *  If the AS Identifier Delegation extension (...)

       *  If the AS Identifier Delegation extension (...)

It should say:

   7.  Compute the VRS-IP and VRS-AS set values as indicated below:

       *  If the IP Address Delegation extension is present in
          certificate x and x=1, set the VRS-IP to the resources found
          in this extension.

       *  If the IP Address Delegation extension (...)

       *  If the IP Address Delegation extension (...)

       *  If the AS Identifier Delegation extension is present in
          certificate x and x=1, set the VRS-AS to the resources found
          in this extension.

       *  If the AS Identifier Delegation extension (...)

       *  If the AS Identifier Delegation extension (...)

Notes:

There seems to be a copy-paste error.

There are two bullet points explaining the initialization of VRS-IP, and none explaining the initialization of VRS-AS.

All the evidence suggests that the two extensions (IP Address Delegation and AS Identifier Delegation) are meant to be handled similarly, so I believe that the last three bullet points are supposed to perfectly mirror the first three.
```

</details>

<br>**Explanation:**
The original text contains duplicate bullet points for handling the IP Address Delegation extension and omits the corresponding handling for the AS Identifier Delegation extension. The correction replaces one set of duplicate bullet points with the correct handling for the AS Identifier Delegation extension, resolving the inconsistency.

---

<details>
<summary><b>Errata 6263</b> from <b>RFC 8410</b> - Algorithm Identifiers for Ed25519, Ed448, X25519, and X448 for Use in the Internet X.509 Public Key Infrastructure (August 2018)</summary>

```
Section 7 says:


NOTE: There exist some private key import functions that have not picked up the new ASN.1 structure OneAsymmetricKey that is defined in [RFC7748].

It should say:

NOTE: There exist some private key import functions that have not picked up the new ASN.1 structure OneAsymmetricKey that is defined in [RFC5958].

Notes:

RFC7748 does not define or even mention OneAsymmetricKey. The correct reference should be RFC5958 "Asymmetric Key Packages"
```

</details>

<br>**Explanation:**
The original text incorrectly cites RFC 7748 as the source for the OneAsymmetricKey ASN.1 structure.  The correction cites RFC 5958, which is the correct source. This inconsistency would affect those trying to locate the correct ASN.1 definition.

---

<details>
<summary><b>Errata 7384</b> from <b>RFC 8410</b> - Algorithm Identifiers for Ed25519, Ed448, X25519, and X448 for Use in the Internet X.509 Public Key Infrastructure (August 2018)</summary>

```
Section 9 says:


    sa-Ed25519 SIGNATURE-ALGORITHM ::= {
       IDENTIFIER id-Ed25519
        PARAMS ARE absent
        PUBLIC-KEYS {pk-Ed25519}
        SMIME-CAPS { IDENTIFIED BY id-Ed25519 }
    }

    pk-Ed25519 PUBLIC-KEY ::= {
        IDENTIFIER id-Ed25519
        -- KEY no ASN.1 wrapping --
        PARAMS ARE absent
        CERT-KEY-USAGE {digitalSignature, nonRepudiation,
                        keyCertSign, cRLSign}
        PRIVATE-KEY CurvePrivateKey
    }

It should say:

    sa-Ed25519 SIGNATURE-ALGORITHM ::= {
       IDENTIFIER id-Ed25519
        PARAMS ARE absent
        PUBLIC-KEYS {pk-Ed25519}
        SMIME-CAPS { IDENTIFIED BY id-Ed25519 }
    }

    pk-Ed25519 PUBLIC-KEY ::= {
        IDENTIFIER id-Ed25519
        -- KEY no ASN.1 wrapping --
        PARAMS ARE absent
        CERT-KEY-USAGE {digitalSignature, nonRepudiation,
                        keyCertSign, cRLSign}
        PRIVATE-KEY CurvePrivateKey
    }

   sa-Ed448 SIGNATURE-ALGORITHM ::= {
      IDENTIFIER id-Ed448
       PARAMS ARE absent
       PUBLIC-KEYS {pk-Ed448}
       SMIME-CAPS { IDENTIFIED BY id-Ed448 }
   }

   pk-Ed448 PUBLIC-KEY ::= {
       IDENTIFIER id-Ed448
       -- KEY no ASN.1 wrapping --
       PARAMS ARE absent
       CERT-KEY-USAGE {digitalSignature, nonRepudiation,
                       keyCertSign, cRLSign}
       PRIVATE-KEY CurvePrivateKey
   }

Notes:

The definitions for sa-Ed448 and pk-Ed448 are missing from RFC 8410.
```

</details>

<br>**Explanation:**
The original specification omits the definitions for sa-Ed448 and pk-Ed448, while the description implies that these should be included.  This omission creates an inconsistency, because the definitions are necessary for complete support of Ed448 signatures and keys.  The correction adds these definitions, resolving the inconsistency.

---

<details>
<summary><b>Errata 5868</b> from <b>RFC 8446</b> - The Transport Layer Security (TLS) Protocol Version 1.3 (August 2018)</summary>

```
Section 4.2.3 says:


   ECDSA algorithms:  Indicates a signature algorithm using ECDSA
      [ECDSA], the corresponding curve as defined in ANSI X9.62 [ECDSA]
      and FIPS 186-4 [DSS], and the corresponding hash algorithm as
      defined in [SHS].  The signature is represented as a DER-encoded
      [X690] ECDSA-Sig-Value structure.

It should say:

   ECDSA algorithms:  Indicates a signature algorithm using ECDSA
      [ECDSA], the corresponding curve as defined in ANSI X9.62 [ECDSA]
      and FIPS 186-4 [DSS], and the corresponding hash algorithm as
      defined in [SHS].  The signature is represented as a DER-encoded
      [X690] ECDSA-Sig-Value structure as defined in [RFC4492].

Notes:

There is a possibility for confusion as the ECDSA-Sig-Value has two conflicting definitions in authoritative standards. TLS always used the following (see RFC4492):

   ECDSA-Sig-Value ::= SEQUENCE {
     r  INTEGER,
     s  INTEGER
   }

but the publicly accessible SECG SEC1 v2.0 (https://www.secg.org/sec1-v2.pdf) defines it like this:

ECDSA-Sig-Value ::= SEQUENCE {
 r INTEGER,
 s INTEGER,
 a INTEGER OPTIONAL,
 y CHOICE { b BOOLEAN, f FieldElement } OPTIONAL
}

I think using the RFC5480 in the Corrected Text would be cleaner than RFC4492, but the former is not an existing reference, so we would need to update section 12 also.
```

</details>

<br>**Explanation:**
The original description of ECDSA signature representation is ambiguous as the ECDSA-Sig-Value structure has multiple definitions. The corrected description explicitly specifies that the signature must be represented as a DER-encoded ECDSA-Sig-Value structure as defined in RFC 4492, resolving the ambiguity and ensuring consistency.

---

<details>
<summary><b>Errata 6123</b> from <b>RFC 8446</b> - The Transport Layer Security (TLS) Protocol Version 1.3 (August 2018)</summary>

```
Section 2 says:


The handshake protocol allows peers to negotiate a protocol version, select cryptographic algorithms, optionally authenticate each other, and establish shared secret keying material.

Notes:

Only client authentication is optional (albeit, server authentication is implicit for PSK-only key exchange mode)

Paul Wouters(AD): corrected with the following text:

The handshake protocol allows peers to negotiate a protocol version, select cryptographic algorithms, authenticate each other (with client authentication being optional), and establish shared secret keying material.
```

</details>

<br>**Explanation:**
The original description is imprecise about the optionality of authentication.  The corrected text clarifies that client authentication is optional, but server authentication is generally required. This is a clarification rather than a correction of an error affecting implementation.

---

<details>
<summary><b>Errata 7303</b> from <b>RFC 8446</b> - The Transport Layer Security (TLS) Protocol Version 1.3 (August 2018)</summary>

```
Section 6.1 says:


This alert notifies the recipient that the sender will not send any more messages on this connection. 

It should say:

This alert notifies the recipient that the sender will not send any more messages on this connection. close_notify alerts should be sent with a severity level of WARNING.

Notes:

Apparently, TLS/1.0 specified these should be set to WARNING, not FATAL, but this text got lost somewhere along the way. https://github.com/pion/dtls/issues/195

OpenSSL/NSS both send as WARNING, and servers that have tried sending as FATAL have encountered compatibility problems with clients which treat FATAL alerts differently than WARNING alerts: e.g. https://source.chromium.org/chromium/chromium/src/+/main:third_party/boringssl/src/ssl/tls_record.cc;l=591;drc=c0872c02015009bf3dbab0a83c0452d141e8e9cf?q=tls_open_record&ss=chromium%2Fchromium%2Fsrc

Paul Wouters(AD): Resolved but with the following Corrected Text:

close_notify:  This alert notifies the recipient that the sender will not send any more messages on this connection.  Any data received after a closure alert has been received MUST be ignored. This alert MUST be sent with AlertLevel=warning.
```

</details>

<br>**Explanation:**
The original text does not specify the severity level for close_notify alerts, while the corrected text specifies that close_notify alerts MUST be sent with a severity level of WARNING. This inconsistency may lead to interoperability issues between implementations that treat alerts with different severity levels differently.

---

<details>
<summary><b>Errata 7250</b> from <b>RFC 8446</b> - The Transport Layer Security (TLS) Protocol Version 1.3 (August 2018)</summary>

```
Section 4.6.1 says:


   The client MAY use this PSK for future handshakes by including the
   ticket value in the "pre_shared_key" extension in its ClientHello
   (Section 4.2.11).

It should say:

(to add)

  Where the client does not support session tickets, this extension MUST be ignored.

Notes:

I've seen a TLS implementation which doesn't implement session tickets.  That's fine, but the implementation doesn't *ignore* session tickets it receives.  Instead, it treats reception of the ticket as un recoverable error, and drops the TLS connection.

It's also worth adding a note to section 4.2 at the bottom of page 38.  To note that in general, f an extension isn't supported AND doesn't materially affect the TLS exchange, THEN it should be ignored.

i.e. there's nothing in the spec which mentions Postel's law "be conservative in what you send, be liberal in what you accept".  So implementors reading this document are free to do all kinds of odd things.

In addition, the text in Section 4.2 at the bottom of page 38 says:

"
      Designers
      and implementors should be aware of the fact that until the
      handshake has been authenticated, active attackers can modify
      messages and insert, remove, or replace extensions.
"

The implicit conclusion here is that an implementation receiving extensions must sanity check them.  e.g. an attacker adding an undefined / unknown extension should not cause the entire session to be torn down.

Paul Wouters(AD): Resolved but with the Corrected Text:

The client MAY use this PSK for future handshakes by including the ticket value in the "pre_shared_key" extension in its ClientHello (Section 4.2.11). Clients which receive a NewSessionTicket message but do not support resumption MUST silently ignore this message.
```

</details>

<br>**Explanation:**
The original specification is unclear about how clients that do not support session tickets should handle the presence of the "pre_shared_key" extension. The corrected text adds a statement clarifying that clients without session ticket support MUST silently ignore the extension. This omission in the original specification leads to ambiguity in implementation.

---

<details>
<summary><b>Errata 7081</b> from <b>RFC 8754</b> - IPv6 Segment Routing Header (SRH) (March 2020)</summary>

```
Section 4.1.1 says:


A reduced SRH does not contain the first segment of the related SR
Policy (the first segment is the one already in the DA of the IPv6
header), and the Last Entry field is set to n-2, where n is the
number of elements in the SR Policy.


It should say:

A reduced SRH does not contain the first segment of the related SR
Policy (the first segment is the one already in the DA of the IPv6
header), and the Last Entry field is set to n-2, where n is the
number of elements in the SR Policy.

When an SRH includes TLVs and only one 128-bit Segment, the reduced
SRH MUST NOT be used to avoid errors of SRH TLV processing defined
in section 2.1. 


Notes:

When only one single Segment is included in the SRH, the last entry will be 0 forever, so a segment endpoint node cannot specify whether the last Segment is included or removed from the SRH. 

As defined in section 2.1, only when the header length of SRH larger then (0+1)*2, the TLVs will be processed. 
1.	When the Segment is removed, Segment Lefts = Last Entry = 0, each segment endpoint node will skip the bytes 8-16, and then process the following bytes following the TLV processing rules, which will cause errors.
2.	When the segment is not removed, Segment Lefts = Last Entry = 0, each segment endpoint will process the TLVs correctly from byte 8+16. 

Choosing option 2 can avoid processing error of SRH TLVs and be compatible with the current hardware implementation. Thus option 1 MUST be avoid in implementation.
```

</details>

<br>**Explanation:**
The original text does not address the case where an SRH contains only one segment and TLVs. The correction adds a restriction against using a reduced SRH in this case, avoiding potential errors in SRH TLV processing.  This inconsistency would lead to implementations incorrectly handling reduced SRHs with only one segment and TLVs.

---

<details>
<summary><b>Errata 7102</b> from <b>RFC 8754</b> - IPv6 Segment Routing Header (SRH) (March 2020)</summary>

```
Section 2 says:


Segments Left:  Defined in [RFC8200], Section 4.4.

It should say:

Segments Left:  Defined in [RFC8200], Section 4.4.
Specifically, for the SRH, the number of unprocessed 
128-bit entries in the Segment List.

Notes:

RFC8754 describes “The encoding of IPv6 segments in the SRH” where IPv6 segments are defined in RFC8402.  RFC8402 describes binding SIDs and adjacency SIDs for SRv6. Both these SID types identify more than a single explicitly listed intermediate node to be visited.

The current definition of Segments Left only indicates it is defined in RFC8200, and RFC8200 defines it as “Number of route  segments remaining, i.e., number of explicitly listed intermediate nodes still to be visited before reaching the final destination”.

Previous versions of draft-ietf-6man-segment-routing-header (0-11) referenced RFC2460/RFC8200 and described the Segments Left field by use in the SRH; as an index into the Segment List. This was removed in later versions (12/13) to consolidate the use of segments left to be specific to the segment processed (now section 4.3.1).  However, that removed the definition of its meaning in the SRH which led to the current issue.

The corrected text restores the meaning of Segments Left for the SRH in relation to Segment List (which is not defined in RFC8200), while still leaving its use during segment processing to the segment definition (section 4.3.1 or future documents).
```

</details>

<br>**Explanation:**
The original text only states that the Segments Left field is defined in RFC 8200 but does not provide its meaning in the context of the SRH. This omission makes the specification incomplete and potentially ambiguous, particularly regarding its relationship to the Segment List within the SRH.

---

<details>
<summary><b>Errata 7894</b> from <b>RFC 8888</b> - RTP Control Protocol (RTCP) Feedback for Congestion Control (January 2021)</summary>

```
Section 3.1 says:


   RTCP Congestion Control Feedback Packets SHOULD include a report
   block for every active SSRC.

It should say:

   RTCP Congestion Control Feedback Packets SHOULD include a report
   block for every SSRC where packets have been received since the
   previous report was generated.

Notes:

The term "active" is ambiguous. Discussion on the avtcore mailing list indicates that this is the intended meaning.
```

</details>

<br>**Explanation:**
The original text uses the term "active SSRC", which is ambiguous. The correction clarifies that a report block should be included for each SSRC where packets have been received since the last report, providing a more precise definition.

---

<details>
<summary><b>Errata 7093</b> from <b>RFC 9083 part of STD 95</b> - JSON Responses for the Registration Data Access Protocol (RDAP) (June 2021)</summary>

```
Section 4.1 says:


The data structure named "rdapConformance" is an array of strings,
each providing a hint as to the specifications used in the construction
of the response.

It should say:

The data structure named "rdapConformance" is an array of strings,
each identifying a registered specification used in the construction
of the response.


Notes:

The original text uses the word "hint", which some people have interpreted to mean "not normative" and/or "can be ignored". This misinterpretation will likely cause significant misunderstanding of the technical specification and might result in faulty implementations if not corrected. The intention and meaning of this sentence is more clearly specified with the corrected text, noting that the array of string identifiers is directly associated with the set of specifications used to construct an RDAP response.
```

</details>

<br>**Explanation:**
The use of the word "hint" in the original description is ambiguous and allows for misinterpretations of the rdapConformance data structure.  The corrected text clarifies that the strings identify registered specifications, removing the ambiguity and ensuring that implementations correctly process this data structure.

---

<details>
<summary><b>Errata 6752</b> from <b>RFC 9134</b> - RTP Payload Format for ISO/IEC 21122 (JPEG XS) (October 2021)</summary>

```
Section 4.2 says:


As specified in [RFC3550] and [RFC4175], the RTP timestamp
designates the sampling instant of the first octet of the video
frame to which the RTP packet belongs.  Packets SHALL NOT include
data from multiple video frames, and all packets belonging to the
same video frame SHALL have the same timestamp.  Several
successive RTP packets will consequently have equal timestamps if
they belong to the same video frame (that is until the marker bit
is set to 1, marking the last packet of the video frame), and the
timestamp is only increased when a new video frame begins.

It should say:

As specified in [RFC3550] and [RFC4175], the RTP timestamp
designates the sampling instant of the first octet of the video
frame/field to which the RTP packet belongs.  Packets SHALL NOT include
data from multiple video frames/fields, and all packets belonging to the
same video frame/field SHALL have the same timestamp.  Several
successive RTP packets will consequently have equal timestamps if
they belong to the same video frame/field (that is until the marker bit
is set to 1, marking the last packet of the video frame/field), and the
timestamp is only increased when a new video frame/field begins.

Notes:

This RFC follows RFC4175 (and also SMPTE2110) for timestamping RTP packets. The intent has always been to have unique timestamps per progressive video frame and/or per interlaced video field (two fields of a frame MUST be allowed to have different timestamps). This is correctly reflected by the marker bit (M) that is used to indicate the last packet of a frame/field (which is correctly explained in this RFC). However, the accompanied text about the timestamp in section 4.2 does not properly formulate this for the interlaced mode case (it was an editorial oversight), which can cause confusion to implementers of this RFC.
```

</details>

<br>**Explanation:**
The original text is unclear about whether the RTP timestamp applies to video frames or fields. The correction clarifies that it applies to both, thus addressing the ambiguity and ensuring that implementations correctly handle both progressive and interlaced video.

---

<details>
<summary><b>Errata 7652</b> from <b>RFC 9252</b> - BGP Overlay Services Based on Segment Routing over IPv6 (SRv6) (July 2022)</summary>

```
Section 3.2.1 says:


   Transposition Offset indicates the bit position, and Transposition
   Length indicates the number of bits that are being taken out of the
   SRv6 SID value and encoded in the MPLS Label field.  The bits that
   have been shifted out MUST be set to 0 in the SID value.

It should say:

   Transposition Offset indicates the bit position and Transposition
   Length indicates the number of bits that are being taken out of the
   SRv6 SID value and put into high order bits of MPLS label field. The
   bits that have been shifted out MUST be set to 0 in the SID value.

Notes:

This errata reverses an editorial change that was made during the AUTH48 phase and restores the text that came from the WG and IESG review. Refer https://datatracker.ietf.org/doc/html/draft-ietf-bess-srv6-services-15#page-10

This change was made during the AUTH48 since the "high order bits" was already covered under various subsections of Sec 6. However, readers have reported that there are other places in Sec 6 and Sec 5 where transposition also occurs and that the original text was still required.
```

</details>

<br>**Explanation:**
The original description of Transposition Offset and Transposition Length is unclear about the placement of the extracted bits within the MPLS Label field. The correction clarifies that these bits are put into the high-order bits of the MPLS Label field, resolving the ambiguity.

---

<details>
<summary><b>Errata 7657</b> from <b>RFC 8006</b> - Content Delivery Network Interconnection (CDNI) Metadata (December 2016)</summary>

```
Section 6.10 says:


   {
     "metadata": [
       {
         "generic-metadata-type": "MI.TimeWindowACL",
         "generic-metadata-value": {
           "times": [
             "windows": [
               {
                 "start": "1213948800",
                 "end": "1478047392"
               }
             ],
             "action": "allow"
           ]
         }
       }
     ]
   }

It should say:

   {
     "metadata": [
       {
         "generic-metadata-type": "MI.TimeWindowACL",
         "generic-metadata-value": {
           "times": [
              {
                "windows": [
                  {
                    "start": 1213948800,
                    "end": 1478047392
                  }
                ],
                "action": "allow"
              }
           ]
         }
       }
     ]
   }

Notes:

1. The "times" property of  the TimeWindowACL object has an array of TimeWindowRule type, so I changed it to "windows" and "action" are contained in braces.
2. The "start" and "end" property of the TimeWindow object have a Time type, which is an alias of Integer. So I changed their values ("1213948800", "1478047392") to Integer (1213948800, 1478047392).
```

</details>

<br>**Explanation:**
The erratum corrects a structural error in the example JSON provided in Section 6.10 of RFC 8006.  The original example has an incorrect nesting of the "windows" and "action" properties within the "times" array. The correction shows the correct nesting, directly impacting how the JSON would be interpreted and parsed during implementation.  This inconsistency makes the original example unimplementable without additional clarification.

---

<details>
<summary><b>Errata 4439</b> from <b>RFC 7240</b> - Prefer Header for HTTP (June 2014)</summary>

```
Section 2 says:


     preference = token [ BWS "=" BWS word ]
                  *( OWS ";" [ OWS parameter ] )
     parameter  = token [ BWS "=" BWS word ]

It should say:

     preference = preference-parameter *( OWS ";" [ OWS
                  preference-parameter ] )
     preference-parameter = parameter / token


Notes:

Section 1.1 incorrectly states that "word" is defined in RFC 7230.  It is not.  Therefore, the syntax is completely under-specified.

The "parameter" rule, as defined in RFC 7231, is used in lots of other header field definitions successfully.  The only drawback is that "parameter" doesn't permit the use of "OWS" either side of the "=" character.

This change would also require changes to Section 1.1.
```

</details>

<br>**Explanation:**
The erratum points out that the original specification uses an undefined term "word" in the definition of `preference` and `parameter`, rendering the syntax incomplete and making it impossible to unambiguously implement support for the Prefer header. The lack of a clear definition for "word" and the suggested replacement using the more precisely defined `parameter` rule from RFC 7231 directly addresses this underspecification, impacting the correct implementation of parsing and handling of the Prefer header.

---

<details>
<summary><b>Errata 6277</b> from <b>RFC 8040</b> - RESTCONF Protocol (January 2017)</summary>

```
Section 4.8.5 says:


The default value is "last".

It should say:

The default value is “last”, except when used with PUT 
and the target resource already exists, in which case the 
default is to replace the target resource without altering
its position in the "ordered-by user” list or leaf-list.


Notes:

The "last" default is intended for when creating a new element.  

A PUT operation that replaces a list or leaf-list entry should not move the entry unless the "insert" parameter is explicitly passed.
```

</details>

<br>**Explanation:**
The description of the default value for the insertion position in Section 4.8.5 is incomplete and inconsistent. It only specifies "last" as the default, neglecting the different behavior when used with a PUT operation on an existing resource. This omission leads to an incorrect understanding of the default behavior for PUT requests, potentially causing unintended modifications to the list's order.  The correction clarifies the behavior for both creating a new element and replacing an existing one, resolving the inconsistency.

---

<details>
<summary><b>Errata 7311</b> from <b>RFC 8040</b> - RESTCONF Protocol (January 2017)</summary>

```
Section 7 says:


              +-------------------------+------------------+
              | error-tag               | status code      |
              +-------------------------+------------------+
(...)
              | unknown-attribute       | 400              |
              |                         |                  |
              | bad-element             | 400              |
(...)

It should say:

              +-------------------------+------------------+
              | error-tag               | status code      |
              +-------------------------+------------------+
(...)
              | unknown-attribute       | 400              |
              |                         |                  |
              | missing-element         | 400              |
              |                         |                  |
              | bad-element             | 400              |
(...)

Notes:

Add missing-element to the table Mapping from <error-tag> to Status Code
in Section 7.

The NETCONF error-tag missing-element is not listed in the table mapping
error-tag to HTTP status code. This seems to be a mistake since all other
error-tags are listed (even the obsolete partial-operation which should not
be used according to RFC 6241).
```

</details>

<br>**Explanation:**
The table in Section 7 mapping error tags to HTTP status codes is missing the entry for "missing-element", which is a valid NETCONF error tag. This omission is inconsistent with the inclusion of other error tags, including an obsolete one. The inconsistency could lead to incorrect implementation of error handling in RESTCONF servers that do not map the missing-element error tag to an appropriate HTTP status code.

---

<details>
<summary><b>Errata 7866</b> from <b>RFC 8040</b> - RESTCONF Protocol (January 2017)</summary>

```
Section Multiple says:


Text occurs in three places

1)    Section 3.5.3

      The leaf-list value is specified as a string, using the canonical
      representation for the YANG data type.  Any reserved characters
      MUST be percent-encoded, according to Sections 2.1 and 2.5 of
      [RFC3986].


2)    Section 3.5.3

      The key value is specified as a string, using the canonical
      representation for the YANG data type.  Any reserved characters
      MUST be percent-encoded, according to Sections 2.1 and 2.5 of
      [RFC3986]. 


3)    Section 5.1

      The contents of any query parameter value MUST be encoded according
      to Section 3.4 of [RFC3986].  Any reserved characters MUST be
      percent-encoded, according to Sections 2.1 and 2.5 of [RFC3986].

It should say:

1)    Section 3.5.3

      The leaf-list value is specified as a string, using the canonical
      representation for the YANG data type.  Any reserved characters
      MUST be percent-encoded, according to Sections 2.1, 2.2, and 2.5 of
      [RFC3986].

2)    Section 3.5.3

      The key value is specified as a string, using the canonical
      representation for the YANG data type.  Any reserved characters
      MUST be percent-encoded, according to Sections 2.1, 2.2, and 2.5 of
      [RFC3986]. 

3)    Section 5.1
      
      The contents of any query parameter value MUST be encoded according
      to Section 3.4 of [RFC3986].  Any reserved characters MUST be
      percent-encoded, according to Sections 2.1, 2.2, and 2.5 of [RFC3986].


Notes:

The reserved character list is defined in section 2.2 of RFC 3986
```

</details>

<br>**Explanation:**
The specification inconsistently refers to sections of RFC3986 for percent-encoding rules.  While Sections 2.1 and 2.5 are mentioned in multiple places, Section 2.2 is omitted but is relevant to defining reserved characters.  This inconsistency creates ambiguity in the implementation of percent-encoding, as implementers may not include all necessary reserved characters specified in Section 2.2.  Therefore, it is classified as INCONSISTENT.

---
