---
coding: utf-8

title: A YANG Data Model for Optical Network Inventory

abbrev: Optical Inventory YANG
docname: draft-yg3bp-ccamp-optical-inventory-yang-01
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
  -
    name: Oscar Gonzalez de Dios
    ins: O. Gonzalez de Dios
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com
  -
    name: Victor Lopez
    org: Nokia
    email: victor.lopez@nokia.com

#contributor:
#  -

normative:
  TMF-MTOSI:
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

The YANG data model presented in this document is intended to be used as the basis toward a generic YANG data model for network inventory data information which can be augmented, when required, with technology-specific (e.g., optical) inventory data, to be defined either in a future version of this document or in another document.

The YANG data model defined in this document conforms to the Network Management Datastore Architecture (NMDA).

--- middle

# Introduction

Network inventory management is a key component in operators' OSS architectures.

  Network inventory is a fundamental functionality in network management
  and was specified many years ago. Given the emerging of data models and 
  their deployment in operator's management and control systems, the traditional function of inventory management
  is also requested to be defined as a data model. 

  Network inventory management and monitoring is a critical part of 
  ensuring the network stays healthy, well-planned, and functioning 
  in the operator's network. Network inventory management allows the
  operator to keep track of what physical network devices are staying
  in the network including relevant software and hardware.

  The network inventory management also helps the operator to know when 
  to acquire new assets and what is needed, or to decommission old or faulty ones, 
  which can help to improve network performance and capacity planning.

In {{?I-D.ietf-teas-actn-poi-applicability}} a gap was identified regarding the lack of a YANG data model that could be used at ACTN MPI interface level to report whole/partial hardware inventory information available at PNC level towards north-bound systems (e.g., MDSC or OSS layer).

{{?RFC8345}} initial goal was to make possible the augmentation of the YANG data model with network inventory data model but this was never developed and the scope was kept limited to network topology data only.

It is key for operators to drive the industry towards the use of a standard YANG data model for network inventory data instead of using vendors proprietary APIs (e.g., REST API).

In the ACTN architecture, this would bring also clear benefits at MDSC level for packet over optical integration scenarios since this would enable the correlation of the inventory information with the links information reported in the network topology model.

The intention is to define a generic YANG data model that would be as much as possible technology agnostic (valid for IP, optical and microwave networks) and that could be augmented, when required, to include some technology-specific inventory details.

{{!RFC8348}} defines a YANG data model for the management of the hardware on a single server and therefore it is more applicable to the PNC South Bound Interface (SBI) towards the network elements rather than at the PNC MPI. However, the YANG data model defined in {{!RFC8348}} has been used as a reference for defining the YANG network inventory data model.

For optical network inventory, the network inventory YANG data model should support the use cases (4a and 4b) and requirements defined in {{ONF_TR-547}}, in order to guarantee a seamless integration at MDSC/OSS/orchestration layers.

The proposed YANG data model has been analysed to cover the requirements and use cases for Optical Network Inventory.

Being based on {{!RFC8348}}, this data model should be a good starting point toward a generic data model and applicable to any technology. However, further analysis of requirements and use cases is needed to extend the applicability of this YANG data model to other types of networks (IP and microwave) and to identify which aspects are generic and which aspects are technology-specific for optical networks.

This document defines one YANG module: ietf-network-inventory.yang ({{ni-yang}}).

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

  TBD: Recap the concept of chassis/slot/component/board/... in {{TMF-MTOSI}}.

  Following terms are used for the representation of the hierarchies in the 
  optical network inventory. 

  Network Element:

  > a device installed on one or several shelves and can afford some specific transmission function independently.

  Cabinet:

  > a holder of the device and provides power supply for the device in it.

  Chassis:

  > a holder of the device installation.

  Slot:

  > a holder of the board.

  Component:

  > holders and equipments of the network element, including rack, shelf, slot, sub-slot, board and port.

  Board/Card:

  > a pluggable equipment on the network element and can afford a specific transmission function independently.

  Port:

  > an interface on board

## Tree Diagram

A simplified graphical representation of the data model is used in {{ni-tree}} of this document.
The meaning of the symbols in these diagrams is defined in {{!RFC8340}}.

## Prefix in Data Node Names

  In this document, names of data nodes and other data model objects
  are prefixed using the standard prefix associated with the
  corresponding YANG imported modules, as shown in the following table.

| Prefix | Yang Module            | Reference    |
| ------ | ---------------------- | ------------ |
| ianahw | iana-hardware          | {{!RFC8348}} |
| ni     | ietf-network-inventory | RFCXXX       |
| yang   | ietf-yang-types        | {{!RFC6991}} |
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

RFC Editor Note:
Please replace XXXX with the RFC number assigned to this document.
Please remove this note.

# YANG Data Model for Optical Network Inventory 

## YANG Model Overview

Based on TMF classification in {{TMF-MTOSI}}, inventory objects can be divided into two groups, holder group and equipment group. The holder group contains rack, shelf, slot, sub-slot while the equipment group contains network-element, board and port. With the requirement of GIS and on-demand domain controller selection raised, the equipment room becomes a new inventory object to be managed besides TMF classification.

Logically,  the relationship between these inventory objects can be described by {{fig-inventory-object-relationship}} below:

~~~~
                +-------------+
                |  inventory  |
                +-------------+
                    // \\
              1:N  //   \\ 1:M
                  //     \\                             
  +----------------+     +-----------------+ 
  | equipment room |     | network element |
  +----------------+     +-----------------+
          ||                     ||
          || 1:N                 ||
          \/                     || 
    +------------+               ||1:M
    |    rack    |               ||
    +------------+               ||
          ||                     ||
          || 1:N                 \/
          ||______________\+------------+
          |---------------/|   shelf    |
                           +------------+
                                 ||
                  ______1:N______||_____1:M_______
                  ||------------------ ---------||
                  \/                            \/      
           +--------------+               +-----------+
           | slot/subslot |               |   board   |
           +--------------+               +-----------+
                                                ||
                                                ||1:N
                                                \/
                                          +-----------+ 
                                          |    port   |
                                          +-----------+

~~~~
{: #fig-inventory-object-relationship title="Relationship between inventory objects"}

In {{!RFC8348}}, rack, shelf, slot, sub-slot, board and port are defined as components of network elements with generic attributes.

While {{!RFC8348}} is used to manage the hardware of a single server (e.g., a Network Element), the Network Inventory YANG data model is used to retrieve the network inventory information that a controller discovers from multiple Network Elements under its control.

However, the YANG data model defined in {{!RFC8348}} has been used as a reference for defining the YANG network inventory data model. This approach can simplify the implementation of this network inventory model when the controller uses the YANG data model defined in {{!RFC8348}} to retrieve the hardware configuration from the network elements under its control.

Note: review in future versions of this document which attributes from {{!RFC8348}} are required also for network inventory and whether there are attributes not defined in {{!RFC8348}}which are required for network inventory

Note: review in future versions of this document whether to re-use definitions from {{!RFC8348}} or use schema-mount.

~~~~
  +--ro network-inventory
     +--ro equipment-rooms
     |  +--ro equipment-room* [uuid]
     |     +--ro uuid        yang:uuid
     |     ...................................
     |     +--ro rack* [uuid]
     |        +--ro uuid           yang:uuid
     |        ...................................
     |        +--ro shelves* [uuid]
     |           +--ro uuid            yang:uuid
     |           ...................................
     |           +--ro chassis-ref
     |              +--ro ne-ref?          leafref
     |              +--ro component-ref?   leafref
     +--ro network-elements
        +--ro network-element* [uuid]
           +--ro uuid          yang:uuid
           ...................................
           +--ro components
              +--ro component* [uuid]
                 +--ro uuid              yang:uuid
                 ...................................
~~~~

The YANG data model for network inventory follows the same approach of {{!RFC8348}} and reports the network inventory as a list of components of different types (e.g., chassis, module, port).

~~~~
  +--ro components
     +--ro component* [uuid]
        +--ro uuid              yang:uuid
        +--ro name?             string
        +--ro description?      string
        +--ro class?            identityref
        +--ro parent-rel-pos?   int32
        +--ro children* [child-ref]
        |  +--ro child-ref    -> ../../uuid
        +--ro parent
           +--ro parent-ref?   -> ../../uuid
~~~~

Note: review in future versions of this document whether the component list should be under the network-inventory instead of under the network-element container

However, considering there are some special scenarios, the relationship between the rack and network elements is not 1 to 1 nor 1 to n. The network element cannot be the direct parent node of the rack. So there should be n to m relationship between racks and network elements.
And the shelves in the rack should have some reference information to the component.

Note that in {{?RFC8345}}, topology and inventory are two subsets of network information. However, considering the complexity of the existing topology models and to have a better extension capability, we define a separate root for the inventory model. We will consider some other ways to do some associations between the topology model and inventory model in the future.

Note: review in future versions of this document whether network inventory should be defined as an augmentation of the network model defined in {{?RFC8345}} instead of under a new network-inventory root.

The proposed YANG data model has been analysed to cover the requirements and use cases for Optical Network Inventory.

Further analysis of requirements and use cases is needed to extend the applicability of this YANG data model to other types of networks (IP and microwave) and to identify which aspects are generic and which aspects are technology-specific for optical networks.

{: #ni-tree}

# Optical Network Inventory Tree Diagram

{{fig-ni-tree}} below shows the tree diagram of the YANG data model defined in module ietf-network-inventory.yang ({{ni-yang}}).

~~~~
{::include ./ietf-network-inventory.tree}
~~~~
{: #fig-ni-tree title="Network inventory tree diagram"}

{: #ni-yang}

# YANG Model for Optical Network Inventory

~~~~
<CODE BEGINS> file "ietf-network-inventory@2021-11-10.yang"
{::include ./ietf-network-inventory.yang}
~~~~
{: #fig-ni-yang title="Network inventory YANG module"}

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
