# ![snmp source](_images/kamelets/snmp-source.svg) SNMP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Poll SNMP (Simple Network Management Protocol) capable devices, or receive SNMP traps.

Set type to POLL or GET\_NEXT to query the OIDs listed in the oids property on a schedule, or to TRAP to listen for traps sent to this host and port.

SNMP v1 and v2c authenticate with a plaintext community string. Prefer snmpVersion 3 with authentication and privacy where the device supports it.

## Configuration Options

The following table summarizes the configuration options available for the `snmp-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **host** | Host | **Required** The hostname of the SNMP device to poll, or the address to listen on when receiving traps. | string |  | 192.168.1.1 |
| **authenticationPassphrase** | Authentication Passphrase | The SNMP v3 authentication passphrase. | string |  |  |
| **authenticationProtocol** | Authentication Protocol | The SNMP v3 authentication protocol. Enum values: \* MD5 \* SHA1 | string |  |  |
| **delay** | Delay | The delay in milliseconds between each poll. Unused for TRAP. | integer | 60000 |  |
| **oids** | OIDs | A comma separated list of OIDs to query. Required for POLL and GET\_NEXT, unused for TRAP. | string |  | 1.3.6.1.2.1.1.3.0,1.3.6.1.2.1.25.3.2.1.5.1 |
| **port** | Port | The port of the SNMP device. Polling normally uses 161 and trap listening normally uses 162. | integer | 161 |  |
| **privacyPassphrase** | Privacy Passphrase | The SNMP v3 privacy (encryption) passphrase. | string |  |  |
| **privacyProtocol** | Privacy Protocol | The SNMP v3 privacy (encryption) protocol, for example DES or AES128. | string |  |  |
| **protocol** | Protocol | The transport protocol to use. Enum values: \* udp \* tcp | string | udp |  |
| **securityLevel** | Security Level | The SNMP v3 security level. 1 is noAuthNoPriv, 2 is authNoPriv and 3 is authPriv. Enum values: \* 1 \* 2 \* 3 | integer | 3 |  |
| **securityName** | Security Name | The SNMP v3 security name (username). | string |  |  |
| **snmpCommunity** | SNMP Community | The community string used by SNMP v1 and v2c. This is a shared secret sent in clear text, so treat it as a credential. | string | public |  |
| **snmpVersion** | SNMP Version | The SNMP protocol version to use. 0 is v1, 1 is v2c and 3 is v3. Enum values: \* 0 \* 1 \* 3 | integer | 0 |  |
| **treeList** | Tree List | Whether to walk the OID tree and return the result as a list of variable bindings. Only used with GET\_NEXT. | boolean | false |  |
| **type** | Type | Whether to poll the device (POLL), walk the OID tree (GET\_NEXT), or listen for incoming traps (TRAP). Enum values: \* POLL \* GET\_NEXT \* TRAP | string | POLL |  |

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/snmp-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/snmp-source.kamelet.yaml)