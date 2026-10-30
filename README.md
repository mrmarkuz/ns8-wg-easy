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

Set a FQDN for the web interface, browse to it and go through the setup wizard.
Add a client to get a config or scan a QR code.

## Migrate from wg-easy 14, ns8-wg-easy 1.0.1

- To migrate the configuration, backup the configuration in the old wg-easy UI.
- After the NS8 update to ns8-wg-easy > 1.0.1, wg-easy doesn't start because of an old config file.

If you missed to export the configuration, you can go back to 1.0.1 by executing

    update-module --force ghcr.io/mrmarkuz/wg-easy:1.0.1

To make wg-easy 15 start after the update from wg-easy 14: (ns8-wg-easy 1.0.1)

    runagent -m wg-easy1
    systemctl --user stop wg-easy
    podman rm -a
    podman volume rm -a
    systemctl --user start wg-easy
    
After wg-easy has started, go through the setup wizard, choose "Yes" when it asks "Do you have an existing setup?"
and import the backup from the first step.

See also https://wg-easy.github.io/wg-easy/v15.5/advanced/migrate/from-14-to-15/

## Get the configuration
You can retrieve the configuration with

```
api-cli run get-configuration --agent module/wg-easy1
```

## Uninstall

To uninstall the instance:

    remove-module --no-preserve wg-easy1
