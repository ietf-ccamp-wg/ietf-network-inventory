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

--- abstract

  Network inventory is a foundamental functionality in network management
  and was specified many years ago. Given the emerging of data model and 
  their deployment in operator's management system, the traditional function
  is also requested to be defined as data model for inventory management. 

  This document defines the YANG data model for optical network inventory
  information. The YANG data model defined in this
   document conforms to the Network Management Datastore Architecture
   (NMDA).

--- middle

# Introduction

  Network inventory management and monitoring is a critical part of 
  ensuring the network stays healthy, well-planned, and functioning 
  in the carriers network. Network inventory management allows the
  operator to keep track of what physical network devices are staying
  in the network including relevant software and hardware. 
   
  The network inventory management also helps the operator to know when 
  to acquire new assets and what is needed, or to decommission old ones, 
  which can help improving network performance and capacity planning.
   
  This document defines one YANG module: TBD
  ({{inventory-yang}}).  This document augments the generic network model {{!RFC8345}}.

  TBD: review the related modules, depending on the augmentation relationship. 
  TBD: give the augmentation relationship.

The proposed YANG data model has been analysed to cover the requirements and use cases for Optical Network Inventory.

Further analysis of requirements and use cases is needed to extend the applicability of this YANG data model to other types of networks.

  The YANG data model defined in this document conforms to the Network
  Management Datastore Architecture {{!RFC8342}}.

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

  A simplified graphical representation of the data model is used in
  {{inventory-tree}} of this document.  The meaning of the symbols in these
  diagrams is defined in {{!RFC8340}}.

## Prefix in Data Node Names

  In this document, names of data nodes and other data model objects
  are prefixed using the standard prefix associated with the
  corresponding YANG imported modules, as shown in the following table.

| Prefix      | YANG module             | Reference
| nw          | ietf-network            | {{!RFC8345}}
| nt          | ietf-network-topology   | {{!RFC8345}}
| ianahw      | iana-hardware           | {{!RFC8348}}
| ni          | ietf-network-inventory  | This Document         
{: #tab-prefixes title="Inventory Related Model and Prefixes"}

# YANG Data Model for Optical Network Inventory 

## YANG Model Overview

The YANG model for optical network inventory augments the abstract network model defined in {{!RFC8345}},
as described in Figure 1 of {{!RFC8345}} and shown below in {{fig-inventory}}.

~~~~
                         +-------------------------+
                         | Abstract Network Model  |
                         +-------------------------+
                                      |
                              +-------+-------+
                              |               |
                              V               V
                       +------------+  ..............
                       |  Abstract  |  : Inventory  :
                       |  Topology  |  :  Model(s)  :
                       |   Model    |  :            :
                       +------------+  ''''''''''''''
~~~~
{: #fig-inventory title="Network Inventory and Network Topology Models Relationship"}

The YANG data model for network inventory follows the same approach of {{!RFC8348}} and reports the network
inventory as a list of components of different types (e.g., chassis, module, port).

TBD whether the component list is under the network or under the node container

TBD whether to re-use definitions from {{!RFC8348}} or use schema-mount

While {{!RFC8348}} is used to manage the hardware of a single server (e.g., a Network Element), the Network
Inventory YANG data model is used to retrieve the network inventory information that a controller that discovers it  from multiple Network Elements it controls.

The proposed YANG data model has been analysed to cover the requirements and use cases for Optical Network Inventory.

Further analysis of requirements and use cases is needed to extend the applicability of this YANG data model to other types of networks.

{: #inventory-tree}

# Optical Network Inventory Tree Diagram

{: #inventory-yang}

# YANG Model for Optical Network Inventory

# Manageability Considerations

  TBD. 

# Security Considerations

  \<Add any security considerations>

# IANA Considerations

  \<Add any IANA considerations>

--- back

{: numbered="false"}

# Acknowledgments

   This document was prepared using kramdown.
