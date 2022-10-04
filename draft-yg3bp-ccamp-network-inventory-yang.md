---
coding: utf-8

title: A YANG Data Model for Network Hardware Inventory

abbrev: Network Inventory YANG
docname: draft-yg3bp-ccamp-network-inventory-yang-01
submissiontype: IETF
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

This document defines a YANG data model for network hardware inventory data information.

The YANG data model presented in this document is intended to be used as the basis toward a generic YANG data model for network hardware inventory data information which can be augmented, when required, with technology-specific (e.g., optical) inventory data, to be defined either in a future version of this document or in another document.

The YANG data model defined in this document conforms to the Network Management Datastore Architecture (NMDA).

--- middle

# Introduction

Network hardware inventory management is a key component in operators' OSS architectures.

  Network inventory is a fundamental functionality in network management
  and was specified many years ago. Given the emerging of data models and 
  their deployment in operator's management and control systems, the traditional function of inventory management
  is also requested to be defined as a data model. 

  Network inventory management and monitoring is a critical part for 
  ensuring the network stays healthy, well-planned, and functioning 
  in the operator's network. Network inventory management allows the
  operator to keep track of what physical network devices are staying
  in the network including relevant software and hardware versions.

  The network inventory management also helps the operator to know when 
  to acquire new assets and what is needed, or to decommission old or faulty ones, 
  which can help to improve network performance and capacity planning.

In {{?I-D.ietf-teas-actn-poi-applicability}} a gap was identified regarding the lack of a YANG data model that could be used at ACTN MPI interface level to report whole/partial network hardware inventory information available at domain controller level towards north-bound systems (e.g., MDSC or OSS layer).

{{?RFC8345}} initial goal was to make possible the augmentation of the YANG data model with network inventory data model but this was never developed and the scope was kept limited to network topology data only.

It is key for operators to drive the industry towards the use of a standard YANG data model for network inventory data instead of using vendors proprietary APIs (e.g., REST API).

In the ACTN architecture, this would bring also clear benefits at MDSC level for packet over optical integration scenarios since this would enable the correlation of the inventory information with the links information reported in the network topology model.

The intention is to define a generic YANG data model that would be as much as possible technology agnostic (valid for IP, optical and microwave networks) and that could be augmented, when required, to include some technology-specific inventory details.

{{!RFC8348}} defines a YANG data model for the management of the hardware on a single server and therefore it is more applicable to the domain controller South Bound Interface (SBI) towards the network elements rather than at the domain controller's northbound. However, the YANG data model defined in {{!RFC8348}} has been used as a reference for defining the YANG network hardware inventory data model presented in this draft.

For optical network hardware inventory, the network inventory YANG data model should support the use cases (4a and 4b) and requirements as defined in {{ONF_TR-547}}, in order to guarantee a seamless integration at MDSC/OSS/orchestration layers.

The proposed YANG data model has been analysed at the present stage to cover the requirements and use cases for Optical Network Hardware Inventory.

Being based on {{!RFC8348}}, this data model should be a good starting point toward a generic data model and applicable to any technology. However, further analysis of requirements and use cases is needed to extend the applicability of this YANG data model to other types of networks (IP and microwave) and to identify which aspects are generic and which aspects are technology-specific for optical networks.

This document defines one YANG module: ietf-network-inventory.yang ({{ni-yang}}).

Note: review in future versions of this document the related modules, depending on the augmentation relationship.

The YANG data model defined in this document conforms to the Network Management Datastore Architecture {{!RFC8342}}.

## Terminology and Notations 

  The following terms are defined in {{!RFC7950}} and are not
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

  Following terms are used for the representation of the hierarchies in the network hardware inventory. 

  Network Element:

  > a device installed on one or several chassis and can afford some specific transmission function independently.

  Rack:

  > a holder of the device and provides power supply for the device in it.

  Chassis:

  > a holder of the device installation.

  Slot:

  > a holder of the board.

  Component:

  > holders and equipment of the network element, including chassis, slot, sub-slot, board and port.

  Board/Card:

  > a pluggable equipment can be inserted into one or several slots/sub-slots and can afford a specific transmission function independently.

  Port:

  > an interface on board

## Requirements Notation

{::boilerplate bcp14}

## Tree Diagram

A simplified graphical representation of the data model is used in {{ni-tree}} of this document.
The meaning of the symbols in this diagram is defined in {{!RFC8340}}.

## Prefix in Data Node Names

  In this document, names of data nodes and other data model objects
  are prefixed using the standard prefix associated with the
  corresponding YANG imported modules, as shown in the following table.

| Prefix | Yang Module            | Reference    |
| ------ | ---------------------- | ------------ |
| ianahw | iana-hardware          | {{!RFC8348}} |
| ni     | ietf-network-inventory | RFC XXXX     |
| yang   | ietf-yang-types        | {{!RFC6991}} |
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

RFC Editor Note:
Please replace XXXX with the RFC number assigned to this document.
Please remove this note.

# YANG Data Model for Network Hardware Inventory 

## YANG Model Overview

Based on TMF classification in {{TMF-MTOSI}}, inventory objects can be divided into two groups, holder group and equipment group. The holder group contains rack, chassis, slot, sub-slot while the equipment group contains network-element, board and port. With the requirement of GIS and on-demand domain controller selection raised, the equipment room becomes a new inventory object to be managed besides TMF classification.

Logically,  the relationship between these inventory objects can be described by {{fig-inventory-object-relationship}} below:

~~~~ ascii-art
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
          |---------------/|   chassis  |
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

In {{!RFC8348}}, rack, chassis, slot, sub-slot, board and port are defined as components of network elements with generic attributes.

Considering there are some special scenarios, there is no direct relationship between the rack and network element. In some cases, one network element contains multiple racks while in other cases one rack contains several shelves belonging to one or more network elements.

While {{!RFC8348}} is used to manage the hardware of a single server (e.g., a network element), the Network Inventory YANG data model is used to retrieve the network hardware inventory information that a controller discovers from all the network elements under its control.

However, the YANG data model defined in {{!RFC8348}} has been used as a reference for defining the YANG network inventory data model. This approach can simplify the implementation of this network hardware inventory model when the controller uses the YANG data model defined in {{!RFC8348}} to retrieve the hardware  from the network elements under its control.

Note: review in future versions of this document whether to re-use definitions from {{!RFC8348}} or use schema-mount.

~~~~ ascii-art
  +--ro network-inventory
     +--ro equipment-rooms
     |  +--ro equipment-room* [uuid]
     |     +--ro uuid        yang:uuid
     |     ...................................
     |     +--ro racks
     |        +--ro rack* [uuid]
     |           +--ro uuid           yang:uuid
     |           ...................................
     |           +--ro contained-chassis* [ne-ref component-ref]
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


### Common Design for All Inventory Objects

For all the inventory objects, there are some common attributes existing. Such as:

Identifier: here we suggest to use uuid format which is widely implemented with systems. It is guaranteed to be globally unique.

Name: name is a human-readable label information which could be used to present on GUI. This name is suggested to be provided by server.

Alias: alias is also a human-readable label information which could be modified by user. It could also be present on GUI instead of name.

Description: description is a human-readable information which could be also input by user. Description provides more detailed information to prompt users when performing maintenance operations.

Location: location is a common management requirement of operators. This location could be an absolute position (e.g. mail address), or a relative position (e.g. port index). Different types of inventory objects may require different types of position.

~~~~ ascii-art
module: ietf-network-inventory
   +--ro network-inventory
      +--ro equipment-rooms
      |  +--ro equipment-room* [uuid]
      |     +--ro uuid           yang:uuid
      |     +--ro name?          string
      |     +--ro description?   string
      |     +--ro alias?         string
      |     +--ro location?      string
      |     ...................................
      |     +--ro racks
      |        +--ro rack* [uuid]
      |           +--ro uuid                 yang:uuid
      |           +--ro name?                string
      |           +--ro description?         string
      |           +--ro alias?               string
      |           +--ro rack-location
      |           |  +--ro equipment-room-name?   leafref
      |           |  +--ro row-number?            uint32
      |           |  +--ro column-number?         uint32
      |           ...................................
      +--ro network-elements
         +--ro network-element* [uuid]
            +--ro uuid             yang:uuid
            +--ro name?            string
            +--ro description?     string
            +--ro alias?           string
            +--ro ne-location
            |  +--ro equipment-room-name*   leafref
            ...................................
            +--ro components
               +--ro component* [uuid]
                  +--ro uuid                     yang:uuid
                  +--ro name?                    string
                  +--ro description?             string
                  +--ro alias?                   string
                  +--ro location                 string
                  ...................................
~~~~

### Reference from RFC8348

The YANG data model for network hardware inventory mainly follows the same approach of {{!RFC8348}} and reports the network hardware inventory as a list of components with different types (e.g., chassis, module, port).

~~~~ ascii-art
  +--ro components
     +--ro component* [uuid]
        +--ro uuid              yang:uuid
        +--ro name?             string
        +--ro description?      string
        +--ro class?            identityref
        +--ro children* [child-ref]
        |  +--ro child-ref    leafref
        +--ro hardware-rev?     string
        +--ro firmware-rev?     string
        +--ro software-rev?     string
        +--ro serial-num?       string
        +--ro mfg-name?         string
        +--ro asset-id?         string
        +--ro is-fru?           boolean
        +--ro mfg-date?         yang:date-and-time
        +--ro uri*              inet:uri
~~~~

But we re-defined some attributes listed in {{!RFC8348}}, based on some integration experience for network wide inventory data.

### Changes with respect to RFC8348

#### New Parent Identifiers' Reference

{{!RFC8348}} provided a "parent-ref" attribute, which was an identifier reference to its parent component. When the MDSC or OSS systems want to find this component's grandparent or higher level component in the hierarchy, they need to retrieve this parent-ref step by step. To reduce this iterative work, we decided to provide a list of hierarchical parent components' identifier references.

~~~~ ascii-art
  +--ro components
     +--ro component* [uuid]
        ...................................
        +--ro parent-references
        |  +--ro equipment-room-uuid?    leafref
        |  +--ro ne-uuid?                leafref
        |  +--ro rack-uuid?              leafref
        |  +--ro component-references
        |     +--ro component-reference* [index]
        |        +--ro index    uint8
        |        +--ro class?   leafref
        |        +--ro uuid?    leafref
        ...................................
~~~~

The hierarchical components' identifier could be found by the "component-reference" list. The "index" attribute is used to order the list by the hierarchical relationship from topmost component (with the "index" set to 0) to bottom component.

#### Component-Specific Info Design

According to the management requirements from operators, some important attributes are not defined in {{!RFC8348}}. These attributes could be component-specific and are not suitable to define under the component list node. So, we defined a choice-case structure for this component-specific extension, as follows:

~~~~ ascii-art
  +--ro components
     +--ro component* [uuid]
        ...................................
        +--ro (component-class)?
           +--:(chassis)
           |  +--ro chassis-specific-info
           +--:(container)
           |  +--ro slot-specific-info
           +--:(module)
           |  +--ro board-specific-info
           +--:(port)
              +--ro port-specific-info
        ...................................
~~~~

Note: The detail of each *-specific-info YANG container is still under discussion, and the leaf attributes will be defined in future.

#### Part Number

According to the description in {{!RFC8348}}, the attribute named "model-name" under the component, is preferred to have a customer-visible part number value. "Model-name" is not straightforward to understand and we suggest to rename it as "part-number" directly.

~~~~ ascii-art
  +--ro components
     +--ro component* [uuid]
        ...................................
        +--ro part-number?           string
        ...................................
~~~~

### Equipment Room

Note: add some more attributes about equipment room in the future.

### Rack

Besides the common attributes mentioned in above section, rack could have some specific attributes, such as appearance-related attributes and electricity-related attributes.
The height, depth and width are described by the figure below (please consider that the door of the rack is facing the user):

~~~~ ascii-art

                 ----------------      ---
                /|              /|      |
               / |             / |      | 
              /  |            /  |      |
             ----|-----------|   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |    height
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   | Door    Q |   |      |
             |   |         Q |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   |           |   |      |
             |   /-----------|----     ---
             |  /            |   /      /
             | /             |  /      depth
             |/              | /      /
             -----------------      ---
             |______width____|
             |               |

~~~~
{: #fig-rack-appearance title="height, width and depth of rack"}

The rack attributes include:

~~~~ ascii-art
   +--ro racks
      +--ro rack* [uuid]
         ...................................
         +--ro height?              uint16
         +--ro width?               uint16
         +--ro depth?               uint16
         +--ro max-voltage?         uint16
         ...................................
~~~~

Max-voltage: the maximum voltage supported by the rack.

### Network Element

We consider that some of the attributes defined in {{?RFC8348}} for components are also applicable for network element. These attributes include:

~~~~ ascii-art
      +--ro network-elements
         +--ro network-element* [uuid]
            ...................................
            +--ro hardware-rev?    string
            +--ro firmware-rev?    string
            +--ro software-rev?    string
            +--ro mfg-name?        string
            +--ro mfg-date?        yang:date-and-time
            +--ro part-number?     string
            +--ro serial-number?   string
            +--ro product-name?    string
            ...................................
~~~~

Note: Not all the attributes defined in {{?RFC8348}} are applicable for network element. And there could also be some missing attributes which are not recognized by {{?RFC8348}}. We will do some more extensions after the missing attributes are fully discussed.

## Efficiency Issue

During  the integration with OSS in some operators, some efficiency/scalability concerns have been discovered when synchronizing network inventory data for big networks.  More discussions are needed to address these concerns.

Considering that relational databases are widely used by traditional OSS systems and also by some network controllers, the inventory objects are most likely to be saved in different tables. With the model defined in current draft, when doing a full synchronization, network controller needs to convert all inventory objects of each NE into component objects and combine them together into a single list, and then construct a response and send to OSS or MDSC. The OSS or MDSC needs to classify the component list and divide them into different groups, in order to save them in different tables. The combining-regrouping steps are impacting the network controller & OSS/MDSC processing, which may result in efficiency/scalability limitations in large scale networks.

An alternative YANG model structure, which defines the inventory objects directly, instead of defining generic components, has also been analyzed. However, also with this model, there still could be some scalability limitations when synchronizing full inventory resources in large scale of networks. This scalability limitation is caused by the limited transmission capabilities of HTTP protocol. We think that this scalability limitation should be solved at protocol level rather than data model level.

In case there are some other special types of inventory objects that could be used in other technologies and have not been considered by us, we would like to provide a generic model. If we define the inventory objects directly and give them fix hierarchical relationships in YANG model, once there is a new type of inventory object that needs to be introduced into the model, we need to break down our YANG model and insert the new one, this is not a backward compatible change and therefore is not an acceptable approach for implementation. With a generic model, we only need to augment a new component class and extend some specific attributes for this new inventory component class, which is more flexible. We consider that this generic data model, enabling a flexible and backward compatible approach for other technologies, represents the main scope of this draft. Solution description to efficiency/scalability limitations mentioned above is considered as out-of-scope.

## Some Other Considerations

Note: review in future versions of this document whether the component list should be under the network-inventory instead of the network-element container.

Note that in {{?RFC8345}}, topology and inventory are two subsets of network information. However, considering the complexity of the existing topology models and having a better extension capability, we define a separate root for the inventory model. We will consider some other ways to do some associations between the topology model and inventory model in the future.

Note: review in future versions of this document whether network hardware inventory should be defined as an augmentation of the network model defined in {{?RFC8345}} instead of under a new network-inventory root.

The proposed YANG data model has been analysed so far to cover the requirements and use cases for Optical Network Inventory.

Further analysis of requirements and use cases is needed to extend the applicability of this YANG data model to other types of networks (IP and microwave) and to identify which aspects are generic and which aspects are technology-specific for optical.

{: #ni-tree}

# Network Hardware Inventory Tree Diagram

{{fig-ni-tree}} below shows the tree diagram of the YANG data model defined in module ietf-network-inventory.yang ({{ni-yang}}).

~~~~ ascii-art
{::include ./ietf-network-inventory.tree}
~~~~
{: #fig-ni-tree title="Network inventory tree diagram"
artwork-name="ietf-network-inventory.tree"}

{: #ni-yang}

# YANG Model for Network Hardware Inventory

~~~~ yang
{::include ./ietf-network-inventory.yang}
~~~~
{: #fig-ni-yang title="Network inventory YANG module"
sourcecode-markers="true" sourcecode-name="ietf-network-inventory@2022-07-11.yang"}

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

