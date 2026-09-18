# Support for Apache Karaf

Apache Camel Karaf is for running Camel in the [Apache Karaf](http://karaf.apache.org) OSGi container.

It includes:

-   Camel features repository allowing to install Camel in Karaf.
    
-   Camel Karaf commands allowing you to view, start, stop, get info, about the Camel contexts and routes running in the Karaf instance.
    

NB: Camel Karaf 4.x needs at least Apache Karaf 4.4.6 to run.

## Install Camel in Karaf

Assuming that you have a running Karaf instance, you can register the Camel features repository:

```sh
karaf@root> feature:repo-add camel 4.5.0
```

where 4.5.0 is the Camel version

Now, we have all Camel features available:

To install Camel, just install the `camel` feature:

```sh
karaf@root> feature:install camel
```

You have to install the Camel features depending of your requirements.

If, in your route, you use an endpoint like `stream:out`, you have to install the `camel-stream` feature:

```sh
karaf@root> feature:install camel-stream
```

And so on, for example if you use the sql, and http components:

```sh
karaf@root> feature:install camel-sql camel-http
```

## Camel Karaf commands

When you install the camel feature, new Camel Karaf commands become available automatically.

For example to list all running Camel contexts:

```sh
karaf@root> camel:context-list
```

You can see all the Camel commands by typing `camel:` and then pressing TAB key.

> **Tip**
> use kbd:\[TAB\] key for completion on the Camel context name.