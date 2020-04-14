# MCCS

## Overview

The mutual credit communication system (MCCS) is a web application that enables a network of trusted individuals and businesses to pay each other without the need for conventional money. 

> _What is mutual credit?_
> 
> Mutual credit provides a mechanism for businesses to trade without money, via a credit clearing system. A credit clearing system is an arrangement in which a group of traders, each of whom is both a buyer and a seller, agree to allocate each other sufficient credit to facilitate their transactions within the network. [🔗](https://open.coop/collaborate/mutual-credit/)

At its core, MCCS is an accounting system that facilitates trading amongst a group of traders who initiate mutual credit (MC) transfers between each other using the MCCS web application. Group governance could be implemented in a number of different ways (see the [Open Credit Network](https://opencredit.network) (OCN) for example), but that is beyond the scope of MCCS, which is simply the web application that facilitates trade discovery and MC transfers between its users.

## Design

The MCCS API is built based on the following data model and functionality:

- [Data Model](alpha-data-model.md)
- [Functionality](alpha-functionality.md)

## Roadmap

### Phase 1 - Standalone MCCS Node (alpha release)

**Create a standalone node that anyone can use in their community**

1. **DONE** - [Proof of concept](https://github.com/ic3network/mccs-alpha)
    - Provide a web-based application that enables OCN members to:
        - Discover each other's products/services and needs
        - Facilitate MC transfers between them
2. **IN PROGRESS** - [API](https://github.com/ic3network/mccs-alpha-api)
    - Enable developers to create a customizable user interface (any language, different users flows, device optimization (i.e., mobile app), etc.)
    - Exposes MCCS functionality for integration with other systems (e.g., instruct a MC transfer from within another application)
3. Build a front-end user interface for MCCS node admins and MCCS node users using the new API
    - Provide an example for front-end developers for further customization and localization

### Phase 2 - Interconnected MCCS Nodes (beta release)

**Connect two or more standalone nodes together into a network to enable inter-node trade discovery and mutual credit transfers**

1. Define and design the communication protocol for MCCS nodes
    - Currently reviewing the [Credit Commons](https://www.creditcommons.net/) [Protocol](https://gitlab.com/credit-commons-software-stack/credit-commons-microservices) as a protocol candidate
2. Extend the API to facilitate interconnected nodes
3. Extend the user and admin front ends

## Get Involved

Take a look at our [proof of concept](https://github.com/ic3network/mccs-alpha) (will not be developed further) and [API](https://github.com/ic3network/mccs-alpha-api) (actively being developed) repositories to see the work we have done so far.

We are looking for talented individuals with relevant technical (e.g., Golang, React/Javascript, front-end web design) or governance (e.g., credit risk management) background to help design and develop MCCS. If you are interested, please reach out to us at _mccs_ at _ic3_ dot _dev_.
