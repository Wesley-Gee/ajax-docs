---
title: Security
page_title: Security | RadAsyncUpload for ASP.NET AJAX Documentation
description: Apply security in RadAsyncUpload and enforce information encryption to prevent attacks.
slug: asyncupload-security
tags: security
published: True
position: 14
---

# Security

This article explains how to ensure information about the RadAsyncUpload configuration is secure and non-readable. Its transmission between the client and the server must be encrypted and impossible to decode, so the data cannot be used by a malicious entity in an attack against the server.

Configuration information includes temporary and target folder on the server, and allowed file extensions.

There are two `appSettings` keys you should add to your `web.config` to ensure information security with file uploads:

* set a custom `ConfigurationEncryptionKey`.

* set a custom `ConfigurationHashKey`.

>important If you do not set any custom keys, default (hardcoded) values are used to encrypt/decrypt the information.


## ConfigurationEncryptionKey

To provide secure encryption, we strongly advise that you set a custom encryption key for **Telerik.AsyncUpload.ConfigurationEncryptionKey**:

````web.config
<appSettings>
	<add key="Telerik.AsyncUpload.ConfigurationEncryptionKey" value="abcdefghijklmnopqrstuvwxyz1234567890" />
</appSettings>
````



## ConfigurationHashKey

As of **R1 2017**, the **Encrypt-then-MAC** approach is implemented, in order to improve the integrity of the encrypted temporary and target folders.

The additional **Telerik.Upload.ConfigurationHashKey** key is used to hash the encrypted text. The value returned from the client is checked in the upload handler for integrity. If the hashing attempt is incorrect, a `new CryptographicException("The hash is not valid!");` exception will be thrown.

````web.config
<appSettings>
	<add key="Telerik.Upload.ConfigurationHashKey" value="0987654321zyxwvutsrqponmlkjihgfedcba" />
</appSettings>
````

