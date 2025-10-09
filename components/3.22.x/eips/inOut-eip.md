# In Out

> **Warning**
> **Deprecated:** This inOut is deprecated and may be removed in a future release.

The **inOut:** EIP define an InOut ExchangePattern.

> **Warning**
> inOut is deprecated. Use [setExchangePattern](event-message.md) instead.

## EIP options

The In Out eip supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **uri** | **Required** Sets the uri of the endpoint to send to. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **description** | Sets the description of this node. |  | DescriptionDefinition |