# ![dns lookup action](_images/kamelets/dns-lookup-action.svg) DNS Lookup Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Asks the DNS for the address records of a host name, such as `apache.org`, and gives them as JSON.

Use it to check that a name exists in the DNS, or to see its records and how long they may be cached, for example to monitor a domain. To get the IP address of a name, use `dns-ip-action` instead, and to ask for other kinds of record, such as mail (MX) records, use `dns-dig-action`.

Input: the name to look up, taken from the `domain-name` header, else from the `ce-domainname` header, else from the body as text.

Output: the body is a JSON array with one entry per record found. Each entry has the type, the class and the time to live of the record.

Good to know: a name the DNS does not know fails the message with "host not found". The Kamelet has no options; it asks the DNS servers of the machine it runs on.

## Configuration Options

The `dns-lookup-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `dns-lookup-action` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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
            uri: "kamelet:dns-lookup-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-lookup-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/dns-lookup-action.kamelet.yaml)