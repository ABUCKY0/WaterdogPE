# Bedrock Dedicated Server (BDS) Compatibility

WaterdogPE now supports connecting to Bedrock Dedicated Server (BDS) by disabling network settings negotiation.

## Problem

By default, WaterdogPE sends a `RequestNetworkSettingsPacket` to downstream servers when using protocol version 1.19.30 and above. However, Bedrock Dedicated Server (BDS) doesn't properly handle this packet, causing connection failures.

## Solution

You can now disable network settings negotiation for specific servers by adding `use_network_settings: false` to your server configuration.

## Configuration Example

```yaml
servers:
  bds-server:
    address: 127.0.0.1:19133
    server_type: bedrock
    use_network_settings: false
  
  regular-server:
    address: 127.0.0.1:19134
    server_type: bedrock
    # use_network_settings defaults to true, so this works with regular Bedrock servers
```

## Backward Compatibility

- The `use_network_settings` field defaults to `true` if not specified
- Existing configurations will continue to work without changes
- Only servers that explicitly set `use_network_settings: false` will skip network settings negotiation

## When to Use

Set `use_network_settings: false` for:
- Bedrock Dedicated Server (BDS)
- Any downstream server that doesn't properly handle `RequestNetworkSettingsPacket`
- Custom server implementations that don't support network settings negotiation

Leave the default (`true`) for:
- Regular Minecraft Bedrock Edition servers
- PocketMine-MP servers
- Nukkit servers
- Any server that properly implements the network settings protocol