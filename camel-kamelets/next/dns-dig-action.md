# ![dns dig action](_images/kamelets/dns-dig-action.svg) DNS DIG Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Asks the DNS for the records of one kind, such as A or MX, of a name, and gives the answer as text, in the format of the `dig` tool.

Use it to see the records of a domain, such as its mail (MX) records, for example to check a DNS change. To get only the IP address of a name, use `dns-ip-action`, and to get its address records as JSON, use `dns-lookup-action`.

Input: the name to look up, taken from the `domain-name` header, else from the `ce-domainname` header, else from the body as text. The kind of record comes from the `dns-type` header, else from the `ce-dnstype` header, else it is `A` (the IPv4 addresses).

Output: the body is the whole answer as text, as the `dig` command shows it: the question, the records found, and the status, such as `NOERROR`.

Good to know: a name the DNS does not know does not fail the message: the answer has the status `NXDOMAIN` and no records. The Kamelet has no options; it asks the DNS servers of the machine it runs on. Headers that start with `CamelDns` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The `dns-dig-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `dns-dig-action` Kamelet relies upon the presence of the following dependencies:

-   camel:dns
    
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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:dns-dig-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-dig-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-dig-action.kamelet.yaml)