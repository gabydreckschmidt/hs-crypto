---

copyright:
  years: 2018, 2021
lastupdated: "2021-01-29"

keywords: release note, new, changelog, what's new, service updates, service bulletin

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:pre: .pre}
{:important .important}
{:external: target="_blank" .external}

# Release notes
{: #what-new}

Stay up-to-date with the new features that are available for {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

<!--
### Updated: The cryptography algorithm that is used to generate signature keys
{: #update-signature-key-algorithm}

The cryptography algorithm to generate signature keys is updated from Rivest–Shamir–Adleman 2048 (RSA 2048) to P521 Elliptic Curve (P521 EC). The cryptographic strength of P521 EC keys is equivalent to RSA 15360, which means the updated signature keys can provide the higher level of security comparing to the previous signature keys. The previous RSA 2048 signature keys are still valid and can be used.
-->

## January 2021
{: #january-2021}

## Added: Support for a single-tenant KMIP adapter

{{site.data.keyword.hscrypto}} now provides a single tenant KMIP adapter to manage the key distribution in the vSphere or vSAN environment. For more information, see [Configuring KMIP in {{site.data.keyword.hscrypto}} for key management and distribution](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware).

## December 2020
{: #december-2020}

### Added: `ReencryptSingle` function in GREP11 API
{: #add-reencryptsingle-function-grep11}

The GREP11 API now supports the `ReencryptSingle` function which enables you to decrypt data with the original key and subsequently encrypt the raw data with a different key in a single call within the cloud HSM. This single call is a viable option where a large amount of data needs to be reencrypted with different keys, and bypasses the need to perform a combination of `DecryptSingle` and `EncryptSingle` functions for each data item that needs to be reencrypted. For more information, see [GREP11 API reference - `ReencryptSingle` function](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-ReencryptSingle).

### Added: Support for the SLIP10 mechanism and Edwards-curve algorithm
{: #add-slip10-eddsa}

{{site.data.keyword.hscrypto}} now supports the SLIP10 mechanism for hierarchical deterministic wallets to derive private and public key pairs. It now also supports the Edwards-curve (ED) 25519 and ED448 algorithms for digital signatures. Before you can use ED algorithms, make sure to enable this feature by following the instructions in [Enabling Edwards-curve Digital Signature Algorithm](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-EdDSA).

<!--
### Added: Managing EP11 keystores and keys with the {{site.data.keyword.cloud_notm}} console
{: #add-ep11-keystores-keys-console}

Apart from using the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) to manage Enterprise PKCS #11 (EP11) keystores and keys, you can now use the {{site.data.keyword.cloud_notm}} console to view, create, and delete EP11 keystores and keys. For more information, see [Managing EP11 keystores with the {{site.data.keyword.cloud_notm}} console](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui) and [Managing EP11 keys with the {{site.data.keyword.cloud_notm}} console](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui).
-->

### Added: Using Terraform to manage {{site.data.keyword.hscrypto}} instances and resources
{: #add-terraform}

Terraform is an open source software that enables you to configure and automate cloud resource provisioning and management. Now you can provision and initialize {{site.data.keyword.hscrypto}} instances, as well as managing root keys and standard keys with the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in. For more information, see [Managing key management service resources with Terraform](/docs/terraform?topic=terraform-kms-resources), [Retrieving key management service data with Terraform](/docs/terraform?topic=terraform-kms-data-sources), and the [sample Terraform template for {{site.data.keyword.hscrypto}}](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-hpcs-crypto){: external}.

### Added: Provisioning and managing service instances with the private-only network
{: #add-private-only-network}

To achieve increased security, you can now limit the network access to your service instance to the private-only network. You can either [choose the allowed network when you provision the service instance](/docs/hs-crypto?topic=hs-crypto-provision) or [update the network access policy after you set up the instance](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies).

Before you update the network access policy, you need to initialize the service instance first. See [Initializing service instances with the IBM Cloud TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) for instructions.
{: important}

### Added: Support for accessing service instances through the Virtual Private Endpoint
{: #add-vpe}

You can now connect your {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) instance to your {{site.data.keyword.hscrypto}} instance through a virtual private endpoint (VPE) gateway, so that you can manage your keys using {{site.data.keyword.hscrypto}} through a private network. For more information, see [Securing connection to {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-secure-connection) and [Create a {{site.data.keyword.hscrypto}} VPE gateway for VPC](/docs/hs-crypto?topic=hs-crypto-secure-connection#create-vpe-gateway).

### Added: Managing the key create and import access policy
{: #add-key-create-import-access}

After you set up your {{site.data.keyword.hscrypto}} instance, you can enable and update the key create and import access policy to control actions permissions for root keys and standard keys. For more information, see [Managing the key create and import access policy](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess).

### Updated: Key management API
{: #update-kms-api-december}

The {{site.data.keyword.hscrypto}} key management API is updated with the following changes:

- Updated: The API methods for the following key actions are now transitioned to individual request paths. The generic path format (except the action of restoring a key) is `/api/v2/keys/<key_ID>/actions/<action>` where `key_ID` is the UUID of the key and `action` is the action name that you want to execute.
  - [Wrap a key](/apidocs/hs-crypto#wrapkey)
  - [Unwrap a key](/apidocs/hs-crypto#unwrapkey)
  - [Rewrap a key](/apidocs/hs-crypto#rewrapkey)
  - [Rotate a key](/apidocs/hs-crypto#rotatekey)
  - [Authorize deletion for a key with a dual authorization policy](/apidocs/hs-crypto#setkeyfordeletion)
  - [Remove an authorization for a key with a dual authorization policy](/apidocs/hs-crypto#unsetkeyfordeletion)
  - [Enable operations for a key](/apidocs/hs-crypto#enablekey)
  - [Disable operations for a key](/apidocs/hs-crypto#disablekey)
  - [Restore a key](/apidocs/hs-crypto#restorekey)

- Updated: You can now use the following two methods to manage the allowed network policy and the key create and import access policy:
  - [Set instance policies](/apidocs/hs-crypto#putinstancepolicy)
  - [List instance policies](/apidocs/hs-crypto#getinstancepolicy)

- Deprecated: [Invoke an action on a key](/apidocs/hs-crypto#actiononkey)

  This method is originally used for performing actions on a key, such as wrap, unwrap, and rotate. It is now replaced with individual request path for each action.

For more information about the API updates, see [{{site.data.keyword.hscrypto}} key management API reference](/apidocs/hs-crypto){: external}.

## November 2020
{: #november-2020}

### Added: Support for the BIP32 mechanism
{: #add-bip32-mechanism}

{{site.data.keyword.hscrypto}} now supports the Bitcoin Improvement Proposal 0032 (BIP32) standard for hierarchical deterministic wallets to define how to derive private and public keys of a digital wallet. To enable BIP 32, follow the instructions in [Enabling BIP32 deterministic wallets](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-BIP32).

### Added: TKE activity tracker events
{: #add-tke-at-events}

{{site.data.keyword.hscrypto}} now supports the Trusted Key Entry (TKE) events auditing. You can now use {{site.data.keyword.at_full_notm}} to monitor TKE activities and analyze failed actions. For more information, see [Auditing events for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-at-events).

## September 2020
{: #september-2020}

### Added: Support for performing cryptographic operations with the standard PKCS #11 API
{: #added-pkcs11}

{{site.data.keyword.hscrypto}} now supports performing cryptographic operations with the standard Public-Key Cryptography Standards (PKCS) #11 API.

With the support of PKCS #11 API, you don not need to change your existing applications that use PKCS #11 standard to make it run in the {{site.data.keyword.hscrypto}} cloud HSM environment. The PKCS #11 library accepts the PKCS #11 API requests from your applications and remotely accesses the cloud HSM to execute the corresponding cryptographic functions.

For more information about the PKCS #11 API use cases, see [Using Hyper Protect Crypto Services as PKCS #11 HSMs](/docs/hs-crypto?topic=hs-crypto-use-cases#pkcs11_hsm).

To learn more about the PKCS #11 API, see [Introducing PKCS #11](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro) and [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).

### Added: Master key rotation
{: #added-master-key-rotation}

You can now rotate your master key on demand by using the {{site.data.keyword.cloud}} Trusted Key Entry CLI plug-in so as to meet industry standards and cryptographic best practices. For more information on how it works, see [Master key rotation introduction](/docs/hs-crypto?topic=hs-crypto-key-rotation#master-key-rotation-intro).

For the detailed instructions, see [Rotating master keys](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli).

## August 2020
{: #august-2020}

### Added: Support for import tokens to securely upload encryption keys
{: #added-import-tokens}

If you have *Writer* or *Manager* access permissions, you can now create import tokens to enable added security for encryption keys that you upload to {{site.data.keyword.hscrypto}}.

To find out more about your options for importing keys, check out [Creating import tokens](/docs/hs-crypto?topic=hs-crypto-create-import-tokens). For a guided tutorial, see [Tutorial: Creating and importing encryption keys](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys).

## July 2020
{: #july-2020}

### Added: {{site.data.keyword.hscrypto}} expands into the Washington DC region
{: #added-wdc-region}

You can now create {{site.data.keyword.hscrypto}} resources in the Washington DC (US East) region.

For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

### Added: {{site.data.keyword.hscrypto}} aligns the key management functions with {{site.data.keyword.keymanagementserviceshort}}
{: #added-key-protect-concurrency}

{{site.data.keyword.hscrypto}}, built on FIPS 140-2 Level 4-compliant HSM, now supports the same level of key management functions as {{site.data.keyword.keymanagementserviceshort}}. The added functions include the following:

* [Policy-based key rotation](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy)
* [Viewing root key versions](/docs/hs-crypto?topic=hs-crypto-view-key-versions)
* [Disabling and enabling root keys](/docs/hs-crypto?topic=hs-crypto-disable-keys)
* Dual authorization policies for {{site.data.keyword.hscrypto}} [instances](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) and [keys](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy)
* [Viewing details about an encryption key](/docs/hs-crypto?topic=hs-crypto-view-key-details)
* [Viewing associations between root keys and IBM Cloud resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources)
* [Restoring a deleted key](/docs/hs-crypto?topic=hs-crypto-restore-keys)

## June 2020
{: #june-2020}

### Added: Support for quorum authentication
{: #added-quorum-authentication-202006}

Both the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in and the {{site.data.keyword.hscrypto}} Management Utilities now support [quorum authentication](/docs/hs-crypto?topic=hs-crypto-understand-concepts#quorum-authenticaion-concept).

Quorum authentication is the way to approve an operation by a set number of crypto unit administrators. Some sensitive operations require a sufficient number of crypto unit administrators to enter their credentials. Setting the [signature thresholds](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept) to a value greater than one enables quorum authentication.

For information on how to initialize a service instance using the TKE CLI and enable quorum authentication, see [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

For information on how to initialize a service instance using the Management Utilities and enable quorum authentication, see [Setting up the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) and [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

## April 2020
{: #april-2020}

### Added: {{site.data.keyword.hscrypto}} adds support for the Management Utilities
{: #added-management-utilities-202004}

{{site.data.keyword.hscrypto}} now supports loading master key parts and signature keys from smart cards for service instance initialization. It ensures the highest level of protection for master key parts and signature keys.

The Management Utilities are two applications that use smart cards to configure service instances. The Smart Card Utility Program sets up and manages the smart cards used. The Trusted Key Entry (TKE) application uses those smart cards to configure service instances. To use the Management Utilities, you need to order IBM-supported smart cards and smart card readers.

For more information, see [Understanding the Management Utilities](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-management-utilities) and [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

### Updated: {{site.data.keyword.cloud_notm}} service integration
{: #added-service-integration-202004}

{{site.data.keyword.hscrypto}} can now be integrated with additional {{site.data.keyword.cloud_notm}} services:

- {{site.data.keyword.ihsdbaas_mongodb_full}}
- {{site.data.keyword.ihsdbaas_postgresql_full}}
- HyTrust DataControl
- {{site.data.keyword.containerlong_notm}}
- {{site.data.keyword.openshiftlong_notm}}

For more information, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

### Added: {{site.data.keyword.hscrypto}} adds support for EP11 private endpoints
{: #added-private-endpoints-202004}

You can now connect to {{site.data.keyword.hscrypto}} over the {{site.data.keyword.cloud_notm}} private network by targeting a private endpoint for the Enterprise PKCS #11 service.

To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. For more information, see [Using private endpoints](/docs/hs-crypto?topic=hs-crypto-secure-connection).

## August 2019
{: #August-2019}

### Added: {{site.data.keyword.hscrypto}} Cloud HSM now supports EP11 cryptographic operations over gRPC
{: #added-EP11}

The managed cloud Hardware Security Module (HSM) supports Enterprise Public-Key Cryptography Standards (PKCS) #11, so your applications can integrate cryptographic operations like digital signing and validation via Enterprise PKCS #11 (EP11) API. The EP11 library provides an interface similar to the industry-standard PKCS #11 API.

{{site.data.keyword.hscrypto}} provides a set of Enterprise PKCS #11 (EP11) over gRPC API calls (also referred to as *GREP11*), with which, all the Crypto functions are executed in HSM on cloud. GREP11 is a stateless interface for cloud programs.

For more information about the GREP11 API, see [Introducing EP11 over gRPC](/docs/hs-crypto?topic=hs-crypto-grep11_intro) and [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).

### Added: {{site.data.keyword.hscrypto}} adds support for private endpoints
{: #added-private-endpoints}

You can now connect to {{site.data.keyword.hscrypto}} over the {{site.data.keyword.cloud_notm}} private network by targeting a private endpoint for the service.

To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. For more information, see [Using private endpoints](/docs/hs-crypto?topic=hs-crypto-secure-connection).

### Added: {{site.data.keyword.hscrypto}} expands into the Frankfurt region
{: #added-frankfurt-region}

You can now create {{site.data.keyword.hscrypto}} resources in the Frankfurt region.

For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

### Added: {{site.data.keyword.cloud_notm}} service integration
{: #added-service-integration}

{{site.data.keyword.hscrypto}} can now be integrated with the following {{site.data.keyword.cloud_notm}} services:

- {{site.data.keyword.cos_full_notm}}
- {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud
- {{site.data.keyword.cloud_notm}} {{site.data.keyword.BluVirtServers_short}} for Virtual Private Cloud
- Key Management Interoperability Protocol (KMIP) for VMware&reg; on {{site.data.keyword.cloud_notm}}

For more information, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

## June 2019
{: #June-2019}

### Added: {{site.data.keyword.hscrypto}} expands into Sydney region
{: #added-sydney-region}

You can now create {{site.data.keyword.hscrypto}} resources in the Sydney region.

For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## March 2019
{: #March-2019}

### {{site.data.keyword.hscrypto}} is generally available
{: #ga-201903}

As of 29 March 2019, provisioning new Hyper Protect Crypto Services Beta instances will no longer be possible. Existing instances will have support until the End of Beta Support Date (30 April 2019).

<!-- See [Migrating keys from a Beta service instance](/docs/hs-crypto/transition-keys.html) for information on migrating keys to a production service instance. -->

For more information about the {{site.data.keyword.hscrypto}} offering, see the [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} home page](https://www.ibm.com/cloud/hyper-protect-crypto){: external}.

### High availability and disaster recovery
{: #ha-dr-new}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, which now supports three availability zones in a selected region, is a highly available service with automatic features that help keep your applications secure and operational.

You can create {{site.data.keyword.hscrypto}} resources in the supported [{{site.data.keyword.cloud_notm}} regions](/docs/hs-crypto?topic=hs-crypto-regions), which represent the geographic area where your {{site.data.keyword.hscrypto}} requests are handled and processed. Each {{site.data.keyword.cloud_notm}} region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.

For more information, see [High availability and disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr).

### Scalability
{: #scalability-new}

The service instance can be scaled out to a maximum of six crypto units to meet your performance requirement. Each crypto unit can crypto-process 5000 keys. In a production environment, it is recommended to select at least two crypto units to enable high availability. By selecting three or more crypto units, these crypto units are distributed among three availability zones in the selected region.

Read [Provisioning the service](/docs/hs-crypto?topic=hs-crypto-provision) for more information.

## February 2019
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} Beta is available
{: #beta-201902}

{{site.data.keyword.hscrypto}} Beta version is released. You can now access the {{site.data.keyword.hscrypto}} service through **Catalog** > **Security** directly.

As of 5 February 2019, provisioning new Hyper Protect Crypto Services Experimental instances will no longer be possible. Existing instances will have support until the End of Experimental Support Date (5 March 2019).

## December 2018
{: #Dec-2018}

### Added: Support for HSM management with Keep Your own Key
{: #hsm-kyok}

{{site.data.keyword.hscrypto}} now supports Keep Your Own Key (KYOK) so that you have more control and authority over your data with encryption keys that you can keep, control, and manage. You can initialize and manage your service instance with {{site.data.keyword.cloud}} command-line interface (CLI).

For more information, see [Initializing service instances to protect key storage](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

### Added: Integration of {{site.data.keyword.keymanagementserviceshort}} API
{: #kp-api}

{{site.data.keyword.keymanagementserviceshort}} API is now integrated with Hyper Protect Crypto Services to generate and protect your keys. You can call the {{site.data.keyword.keymanagementserviceshort}} API directly through {{site.data.keyword.hscrypto}}.

For more information, see [Setting up the key management API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api) and [{{site.data.keyword.hscrypto}} key management API reference](https://{DomainName}/apidocs/hs-crypto){: external}.

### Deprecated: Function of accessing {{site.data.keyword.hscrypto}} through Advanced Cryptography Service Provider
{: #deprecated-acsp}

At the current stage, accessing {{site.data.keyword.hscrypto}} through an Advanced Cryptography Service Provider (ACSP) client is being deprecated. If you are using a previous service instance, you can still use ACSP to explore {{site.data.keyword.hscrypto}}.
