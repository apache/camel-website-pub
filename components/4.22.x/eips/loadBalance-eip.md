# Load Balance

The Load Balancer Pattern allows you to delegate to one of a number of endpoints using a variety of different load balancing policies.

## Built-in load balancing policies

Camel provides the following policies out-of-the-box:

 
| Policy | Description |
| --- | --- |
| [Custom Load Balancer](customLoadBalancer-eip.md) | To use a custom load balancer implementation. |
| [Fail-over Load Balancer](failoverLoadBalancer-eip.md) | In case of failures, the exchange will be tried on the next endpoint. |
| [Round Robin Load Balancer](roundRobinLoadBalancer-eip.md) | The destination endpoints are selected in a round-robin fashion. This is a well-known and classic policy, which spreads the load evenly. |
| [Random Load Balancer](randomLoadBalancer-eip.md) | The destination endpoints are selected randomly. |
| [Sticky Load Balancer](stickyLoadBalancer-eip.md) | Sticky load balancing using an [Expression](../../../manual/expression.md) to calculate a correlation key to perform the sticky load balancing. |
| [Topic Load Balancer](topicLoadBalancer-eip.md) | Topic which sends to all destinations. |
| [Weighted Loader Balancer](weightedLoadBalancer-eip.md) | Use a weighted load distribution ratio for each server with respect to others. |