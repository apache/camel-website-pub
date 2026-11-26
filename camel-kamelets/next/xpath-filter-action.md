# ![xpath filter action](_images/kamelets/xpath-filter-action.svg) XPath Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Keeps only the XML messages that match an XPath expression, and drops all others.

Use it to pass on only the XML documents you care about, for example only the orders above a certain amount with `/order[amount > 100]`, or only the paid invoices of an XML feed. For JSON, use `predicate-filter-action`; to keep or drop messages by a header, use `header-matches-filter-action`; to check XML against an XML Schema, use `xml-schema-validator-action`.

Input: XML as text, bytes or a stream.

Output: the same message, unchanged, when the expression matches: text stays text, bytes stay bytes, a stream can still be read, and the headers are kept. When it does not match, the message is dropped and nothing is sent on.

Good to know: the expression matches when it selects at least one element, such as `/order[amount > 100]`, or when it is a condition that is true, such as `/order/customer = 'Ann'`. A message without a body is dropped. A body that is not XML fails with an error such as `Content is not allowed in prolog.`; it is not dropped silently, so the error handling of the integration decides what happens to it. A message with a DOCTYPE fails too, so its entities are never expanded and an entity that points to a file or URL is never read. An element in a namespace is matched with a prefix: declare one with `namespacePrefix` and `namespaceUri`, or several at once with `namespaces`, such as `o=urn:example:orders,c=urn:example:customers` for `/o:order[c:customer/c:name = 'Ann']`. The expression is set by you; it cannot come from the message.

## Configuration Options

The following table summarizes the configuration options available for the `xpath-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **expression** | Expression | **Required** The XPath 1.0 expression a message must match to be kept. For example, `/order[amount > 100]` keeps the orders whose `amount` element is more than 100, and `/order/customer = 'Ann'` those of the customer Ann. | string |  | /order\[amount > 100\] |
| **namespacePrefix** | Namespace Prefix | A prefix to use in the expression for the namespace given by `namespaceUri`. For example, with the prefix `o` and the namespace `urn:example:orders`, `/o:order[o:status = 'paid']` keeps the paid orders of `<order xmlns="urn:example:orders">`. An element in a namespace is not matched by a name without a prefix. | string |  | o |
| **namespaceUri** | Namespace URI | The namespace that `namespacePrefix` stands for, as written in the `xmlns` attribute of the XML. | string |  | urn:example:orders |
| **namespaces** | Namespaces | Several namespaces to use in the expression, each as `prefix=uri`, separated by commas. For example, `o=urn:example:orders,c=urn:example:customers` lets `/o:order[c:customer/c:name = 'Ann']` match an order whose customer is in another namespace. A prefix that is also set by `namespacePrefix` takes the URI of `namespaceUri`. A value without `=` fails the integration when it starts. | string |  | o=urn:example:orders,c=urn:example:customers |

## Dependencies

At runtime, the `xpath-filter-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:xpath
    

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
            uri: "kamelet:xpath-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/xpath-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/xpath-filter-action.kamelet.yaml)