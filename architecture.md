# Architecture

##

## Entities

The domain model underneath show the entities a their relationships to each other. The abstracted world view of the system so to speak.

Everything is and _Identity_ which can be associated with multiple _CoinAddress_es. A _CoinAddress_ represents the address or identifier on a blockchain and follows the derivation path of a master key. As an _Identity_ can bis associated with multiple _CoinAddresses,_ those identities can operate on multiple blockchains at the same time. All sub-classes of an _Identity_ can operator on blockchains as well.

An _Identity_ can either be a _Device_ or a _User. Devices_ are associated with _Measurements_ that are created in the system based on the measurements of a physical device. _Devices_ can further be specialised as _EnergyConsumptionUnits_ and _EnergySources._

_EnergyConsumptionUnits_ represent everything that consumes energy and they are always associated with one _Member._

_EnergySources_ on the other hand are devices that produce energy and are associated with one or multiple _Shares_. Where _Members_ can own multiple _Shares_ of an _EnergySource._

_Members_ are specific form of a _User._

Operators are not considered in the domain model as their purpose is only to operate on the entities described above.



<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F37URXugGKPWDi5ErP0ov%2Fuploads%2FC84eHuc8gKVY10SKo8Wz%2FMyPower%20-%20Class%20Diagram.svg?alt=media&#x26;token=7ee6ed7c-2ca0-4995-800d-71e22797346a" alt=""><figcaption></figcaption></figure>

## Components

They system considers various environments with their components:

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F37URXugGKPWDi5ErP0ov%2Fuploads%2FDqUEsa6PnHjhtlVDKwgt%2FMyPower%20-%20Component%20Diagram.svg?alt=media&#x26;token=375a41a3-5baa-4cac-ba51-a7fb0953ac51" alt=""><figcaption></figcaption></figure>

### Device Environment

Those components are installed at the physical device that should be considered in the system. This can either be an energy source like a solar panel, as well as a consumption unit like the flat of a member.

In order to receive measurements of a device a _Meter_ needs to be present. A _Trusted Gateway_ is attached to the _Meter_ and queries in a predefined time interval its measurements. To be able to proof the integrity of the measurement at any time, the _Trusted Gateway_ creates a digital signature based on the measurements. Those information will be encrypted and sent via Lora to a _Lora Gateway_ from which it will be forwarded to the LoraWan Provider.

To transmit metering data from the infrared customer interface of a smart meter like it is used by the Wiener Netze, we connect an IR sensor to the smart meter and via USB to the Trusted Gateway. The other protocols are used similarly with respective USB dongles.

The current data flow of the metering data using the Trusted Gateway is:

1. The Trusted Gateway queries in regular time intervals (currently 15 minutes) the _absolute energy_ together with a timestamp from the smart meter,
2. A hash of the payload from the meter is created
3. The hash is signed with the private key stored in the Secure Element
4. The payload together with the previous created signature is sent via LoRaWan to nearby _Lora Gateway_
5. The Lora Gateway forwards the LoRa message via TCP/IP to a LoRa Wan Provider. We are currently using [TheThingsNetwork](https://www.thethingsnetwork.org/). (The Trusted Gateway was registered to the LoRaWan provider beforehand!)
6. The backend service connects to the LoRaWan provider via a publish-subscriber pattern so that any message sent by the Trusted Gateway will be forwarded to the backend.
7. The backend verifies the integrity of the data by using the public key of the Trusted Gateway by creating a hash of the payload and comparing it to the digital signature created by the device.
8. If the data is valid, the application either only stores the measurement in its database (Consumption), or mints KWH tokens on Polygon and distributes it to the shareholder of the energy source (Production).

The components of the Trusted Gateway Lora, can be found

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F37URXugGKPWDi5ErP0ov%2Fuploads%2FrfJyeuJZLGS1l7HvPVS5%2F1ed809af-53f2-4c00-86d9-b117fc55c81a.png?alt=media\&token=91222f04-6b29-4504-99c2-41f9dd0b3db4) ![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F37URXugGKPWDi5ErP0ov%2Fuploads%2FA0Bw9SZlQ5AQFVmhdzrE%2F72cd6ada-9b73-4aae-9f52-11fa09d0bffa.png?alt=media\&token=089b90ab-62cf-45ed-a2a8-f7c16b8232e1)

### LoraWan Provider <a href="#lorawan-provider" id="lorawan-provider"></a>

This is the environment of an external service provider. The service it is hosting is called _TheThingsNetwork_ which is a messaging broker for Lora devices.

**The Things Network**

[https://www.thethingsnetwork.org/](https://www.thethingsnetwork.org/)

### Riddle & Code <a href="#riddle-and-code" id="riddle-and-code"></a>

This components are deployed within three datacenter located in Austria. The business logic is implemented in the _MyPower-Backend_ that subscribed to _TheThingsNetwork_ and awaits measurements from devices. Based on the information stored in the _SQL Database_ those measurements can be decrypted and associated with devices added to the system. For the production of energy sources it creates blockchain transactions by using the _Signature Broker_ and _Signers._

Instead of receiving measurements from TheThingsNetwork, the system can use a _Device Broker_ where information from devices can be sent to. It uses an MQTT protocol and a publish subscriber pattern between the devices and the _MyPower Backend._

The _MyPower Frontend_ provides the users a graphical interface to interact with the system. It is served via _NginX_ that is used as a web server as well as a proxy to for requests to the _MyPower Backend._

The authentication to the system is handled by the _Identity and Access_ management component. It is a KeyCloak instance and uses the industrial standard for authentication OAuth2. The system works without this component and the purpose of it is to link the cryptographic identities of the _MyPower Backend_ with the information from the users like, name and email. This component can either be deployed on customer side or can be offered by Riddle\&Code as a service.

**MyPower Backend**&#x20;

Github: [https://github.com/RiddleAndCode/energy-community](https://github.com/RiddleAndCode/energy-community)

An description of the API can be found under following URL

`1<your-instance-url>/riddleandcode/energy-community/api/v1/redoc`

**MyPower Frontend**

Github: [https://github.com/RiddleAndCode/energy-community-frontend](https://github.com/RiddleAndCode/energy-community-frontend)

**Signer**

[https://github.com/RiddleAndCode/tx-builder](https://github.com/RiddleAndCode/tx-builder)

**Signature & Device Broker**

[https://www.rabbitmq.com/](https://www.rabbitmq.com/)
