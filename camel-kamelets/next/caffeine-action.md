# ![caffeine action](_images/kamelets/caffeine-action.svg) Caffeine Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Stores a value under a key, reads it back, or removes it, in a Caffeine cache kept in the memory of the running application.

Use it to remember something between messages without an outside system, for example the last status seen for each order, or to look up a value that an earlier message stored. To share the values between several applications, or to keep them after a restart, use `redis-sink` or `infinispan-sink` instead.

Input: the operation comes from the `caffeine-operation` header (or `ce-caffeineoperation`): `GET` (the default when no header is set), `PUT`, `INVALIDATE` to remove one key, or `INVALIDATE_ALL` to empty the cache. The key comes from the `caffeine-key` header (or `ce-caffeinekey`), else from the body as text. For `PUT`, the body is the value to store.

Output: for a `GET` of a key that is in the cache, the body is the stored value; for a key that is not, the body is unchanged. The other operations keep the body. The `CamelCaffeineActionHasResult` header is true when a `GET` found the key, and `CamelCaffeineActionSucceeded` tells whether the operation worked.

Good to know: the cache lives only in the memory of the running application. It is empty after a restart, and it is not shared with other applications. All the Kamelets with the same `cacheName` in one application share the same cache.

## Configuration Options

The following table summarizes the configuration options available for the `caffeine-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **cacheName** | Cache Name | **Required** The name of the cache to use. Use the same name in several places of the application to share the values between them, and different names to keep them apart. | string | caffeine-cache | order-status |

## Dependencies

At runtime, the `caffeine-action` Kamelet relies upon the presence of the following dependencies:

-   camel:caffeine
    
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
            uri: "kamelet:caffeine-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/caffeine-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/caffeine-action.kamelet.yaml)