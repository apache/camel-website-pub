# ![dns ip action](_images/kamelets/dns-ip-action.svg) DNS IP Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Finds the IP address of a host name, such as `apache.org`, and gives it as text.

Use it to turn a host name into an address for a later step, or to check that a name can be resolved. To see all the address records of a name with how long they may be cached, use `dns-lookup-action`, and to ask for other kinds of record, such as mail (MX) records, use `dns-dig-action`.

Input: the name to look up, taken from the `domain` header, else from the `ce-domain` header, else from the body as text.

Output: the body is one IP address, as text, such as `151.101.2.132`.

Good to know: when a name has several addresses, only one of them is given. A name the DNS does not know fails the message with an unknown host error. The headers are `domain` and `ce-domain`, not `domain-name` as for `dns-lookup-action` and `dns-dig-action`. The Kamelet has no options; it uses the name resolution of the machine it runs on. Headers that start with `CamelDns` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The `dns-ip-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `dns-ip-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:dns-ip-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-ip-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-ip-action.kamelet.yaml)