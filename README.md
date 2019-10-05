
# Dark Crystal Protocol Specification (WIP)

![dark crystal icon](./assets/dark-crystal-icon_200x200.png)

## Introduction

## Terms used

- ***Secret*** -
- ***Secret-owner*** -
- ***Shard*** - 
- ***Custodian*** -

## Scenarios

## Setup process

### Step 1 - Combine secret with contextual metadata

This is to indicate the intended purpose of the secret, meaning that it is still useful if recovered 'out of context'. This will generally include a 'label' property which will be a human readable description, including, for example, the name of the application it is useful for. This may also include application-specific data. This is because, as Pamela Morgan makes clear in her book 'Cryptoasset inheritance planning', recovering a key is only half the story.  For it be useful, we need to know what to do with it.

The amount of information included here depends on how critical it is that share size is kept small.

### Step 2 - Encrypt data with symmetric key

If the data to be backed up is larger than *maxbytes* bytes, the data is encrypted with a symmetric key and this key is taken to be the secret. Otherwise, the data itself is taken to be the secret. It needs to be noted that many implementations of secret sharing do this internally, and produce shares which are a concatonation of a key-share and the encrypted secret.

This means there is some duplication of data - a portion of each share is identical to the others. So in the case of particularly large secrets, it makes sense if the encrypted secret is stored only once in a place which is accessible to all share-holders (if the practicalities of the chosen transport layer make this possible).

### Step 3 - Message Authentication Code added

The secret is appended with it’s SHA-256 hash which serves as a message authentication code (MAC). This allows us to later verify that the secret has been correctly recovered.

It is assumed that in step 2, the symmetric encryption algorithm used will also use a MAC.

### Step 4 - Shards generated

Shards are generated using a secure threshold-based secret sharing algorithm. 

### Step 5 - Shards are signed

Each shard is signed by the owner of the secret using a keypair with an established public key (such as the same keypair used to sign other messages in the application). 
Shards are appended with these signatures.

### Step 6 - Schema version number added

To ensure backward compatibility with future versions of the protocol.

### Step 7 - Signed shards encrypted for each custodian

Shards are encrypted with the public key of each custodian and represented as base64 strings. The unencrypted shards are removed from memory. 

### Step 8 - Transmission

Each encrypted shard is packed together with some metadata into a message, transmitted to the custodian, and a local (encrypted) copy is retained.

TODO: explain process of keeping a personal copy with serves as a reference that the shard was sent, but the shard data itself cannot be read by the secret-owner.

## Recovery process

TODO: 
* Upon loss of data, the secret owner establishes a new account. 
* They contact the custodians out of band to confirm that the new identity belongs to them. 
* Each custodian sends the shard they were holding to the new account. 
* The signatures are validated with the original public key, proving that the returned shards are identical to those sent out. 
* The shards are combined to recover the secret, and the MAC is used to establish that recovery was successful. 
