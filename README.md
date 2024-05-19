# ns8-wg-easy

WireGuard Easy is a WireGuard VPN management interface.

## Install

Install via Software Center by adding my repo as explained [here](https://repo.mrmarkuz.com)

Install on CLI:

    add-module ghcr.io/mrmarkuz/wg-easy:latest 1

The output of the command will return the instance name.
Output example:

    {"module_id": "wg-easy1", "image_name": "wg-easy", "image_url": "ghcr.io/mrmarkuz/wg-easy:latest"}

## Configure

Set a FQDN for the web interface, a public FQDN where the clients/peers can reach the WireGuard VPN server and a password for the web UI in the app settings.

## iptables kernel module for RHEL-based distro

RHEL-based distros don't autoload the module iptable_nat anymore so one needs to load it manually on the NS8 host. I'm working on implementing nft in the container to avoid this in future.

Thanks to LayLow for this solution, see also [NethServer Community](https://community.nethserver.org/t/vpn-ui-implementation-on-ns8/23054/33?u=mrmarkuz)

Load the module:

`modprobe iptable_nat`

To autoload it at boot, create `/etc/modules-load.d/iptable_nat.conf` with following content:

```
iptable_nat
```

## Get the configuration
You can retrieve the configuration with

```
api-cli run get-configuration --agent module/wg-easy1
```

## Uninstall

To uninstall the instance:

    remove-module --no-preserve wg-easy1
