---

copyright:
  years: 2018
lastupdated: "2019-11-14"

keywords: nat, working, gateways, nodes

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Working with sNAT
{: #working-with-snat}
{: help}
{: support}

This topic provides a sample configuration for sNAT on a vSRX appliance. With this configuration, a private node routed behind the Gateway can communicate with the outside world.
{: shortdesc}

![Sample topology](images/Sample-Topology-SNAT.png "Sample topology")

```sh
from-zone CUSTOMER-PRIVATE to-zone SL-PUBLIC {
   policy SNAT {
       match {
           source-address any;
           destination-address any;
           application any;
       }
       then {
           permit;
       }
   }
}

nat {
   source {
       rule-set rs1 {
           from zone CUSTOMER-PRIVATE;
           to zone SL-PUBLIC;
           rule r1 {
               match {
                   source-address 0.0.0.0/0;
                   destination-address 0.0.0.0/0;
               }
               then {
                   source-nat {
                       interface;
                   }
               }
           }
       }
   }
}
```

To configure NAT for the {{site.data.keyword.vsrx_full}}, refer to this [configuration guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf){: new_window} on the Juniper website.
