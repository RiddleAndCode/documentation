# Trust Anchor & HW-03

The Trust Anchor is a combination of hardware and software that links the physical world with the digital one.&#x20;

<figure><img src="../.gitbook/assets/r&#x26;c_trust_anchor (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

The Trust Anchor is a compact and sophisticated hardware wallet device measuring 24.2x31.2x9.3 cm. It includes a USB-C, Secure Element, Cryptographic Wallet, CPU, ample storage space, and CPIOS, all packed with cutting-edge technology.

This device is the cornerstone of the RDDL Network Blockchain, providing unique digital identities for associated devices. It goes beyond traditional constraints, solving the _Oracle Problem_ and establishing a reliable and trusted data source. It seamlessly attaches to various machinery, effortlessly capturing raw data at the source.

Once linked to a machine, the Trust Anchor enhances communication through an open cryptographic protocol or direct interface if embedded. The accompanying service software, 0x21e8, and optional rddl-client simplify the connection to Planetmint, the metadata storage, and Liquid, the token creation platform. This ensures a user-friendly experience for setting up your desired business model.



***

## **Trust Anchor vs HW-03 Device**

The **Trust Anchor** and **HW-03** are both pivotal components in the technological ecosystem. However, they serve distinct purposes and possess unique features. To understand them better, let's delve into their primary characteristics and compare their configurations for different industry solutions.

#### **Trust Anchor:**

* **Core Function:** The Trust Anchor operates as the foundational hardware wallet essential for connecting to a machine. It's designed to provide the primary layer of secure and trusted interaction.

#### **HW-03:**

* **Core Function:** While the HW-03 incorporates the foundational elements of the Trust Anchor, it differentiates itself by adding industry-specific features, enhancing its utility for particular applications.

#### **Comparative Configurations:**

1. **Energy Solution Components:**
   * **Trust Anchor:** Fundamental hardware wallet for secure connection.
   * **RPI Zero:** A mini computer that can run various programs and functions.
   * **USB HUB:** Allows for the connection of multiple USB devices.
   * **RF Module:** Facilitates wireless communication.
2. **Industry Solution Components:**
   * **Trust Anchor:** Base component for connection and security.
   * **Battery Pack:** Provides a portable power source.
   * **RF Module:** Enables wireless data transmission.
   * **Power Management:** Controls and manages power distribution.
   * **iMX8:** A modern processing unit offering high performance.
   * **Power Supply Unit:** Supplies electrical power to the device.
   * **M-12 Connector:** A circular connector for industrial applications.
   * **CAN Transceiver:** Provides a physical layer for the CAN protocol, enabling communication.

In essence, while the Trust Anchor is a foundational piece of hardware focused on secure connectivity, the HW-03 is a more versatile, industry-adapted device that incorporates the Trust Anchor and builds upon it with additional components tailored to specific use cases.



***

## **In a Nutshell: How it Works**

* Connect the Trust Anchor and/or HW-03 device\* to the machine.
* Once connected, it will automatically trigger the Master Identity creation (Public and Private Key pair) representing the machine on the blockchain.
* Machine/HW-03 device gathers productivity data and creates a unique fingerprint (CID) of this metadata using a hashing algorithm.
* Trust Anchor creates a transaction on Planetmint, signing it with the machine’s identity and storing the CID on Planetmint.
  * the original notarised data is stored on cloud storage or on-premise storage, or distributed storage like IPFS. Other data storage solutions are also possible.
* The productivity data of the machine can be verified through the “Resolver” service of RDDL Network comparing CIDs.



<figure><img src="../.gitbook/assets/Trust Anchor Product Folder - V1.png" alt=""><figcaption></figcaption></figure>

## **Have a Look**

{% embed url="https://www.youtube.com/watch?v=iLwzdibJztA" %}
