---
title: Apt Complaining about Kali's expired key
description:
icon:
date: 2025-07-15
weight:
author: ["serval123",]
keywords: ["",]
og_description:
---

## The Issue

A GPG key is used to sign the repository to ensure Authenticity, integrity and trust while updating the packages.Every 2-3 years, the Kali team either extends the lifetime of the GPG key used to sign the APT repository or replaces it with a new key. This can cause errors for users who haven't updated their kali-archive-keyring package in a long time. The error will look like this:

```console
kali@kali:~$ sudo apt update
[sudo] password for kali:
Get:1 https://http.kali.org/kali kali-rolling InRelease [41.5 kB]
Err:1 https://http.kali.org/kali kali-rolling InRelease
  Sub-process /usr/bin/sqv returned an error code (1), error message is: Missing key 827C8569F2518CC677FECA1AED65462EC8D5E4C5, which is needed to verify signature.
Fetched 41.5 kB in 3s (16.5 kB/s)
82 packages can be upgraded. Run 'apt list --upgradable' to see them.
Warning: An error occurred during the signature verification. The repository is not updated and the previous index files will be used. OpenPGP signature verification failed: https://http.kali.org/kali kali-rolling InRelease: Sub-process /usr/bin/sqv returned an error code (1), error message is: Missing key 827C8569F2518CC677FECA1AED65462EC8D5E4C5, which is needed to verify signature.
Warning: Failed to fetch https://http.kali.org/kali/dists/kali-rolling/InRelease  Sub-process /usr/bin/sqv returned an error code (1), error message is: Missing key 827C8569F2518CC677FECA1AED65462EC8D5E4C5, which is needed to verify signature.
Warning: Some index files failed to download. They have been ignored, or old ones used instead.

```

The easiest way to resolve this issue is to retrieve the latest key and store it in a place where apt will find it.

```console
kali@kali:~$ sudo wget https://archive.kali.org/archive-keyring.gpg -O /usr/share/keyrings/kali-archive-keyring.gpg

```
To avoid this issue in the future, update your system regularly.
Also note that if your kali's version is more than 2 years old, you may not be able to receive further updates unless you switch to the latest version.



