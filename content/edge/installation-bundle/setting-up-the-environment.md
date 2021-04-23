---
weight: 20
title: Setting up the environment
layout: redirect
---

For your convenience, we provide the hypervisor examples for setting up Cumulocity IoT Edge:

* [Example setup for ESXi VMWare](/edge/installation#setting-up-esxi)
* [Example setup for VMWare Workstation Player](/edge/installation#setting-up-vmware)
* [Example setup for Hyper-V](/edge/installation#setting-up-hyper-v)
* [Example setup for VirtualBox](/edge/installation#setting-up-virtual-box)

For all hypervisors, we recommend you to use UTC on your host machines.

>**Info:** VirtualBox support is deprecated, so it is not recommended to use it in a production environment.

### VM login details

SSH login into Cumulocity IoT Edge is allowed through the “admin” user. All operational activities described in this guide need to be carried out through the admin user.

Use the following login credentials for SSH login into the Edge instance:

* Username: admin
* Password: manage

>**Important:** Changing the hostname of the Edge VM is not supported.


In the Edge VM, the default keyboard layout is **en_US**. If your keyboard is other than **en_US**, the characters that you type might not match the keys on the keyboard. This might affect your Edge VM password when setting the password or logging in to Edge VM directly through the VM console.

Use the following command to log into Edge server via SSH:

```shell
ssh admin@<IP address>

$ Password: manage
```

Use the IP address provided during [network configuration](/edge/installation#configuration).

|Hypervisor|Default IP Address|
|:---|:---|
|Virtual Box|192.168.56.120
|Hyper-V|192.168.66.10

>**Info:**
Root access is not supported in the Edge VM instance. Changes made as root user might cause failure of the described operational procedures.
Moreover, the Edge VM is tested and validated with the configuration shipped (i.e. OS version/patch level, other components compatibility etc). Root access would alter Cumulocity IoT Edge to an unknown and not tested configuration and handling support tickets would no longer work.