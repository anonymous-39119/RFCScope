# Errata 8132 - RFC 9656

- **RFC Title:** A YANG Data Model for Microwave Topology
- **RFC Publication Date:** September 2024
- Link to original errata report: [rfc-editor.org/errata/eid8132](https://www.rfc-editor.org/errata/eid8132)

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

## Explanation

The example in Annex A.2 uses an inconsistent number of protecting carriers (0) compared to the other examples and the description, which implies that this number should be 1 in a protected configuration.  The correction sets the num-protecting-carriers value to 1, resolving the inconsistency.
