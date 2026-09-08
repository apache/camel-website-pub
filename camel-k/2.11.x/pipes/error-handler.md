# Pipes Error Handler

Pipes offer a mechanism to specify an error policy to adopt in case an event produced by a `source` or consumed by a `sink`. Through the definition of an `errorHandler` you will be able to apply certain logic to the failing event, such as simply logging, ignoring the event or posting the event to another `Sink`.

my-binding.yaml

```yaml
apiVersion: camel.apache.org/v1
kind: Pipe
metadata:
  name: my-binding
spec:
  source: (1)
...
  sink: (2)
...
  errorHandler: (3)
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Reference to the source that provides data</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Reference to the sink where data should be sent to</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>Error Handler Configuration</td></tr></tbody></table>

## Error Handler Types

We have different types of error handler: `none`, `log` and `sink`. The `errorHandler` parameter is optional.

### No error handler

There may be certain cases where you want to just ignore any failure happening on your integration. In this situation just use a `none` error handler.

my-binding.yaml

```yaml
apiVersion: camel.apache.org/v1
kind: Pipe
metadata:
  name: my-binding
spec:
  source:
...
  sink:
...
  errorHandler:
    none: (1)
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td><code>none</code> error handler does not expect any configuration</td></tr></tbody></table>

### Log error handler

Apache Camel offers a default behavior for handling any failure: log to standard output. However you can use the `log` error handler to specify other behaviors such as redelivery or delay policy.

my-binding.yaml

```yaml
apiVersion: camel.apache.org/v1
kind: Pipe
metadata:
  name: my-binding
spec:
  source:
...
  sink:
...
  errorHandler:
    log:
      parameters: (1)
        maximumRedeliveries: 3
        redeliveryDelay: 2000
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Parameters belonging to the <code>log</code> error handler type</td></tr></tbody></table>

### Sink error handler

The `Sink` is probably the most interesting error handler type as it allows you to redirect any failing event to any other component, such as a third party URI, a queue or even another `Kamelet` which will be performing certain logic with the failing event.

my-binding.yaml

```yaml
apiVersion: camel.apache.org/v1
kind: Pipe
metadata:
  name: my-binding
spec:
  source:
...
  sink:
...
  errorHandler:
    sink:
      endpoint:
        ref: (1)
          kind: Kamelet
          apiVersion: camel.apache.org/v1
          name: error-handler
        properties:
          message: "ERROR!" (2)
          ...
      parameters:
        maximumRedeliveries: 1 (3)
        ...
```

<table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>You can use <code>ref</code> or <code>uri</code>. <code>ref</code> will be interpreted by the operator according the <code>kind</code>, <code>apiVersion</code> and <code>name</code>. You can use any <code>Kamelet</code>, <code>KafkaTopic</code> channel or <code>Knative</code> destination.</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Properties belonging to the endpoint (in this example, to the <code>Kamelet</code> named error handler)</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>Parameters belonging to the <code>sink</code> error handler type</td></tr></tbody></table>