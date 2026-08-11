# BrowsableEndpoint

The `BrowseableEndpoint` is an extension interface an `Endpoint` may implement to support the browsing of the Message [Exchanges](exchange.md) which are pending or have been sent on it.

Some implementations include:

-   [JMS](../components/4.22.x/jms-component.md) for queues only
    
-   [Mock](../components/4.22.x/mock-component.md)
    
-   [SEDA](../components/4.22.x/seda-component.md)