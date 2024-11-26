# SSI Turkey DID Method Specification
## Draft, 25.11.2024
## BILGEM Blockchain Research Laboratory


The **tur** method is designed to generate decentralised identifiers utilised in Turkey's SSI Digital Identity System to create digital identity credentials. SSI Digital Identity System is built by TUBITAK BILGEM, which supports the Self-Sovereign Identity (SSI) model and is governed by its own community. Self-Sovereign Identity (SSI) is a model that gives individuals full ownership and control of their digital identities without relying on a third party. 

Please refer to https://ssiturkiye.bag.org.tr/ for further details.

SSI Turkey Identity System is built on Hyperledger Indy blockchain infrastructure. Hyperledger Indy is a public ledger designed specifically and only for privacy-preserving self-sovereign identity. 

**indy-did-method** and **sovrin-method** serve as conceptual and practical inspirations for **tur** as they are all built on top of the Hyperledger Indy ledger. SSI-Türkiye ecosystem plays a significant role in shaping the principles and governance frameworks for decentralized identity and interoperable DID methods in the Turkish Digital Identity System that fosters digital identity usage in Turkey’s public services, private sector applications, and national regulations.

This specification conforms to the requirements specified in the **indy-did-method** and **sovrin method** and DIDs specification published by the W3C Credentials Community Group.

## Status of this Document
This is a draft document. It may be periodically updated, replaced or removed without notice at any time.

## DID Method Name
The method's name that identifies this DID method SHALL be **tur**.

A DID that uses this method MUST begin with the following prefix: did: tur. Per the DID specification, this string MUST be in lowercase. The remainder of the DID, after the prefix, is specified below.

## Method Specific Identifier
The copyright DID scheme is defined by the following specifications:
```sh
tr-did = "did" : tr-method-name : tr-specific-id
tr-method-name	= "tur"
tr-specific-id	= UUID
```
Refer to [RFC4122](https://www.ietf.org/rfc/rfc4122.txt) for UUID. UUID is an identifier within the namespace of a Hyperledger Indy network that is unique for that namespace.

An example of DID is as follows:
```sh
did:tur:9f6a4fcd-7ae5-4de8-a104-5c8f303bc5a6
```

## DID Documents

Refer to [DID specification](https://w3c.github.io/did-core/) for further details.

## CRUD Operation Definitions

This section is conformant to **(https://hyperledger.github.io/indy-did-method/#did-operations)** section.

### Create

The issuer, holder, and verifier can generate their own DID and DID documents and optionally register through the Turkey SSI DID Registrar. This specification does not require DID and DID documents to be registered.

It is recommended that the issuer, holder and verifier create their own DID and DID documents.

In general, the holder's DID will be designated as the DID controller of the DID document, but not necessarily. 

DID creation details align with **https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html#crud-operation-definitions**

#### DID Service Endpoint

DID service endpoint creation details align with **https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html#crud-operation-definitions**

### Read/Resolve

Read operations, including DID Service Endpoint, Resolver DID Document Format, are aligned with **https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html#crud-operation-definitions**

For more information, Refer [DID Specification](https://www.w3.org/TR/did-core/) and [Decentralized Identifier Resolution](https://w3c-ccg.github.io/did-resolution/)


### Update
If a delegation of rights occurs(for example, when Alice delegates copyright/asset ownership to Bob), the DID controller must be changed from the DID of the delegator (Alice) to the DID of the delegatee (Bob). In this case, the delegator (Alice) can change this DID document. 

If there is a target property in the DID document, it is recommended that this value is not changed once the target property is designated. If you want to change the target property, it is recommended that you create a new DID and DID document rather than changing the target property.

DID Update details align with **https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html#crud-operation-definitions**


### Deactivate/Revoke

When the DID is deactivated, a DID document that has this DID as a DID controller must not exist. If a non-existent DID is specified in the DID controller of the DID document, the management of the DID document may become impossible.

Deactivation details align with **https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html#crud-operation-definitions**

## Privacy Considerations

The data of the **tur** name will be referred to as "The Information" in the following text.

### Keeping PII off-chain
Regardless of encryption, The Information should not include Personally Identifiable Information (PII). The Information should contain only did, public keys, and service endpoints.

### Name Tracing
When any data (e.g. W3C Verifiable Credentials) is associated with **tur** DIDs, sharing that data would also impose sharing the onchain data graph (e.g. transaction history, NFTs, etc.) of the payload that owns the **tur** name.

### Disclosure
The information and its historical data are stored on the ssi-turkiye blockchain platform. Users should understand that on-chain data is public and does not have limitations on its use or disclosure.

### Security considerations
The DID controller of the DID document should be managed so that the owner's DID, such as the creator, can be designated. The  DID registrar may verify the holder's authentication when registering the DID document.

**tur** is based on the blockchain ( Hyperledger Indy ), which is public permissioned, and anyone who wants to publish DIDs needs to get the role of Trust Anchor on the ledger. A BLS key identifies each node. To add a node to a network, an agent needs to send a transaction(including the public key and node IP) to add that node to the existing network. The transaction usually needs to be signed by an agent who controls a key(ED25519) and has the role of trustee and steward on the network.

Further security considerations align with **https://github.com/hyperledger/indy-did-method** and **https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html**



## References

- [DID Specification](https://www.w3.org/TR/did-core/)
- [Decentralized Identifier Resolution](https://w3c-ccg.github.io/did-resolution/)
- https://hyperledger.github.io/indy-did-method/
- https://sovrin-foundation.github.io/sovrin/spec/did-method-spec-template.html
