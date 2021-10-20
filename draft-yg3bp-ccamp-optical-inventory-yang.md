---
coding: utf-8

title: A YANG Data Model for Optical Network Inventory

abbrev: Optical Inventory YANG
docname: draft-xx-ccamp-optical-inventory-yang-00
workgroup: CCAMP Working Group
category: std
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Chaode Yu
    org: Huawei Technologies
    email: yuchaode@huawei.com
  -
    name: Italo Busi
    org: Huawei Technologies
    email: italo.busi@huawei.com
  -
    name: Aihua Guo
    org: Futurewei Technologies
    email: aihuaguo.ietf@gmail.com
  -
    name: Sergio Belotti
    org: Nokia
    email: sergio.belotti@nokia.com
  -
    ins: J-F. Bouquier
    name: Jean-Francois Bouquier
    org: Vodafone
    email: jeff.bouquier@vodafone.com
  -
    name: Fabio Peruzzini
    org: TIM
    email: fabio.peruzzini@telecomitalia.it

#contributor:
#  -

normative:
  TMF-MTOSI_4.0:
    title: TMF MTOSI 4.0 Equipment Model
    author:
      org: TM Forum (TMF)
    date:  2008
    seriesinfo: TMF SD2-20_EquipmentModel
    target: https://www.tmforum.org/resources/suite/mtosi-4-0/

informative:
  ONF_TR-547:
    title: TAPI v2.1.3 Reference Implementation Agreement
    author:
      org: Open Networking Foundation (ONF)
    date:  July 2020
    seriesinfo: ONF TR-547 TAPI RIA v1.0
    target: https://opennetworking.org/wp-content/uploads/2020/08/TR-547-TAPI-v2.1.3-Reference-Implementation-Agreement-1.pdf

--- abstract

This document defines a YANG data model for optical network inventory data information.

Future versions of this document may define a generic YANG data model for network inventory data information which can be augmented, when required, with technology-specific (e.g., optical) inventory data.

The YANG data model defined in this document conforms to the Network Management Datastore Architecture (NMDA).

--- middle

# Introduction

Network inventory management is a key component in operators' OSS architectures.

In {{?I-D.ietf-teas-actn-poi-applicability}} a gap was identified regarding the lack of a YANG data model that could be used at ACTN MPI interface level to report whole/partial hardware inventory information available at PNC level towards north bound systems (e.g., MDSC or OSS layer).

{{?RFC8345}} initial goal was to make possible the augmentation of the YANG data model with network inventory data model but this was never developped and the scope was kept limited to network topology data only.

It is key for operators to drive the industry towards the use of standard YANG data model for network inventory data instead of using vendors proprietary APIs (e.g., REST API).

In the ACTN architecture this would bring also clear benefits at MDSC level for packet over optical integration scenarios since this would enable to correlate the inventory information with the links information reported in the network topology model.

The intention is to define a generic YANG data model that would be as much as possible technology agnostic (valid for IP, optical and microwave networks) and that could be augmented, when required, to include some technology-specific inventory details.

{{!RFC8348}} defines a YANG data model for the management of the hardware on a single server and therefore it is more applicable to the PNC South Bound Interface (SBI) towards the network elements rather than at the PNC MPI. However, the YANG data model defined in {{!RFC8348}} has been used as a reference for defining the YANG network inventory data model.

For optical network inventory, the network inventory YANG data model should support the use cases (4a and 4b) and requirements defined in {{ONF_TR-547}}, in order to guarantee a seamless integration at MDSC/OSS/orchestration layers.

The proposed YANG data model has been analysed to cover the requirements and use cases for Optical Network Inventory.

Further analysis of requirements and use cases is needed to extend the applicability of this YANG data model to other types of networks (IP and microwave) and to identify which aspects are generic and which aspects are tecnology-spefic for optical networks.

This document defines one YANG module: TBD ({{ni-yang}}).

Note: review in future versions of this document the related modules, depending on the augmentation relationship.

The YANG data model defined in this document conforms to the Network Management Datastore Architecture {{!RFC8342}}.

## Terminology and Notations 

  Refer to {{!RFC7446}} and {{!RFC7581}} for the key terms used in this
  document.  The following terms are defined in {{!RFC7950}} and are not
  redefined here:

  *  client

  *  server

  *  augment

  *  data model

  *  data node

  The following terms are defined in {{!RFC6241}} and are not redefined
  here:

  *  configuration data

  *  state data

  The terminology for describing YANG data models is found in
  {{!RFC7950}}.

  TBD: Recap the concept of chassis/slot/component/board/... in TMF.
   
  Following terms are used for representation of the hierarchies in the 
  optical network inventory. 
   
  Network Element:
   
  Cabinet：a combination of rack, chassis and shelf. 
   
  Chassis: 
   
  Slot: 
   
  Component: 
   
  Board/Card:    

## Tree Diagram

A simplified graphical representation of the data model is used in {{ni-tree}} of this document.
The meaning of the symbols in these diagrams is defined in {{!RFC8340}}.

## Prefix in Data Node Names

  In this document, names of data nodes and other data model objects
  are prefixed using the standard prefix associated with the
  corresponding YANG imported modules, as shown in the following table.

| Prefix      | YANG module             | Reference
| ianahw      | iana-hardware           | {{!RFC8348}}
| ni          | ietf-network-inventory  | RFCXXXX         
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

RFC Editor Note:
Please replace XXXX with the RFC number assigned to this document.
Please remove this note.

# YANG Data Model for Optical Network Inventory 

## YANG Model Overview

The YANG model for optical network inventory ...

TBD: add some overview of the tree (network-inventory, rooms and network-elements lists)

Note: review in future versions of this document whether network inventory should be defined as an augmentation of the network model defined in {{?RFC8345}} instead of under a new network-inventory root

TBD: add some overview of the tree of the equiment rooms

The YANG data model for network inventory follows the same approach of {{!RFC8348}} and reports the network inventory as a list of components of different types (e.g., chassis, module, port).

TBD: add some overview of the tree of the component list

Note: review in future versions of this document whether the component list should be under the network-inventory instead of under the network-element container

While {{!RFC8348}} is used to manage the hardware of a single server (e.g., a Network Element), the Network Inventory YANG data model is used to retrieve the network inventory information that a controller discovers from multiple Network Elements under its control.

However, the YANG data model defined in {{!RFC8348}} has been used as a reference for defining the YANG network inventory data model.

Note: review in future versions of this document which attributes from {{!RFC8348}} are required also for network inventory and whether there attributes not defined in {{!RFC8348}}which are required for network inventory

Note: review in future versions of this document whether to re-use definitions from {{!RFC8348}} or use schema-mount

The proposed YANG data model has been analysed to cover the requirements and use cases for Optical Network Inventory.

Further analysis of requirements and use cases is needed to extend the applicability of this YANG data model to other types of networks (IP and microwave) and to identify which aspects are generic and which aspects are tecnology-spefic for optical networks.

{: #ni-tree}

# Optical Network Inventory Tree Diagram

TBA

{: #ni-yang}

# YANG Model for Optical Network Inventory

TBA

# Manageability Considerations

  \<Add any manageability considerations>

# Security Considerations

  \<Add any security considerations>

# IANA Considerations

  \<Add any IANA considerations>

--- back

{: numbered="false"}

# Acknowledgments

The authors of this document would like to thank the authors of {{?I-D.ietf-teas-actn-poi-applicability}} for having identified the gap and requirements to trigger this work.

This document was prepared using kramdown.
