---
coding: utf-8

title: Inventory YANG Data Model in Optical Networks 

abbrev: Optical Inventory YANG
docname: draft-xx-ccamp-optical-inventory-yang-00
workgroup: CCAMP Working Group
category: std
ipr: trust200902

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Haomian Zheng
    org: Huawei Technologies
    street: H1, Xiliu Beipo Village, Songshan Lake
    city: Dongguan
    country: China
    email: zhenghaomian@huawei.com
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
  information. It augments the generic YANG model entities and can be used
  for resource management. 

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
   
  TBD: review the related modules, depending on the augmentation relationship. 
  TBD: give the augmentation relationship. 

# Terminologies

## Terms on Network Equipment 

  TBD: Recap the concept of chassis/slot/component/board/... in TMF.
   
  Following terms are used for representation of the hierarchies in the 
  optical network inventory. 
   
  Network Element:
   
  Cabinet：a combination of rack, chassis and shelf. 
   
  Chassis: 
   
  Slot: 
   
  Component: 
   
  Board/Card:    
   

## State of Network Equipment: 

  Empty: no equipment is installed and no expected equipment has been identified; 
   
  Installed & not expected: physically inserted in the NE but not expected;
   
  Expected & not Installed: expected but not currently installed;
   
  Installed & Expected: expected and currently installed;
   
  Mismatch of Installed & Expected: there is an inconsistency between the expected equipment and the installed equipment;
   
  Unavailable: this holder cannot accept the installation or provisioning of equipment (this is typically caused by a double width card installed next to this slot);
   
  Unknown: the state of the equipment are not known;

## Model Structure

  TBD: Top-down relationship from the above terms.
   

   


# YANG Data Model for Optical Network Inventory 

## YANG Model Overview

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
{: #fig-yang title="Inventory Model Position"}

  In this document, names of data nodes and other data model objects
  are prefixed using the standard prefix associated with the
  corresponding YANG imported modules, as shown in the following table.

| Prefix      | YANG module             | Reference
| nw          | ietf-network            | {{!RFC8345}}
| nt          | ietf-network-topology   | {{!RFC8345}}
| ninv        | ietf-network-inventory  | This Document         
{: #tab-prefixes title="Inventory Related Model and Prefixes"}

## MPI YANG Model Tree

# YANG Code for Optical Network Inventory

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
