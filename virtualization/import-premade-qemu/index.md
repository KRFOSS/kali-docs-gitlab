---
title: Import Pre-Made Kali QEMU VM
description:
icon:
weight: 219
author: ["Deztryoz",]
---

Importing the [Kali QEMU image](/get-kali/#kali-virtual-machines) with `virt-manager` is very straightforward.

We first need to extract the downloaded QEMU image:

```console
kali@kali:~$ 7z x kali-linux-<VERSION>-qemu-amd64.7z
[...]
kali@kali:~$
```

This will extract the pre-built Kali `.qcow2` disk image.

If `virt-manager` is not already installed, we can install it with:

```console
kali@kali:~$ sudo apt update && sudo apt install virt-manager -y
[...]
```

We then launch `virt-manager` and create a new virtual machine.

From here we select **Import existing disk image**:

![](qemu-import-1.png)

We then select the extracted Kali `.qcow2` disk image:

![](qemu-import-2.png)

If `virt-manager` does not automatically detect the operating system, we disable automatic detection and manually select an appropriate Debian version:

![](qemu-import-3.png)

We can now configure the amount of memory and CPU cores assigned to the virtual machine. In this example, we use 2 GB of memory and 2 CPU cores:

![](qemu-import-4.png)

We can now review the virtual machine configuration, change the VM name if needed, and make any additional changes before finishing the setup:

![](qemu-import-5.png)

Once we are happy with the configuration, we finish creating the virtual machine and start it.

![](qemu-import-6.png)

The pre-built Kali QEMU image should now boot normally. The default login is `kali` for the user and `kali` for the password.
