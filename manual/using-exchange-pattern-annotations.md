# Using Exchange Pattern Annotations

Invoking InOut methods for [request/reply](../components/4.22.x/eips/requestReply-eip.md) when working with [POJO Producing](pojo-producing.md) is typically synchronous. As such, the caller will block until the server returns a result.

InOut means that there is an In message for the input and an Out for the output/result.

> **Note**
> Other books, posts and reference guides may use the terms In/Out and In/Only for the patterns. In this guide we use InOut and InOnly respectively, as these are the names used within Camel.

You can also implement support for [Event Messages](../components/4.22.x/eips/event-message.md) with Apache Camel, using the InOnly [pattern](exchange-pattern.md). These are often called "fire and forget" (i.e., like sending a JMS message but not waiting for any response).

## Specifying InOnly and InOut methods

Typically, the InOut pattern is what most users want, but you can customize to use InOnly using an annotation. For instance:

```java
public interface Foo {

  Object someInOutMethod(String input);
  String anotherInOutMethod(Cheese input);

  @InOnly
  void someInOnlyMethod(Document input);
}
```

The above code shows three methods on an interface:

-   the first two use the default InOut mechanism
    
-   the third one, `someInOnlyMethod` uses the `@InOnly` annotation to specify it as being a one-way method call.
    

## Class level annotations

You can also use class level annotations to default all methods in an interface to a pattern:

```java
@InOnly
public interface Foo {
  void someInOnlyMethod(Document input);
  void anotherInOnlyMethod(String input);
}
```

Apache Camel will detect annotations on base classes or interfaces. For instance, suppose you created a client side proxy for the following code:

```java
public class MyFoo implements Foo {
  ...
}
```

In this case, the methods inherited from Foo would all be `@InOnly`.

### Overloading a class level annotation

You can overload a class level annotation on specific methods. Suppose you have a class or interface with many `@InOnly` methods, but you want to annotate just one or two methods as `@InOut`. You can do it like this:

```java
@InOnly
public interface Foo {
  void someInOnlyMethod(Document input);
  void anotherInOnlyMethod(String input);

  @InOut
  String someInOutMethod(String input);
}
```

In the above `Foo` interface only the `someInOutMethod` will be `@InOut`, and all the others will be `@InOnly`.

## Using your own annotations for exchange patterns

You might want to create your own annotations to represent a group of different bits of metadata; such as combining synchrony, concurrency and transaction behavior.

In this case you can annotate your annotation with the `@Pattern` annotation to the default exchange pattern you wish to use.

For example, lets say we want to create our own annotation called `@MyAsyncService`:

```java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE, ElementType.METHOD})
// specify the message pattern
@Pattern(ExchangePattern.InOnly)
public @interface MyAsyncService {
}
```

Now we can use this annotation, and Camel will figure out the correct exchange pattern.

```java
public interface Foo {
  void someInOnlyMethod(Document input);
  void anotherInOnlyMethod(String input);

  @MyAsyncService
  String someInOutMethod(String input);
}
```