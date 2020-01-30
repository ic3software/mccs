# MCCS

Looking for the code? See the [alpha release](https://github.com/ic3network/mccs-alpha) repository.

## Overview

The mutual credit communication system (MCCS) is a web application that enables a network of trusted individuals and businesses to pay each other without the need for conventional money. 

> _What is mutual credit?_
> 
> Mutual credit provides a mechanism for businesses to trade without money, via a credit clearing system. A credit clearing system is an arrangement in which a group of traders, each of whom is both a buyer and a seller, agree to allocate each other sufficient credit to facilitate their transactions within the network. [🔗](https://open.coop/collaborate/mutual-credit/)

At its core, MCCS is an accounting system that facilitates trading amongst a group of traders who initiate mutual credit (MC) transfers between each other using the MCCS web application. Group governance could be implemented in a number of different ways (see the [Open Credit Network](https://opencredit.network) (OCN) for example), but that is beyond the scope of MCCS, which is simply the web application that facilitates MC transfers between its users.

## Roadmap

### Phase 1 - Standalone MCCS Node

**Create a standalone node that anyone can use in their community**

- **DONE** - Initial [alpha release](https://github.com/ic3network/mccs-alpha) to enable OCN to prove the concept
  - Provide a web-based application that enables OCN members to:
    - Discover each other's products/services and needs
    - Facilitate MC transfers between them
- **IN PROGRESS** - [API for the alpha software](https://github.com/ic3network/mccs-alpha-api)
  - Allow MCCS functionality to be integrated with other systems (e.g., instruct a MC transfer from within another application)
- Build a front-end for end users using the new API
  - Enable developers to create a customizable user interface (any language, different users flows, device optimization (i.e., mobile app), etc.)
- Build a front-end for admin users using the new API
  - Enable developers to create a customizable admin interface

### Phase 2 - Interconnected MCCS Nodes

**Connect two or more standalone nodes together into a network to enable inter-node business discovery and credit transfers**

- Define and design the communication protocol for MCCS nodes
  - Currently reviewing the [Credit Commons](https://www.creditcommons.net/) [Protocol](https://gitlab.com/credit-commons-software-stack/credit-commons-microservices) as a protocol candidate

## Get Involved

Take a look at our [alpha release](https://github.com/ic3network/mccs-alpha) and [API](https://github.com/ic3network/mccs-alpha-api) repositories to see the work we have done so far.

We are looking for talented individuals with relevant technical (e.g., Golang, React/Javascript, front-end web design) or governance (e.g., credit risk management) background to help design and develop MCCS. If you are interested, please reach out to us at _mccs_ at _ic3_ dot _dev_.
