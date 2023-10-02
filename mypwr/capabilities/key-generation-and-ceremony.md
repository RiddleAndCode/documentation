# Key Generation and Ceremony

The key ceremony is the confidential creation of a master key in the key store. The master key is used to derive further addresses and to manage their assets.

The identity who has access to the master key owns the assets of the system!

#### Paradigms of a Key Ceremony <a href="#paradigms-of-a-key-ceremony" id="paradigms-of-a-key-ceremony"></a>

* Secure way to create and store key material
* Only the client has access to the key material inside the enclave of a Trusted Execution Environment (TEE) at any point in time
* An audited solution that proves that the technology provider (Riddle & Code) cannot access the Trusted Execution Environment and the key material
* The key material can be recovered by the client in case of a disaster

#### Process of creating the master key <a href="#process-of-creating-the-master-key" id="process-of-creating-the-master-key"></a>

1. User triggers the generation of a random number via the user interface
2. A random number is created inside the Hardware Secure Module (HSM)
3. The random number is used to generate a seed
4. A mnemonic phrase and master key generation is performed
5. The master key is stored in a Trusted Execution Environment to prevent anybody to access it

#### Backup of the master key <a href="#backup-of-the-master-key" id="backup-of-the-master-key"></a>

1. The mnemonic phrase is exposed via the user interface
2. The mnemonic phrase can be stored via steel plates

The mnemonic phrase and the option to back it up is **only available once** during the key ceremony. Hence, the mnemonic phrase cannot be retrieved at a later point.

#### Recovery option in case of disaster <a href="#recovery-option-in-case-of-disaster" id="recovery-option-in-case-of-disaster"></a>

If anything should happen to the system the keys and their assets can be restored using the backup of the master key.

1. the user enters the 24 words of the mnemonic phrase via the user interface
2. The master key is created and stored again in the Trusted Execution Environment

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F37URXugGKPWDi5ErP0ov%2Fuploads%2FaX6W1Tj9MT4tIza2Ofnx%2F0585b5cf-ca7f-47a9-a347-c0800cb66f61.png?alt=media&#x26;token=54ee7624-022e-45a6-9fe7-a12a6eeba43b" alt=""><figcaption></figcaption></figure>

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F37URXugGKPWDi5ErP0ov%2Fuploads%2F7lM7WfFkcB1POwDkI75s%2F5c4874db-3be2-4a91-9f92-f97bea5f3dad.png?alt=media&#x26;token=f2ca2623-3dd3-4e06-bb4e-f9f41372910b" alt=""><figcaption></figcaption></figure>
