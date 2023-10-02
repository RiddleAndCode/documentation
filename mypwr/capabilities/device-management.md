# Device Management

Devices are an essential part of the system and needs to be managed. In this release we’re enabling operators to add energy sources to the system. Each member of the system will be associated with an energy consumption unit once it become a member.

Devices are associated with physical machines via a public keys or with a brute-force algorithm using a decryption key.

Energy Sources can be added to the system by an operator by using a simple form. During this process an energy sources gets tokenized. Once added to the system, measurement about a device can be requested

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F37URXugGKPWDi5ErP0ov%2Fuploads%2Fjnl6SpD3scMiS57jKtRc%2Fc8fcd1d3-0956-4f82-9f64-1fe5ce8e3376.png?alt=media\&token=d6548cf0-8f11-4501-a2f7-a989daa97bc7)

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F37URXugGKPWDi5ErP0ov%2Fuploads%2FhBiAdsDwAh30jYFLsVe7%2F757dfc6c-d1ee-4eb7-8549-98456fc5184d.png?alt=media\&token=b21bc9a0-fedd-4104-b059-22779b21e079)

#### Brute Force <a href="#brute-force" id="brute-force"></a>

If the measurements of a device are encrypted and a decryption was added for a device, the system will try to match the measurements of physical devices with the device in the system. This is done by trying to decrypt every incoming measurement, once it found a measurement where the decryption key is working, it will link the partial public key of the physical device from the measurement and add this information to the device in the system. The system will no longer use this decryption key in its brute force algorithm.

#### Device Brokers <a href="#device-brokers" id="device-brokers"></a>

Measurements can be set to the system by using two different technologies. Both use a publish subscriber pattern where measurements are published by the Trusted Gateways attached to the physical machines in a given time interval.

**The Things Network**

Measurements are sent via Lora to a LoraWan provider called TheThingsNetwork. Therefore, the devices need to be registered to an application (messaging queue) on the TheThingsNetwork where the measurements are published too. The backend subscribes to this application and receives in measurements that are further processed.

**MQTT Broker**

The MQTT Broker works similar to TheThingsNetwork, but instead of sending measurements via LoRa to the broker, it uses TCP.
