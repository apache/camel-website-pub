# ![snmp source](_images/kamelets/snmp-source.svg) SNMP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Reads values, such as uptime or interface counters, from a network device over SNMP at a regular interval, or receives the SNMP traps that devices send, one message per reading or trap.

Use it to monitor routers, switches, printers or servers that speak SNMP, for example to store their counters over time, or to forward their alarms (traps) to a ticketing or chat system.

Output: the body is XML text with one `entry` per value, each with its `oid` (the identifier of the value, such as `1.3.6.1.2.1.1.3.0` for the uptime) and its `value`, inside an `snmp` element. For a trap, the `peerAddress` header is the address of the device that sent it.

Good to know: with `type` set to `TRAP`, `host` and `port` are the address to listen on, not a device; traps are usually sent to port 162, but `port` is 161 by default, and a port below 1024 needs administrator rights on most systems. A device that does not answer a poll gives no message. SNMP v1 and v2c send the community string in clear text; prefer v3 when the device supports it.

## Configuration Options

The following table summarizes the configuration options available for the `snmp-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **host** | Host | **Required** The host name or IP address of the device to poll. With `type` set to `TRAP`, the local address to listen on for traps, such as `0.0.0.0` for all addresses. | string |  | 192.168.1.1 |
| **authenticationPassphrase** | Authentication Passphrase | The SNMP v3 password of the user, as set on the device. Used with `securityLevel` 2 or 3. | string |  |  |
| **authenticationProtocol** | Authentication Protocol | The SNMP v3 hash used to check the login, as set for the user on the device. Used with `securityLevel` 2 or 3. Enum values: \* MD5 \* SHA1 | string |  |  |
| **delay** | Delay | How long to wait between two polls, in milliseconds. For example, 60000 is one minute. Not used for `TRAP`. | integer | 60000 |  |
| **oids** | OIDs | The identifiers (OIDs) of the values to read, separated by commas. Required for `POLL` and `GET_NEXT`, not used for `TRAP`. | string |  | 1.3.6.1.2.1.1.3.0,1.3.6.1.2.1.25.3.2.1.5.1 |
| **port** | Port | The UDP or TCP port of the device to poll, usually 161. With `type` set to `TRAP`, the port to listen on, usually 162. | integer | 161 |  |
| **privacyPassphrase** | Privacy Passphrase | The SNMP v3 encryption password of the user, as set on the device. Used with `securityLevel` 3. | string |  |  |
| **privacyProtocol** | Privacy Protocol | The SNMP v3 encryption, such as `DES` or `AES128`, as set for the user on the device. Used with `securityLevel` 3. | string |  | AES128 |
| **protocol** | Protocol | The network protocol to use. Most devices use `udp`. Enum values: \* udp \* tcp | string | udp |  |
| **securityLevel** | Security Level | The SNMP v3 security level. 1 is no login and no encryption (noAuthNoPriv), 2 is login without encryption (authNoPriv), and 3 is login with encryption (authPriv). Only used with `snmpVersion` 3. Enum values: \* 1 \* 2 \* 3 | integer | 3 |  |
| **securityName** | Security Name | The SNMP v3 user name, as set on the device. Only used with `snmpVersion` 3. | string |  |  |
| **snmpCommunity** | SNMP Community | The community string of SNMP v1 and v2c, which works as a password and is set on the device. It is sent in clear text, so treat it as a secret. | string | public |  |
| **snmpVersion** | SNMP Version | The version of SNMP to use. 0 is v1, 1 is v2c and 3 is v3. It must match the version the device or the trap sender uses. Enum values: \* 0 \* 1 \* 3 | integer | 0 |  |
| **treeList** | Tree List | If true, the values found by `GET_NEXT` are returned as one list. Only used with `GET_NEXT`. | boolean | false |  |
| **type** | Type | What to do. `POLL` reads the values of the OIDs in `oids` every `delay`; `GET_NEXT` reads the values that come after them, to walk a part of the tree of the device; `TRAP` listens for traps sent by devices. Enum values: \* POLL \* GET\_NEXT \* TRAP | string | POLL |  |

## Dependencies

At runtime, the `snmp-source` Kamelet relies upon the presence of the following dependencies:

-   camel:snmp
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:snmp-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## SNMP Source Kamelet Description

### Modes

Set `type` to `POLL` or `GET_NEXT` to query the OIDs listed in the `oids` property on a schedule, or to `TRAP` to listen for traps sent to this host and port.

Polling normally uses port 161 and trap listening normally uses port 162.

### Security

SNMP v1 and v2c authenticate with a community string that is sent in clear text, so the `snmpCommunity` value should be treated as a credential even though it is not encrypted on the wire.

Prefer `snmpVersion` 3 where the device supports it. `securityLevel` defaults to 3 (authPriv), which gives both authentication and privacy.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/snmp-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/snmp-source.kamelet.yaml)