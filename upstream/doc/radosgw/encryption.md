# Encryption

::: versionadded
Luminous
:::

The Ceph Object Gateway supports server-side encryption of uploaded
objects, with 3 options for the management of encryption keys.
Server-side encryption means that the data is sent over HTTP in its
unencrypted form, and the Ceph Object Gateway stores that data in the
Ceph Storage Cluster in encrypted form.

:::: note
::: title
Note
:::

Requests for server-side encryption must be sent over a secure HTTPS
connection to avoid sending secrets in plaintext. If a proxy is used for
SSL termination, `rgw trust forwarded https` must be enabled before
forwarded requests will be trusted as secure.
::::

:::: note
::: title
Note
:::

Server-side encryption keys must be 256-bit long and base64 encoded.
::::

## Customer-Provided Keys

In this mode, the client passes an encryption key along with each
request to read or write encrypted data. It is the client\'s
responsibility to manage those keys and remember which key was used to
encrypt each object.

This is implemented in S3 according to the [Amazon
SSE-C](https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerSideEncryptionCustomerKeys.html)
specification.

As all key management is handled by the client, no special Ceph
configuration is needed to support this encryption mode.

## Key Management Service

In this mode, an administrator stores keys in a secure key management
service. These keys are then retrieved on demand by the Ceph Object
Gateway to serve requests to encrypt or decrypt data.

This is implemented in S3 according to the [Amazon
SSE-KMS](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html)
specification.

In principle, any key management service could be used here. Currently
integration with [Barbican](https://wiki.openstack.org/wiki/Barbican),
[Vault](https://www.vaultproject.io/docs/), and
[KMIP](http://www.oasis-open.org/committees/kmip/) are implemented.

See [OpenStack Barbican Integration](../barbican), [HashiCorp Vault
Integration](../vault), and [KMIP Integration](../kmip).

## SSE-S3

This makes key management invisible to the user. They are still stored
in Vault, but they are automatically created and deleted by Ceph and
retrieved as required to serve requests to encrypt or decrypt data.

This is implemented in S3 according to the [Amazon
SSE-S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingServerSideEncryption.html)
specification.

In principle, any key management service could be used here. Currently
only integration with [Vault](https://www.vaultproject.io/docs/), is
implemented.

See [HashiCorp Vault Integration](../vault).

## Bucket Encryption APIs

Bucket Encryption APIs to support server-side encryption with Amazon
S3-managed keys (SSE-S3) or AWS KMS customer master keys (SSE-KMS).

See
[PutBucketEncryption](https://docs.aws.amazon.com/AmazonS3/latest/API/API_PutBucketEncryption.html),
[GetBucketEncryption](https://docs.aws.amazon.com/AmazonS3/latest/API/API_GetBucketEncryption.html),
[DeleteBucketEncryption](https://docs.aws.amazon.com/AmazonS3/latest/API/API_DeleteBucketEncryption.html)

## Automatic Encryption (for testing only)

A `rgw crypt default encryption key` can be set in ceph.conf to force
the encryption of all objects that do not otherwise specify an
encryption mode.

The configuration expects a base64-encoded 256 bit key. For example:

    rgw crypt default encryption key = 4YSmvJtBv0aZ7geVgAsdpRnLBEwWSWlMIGnRS8a9TSA=

:::: important
::: title
Important
:::

This mode is for diagnostic purposes only! The ceph configuration file
is not a secure method for storing encryption keys. Keys that are
accidentally exposed in this way should be considered compromised.
::::
