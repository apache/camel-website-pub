# Wasm

**Since Camel 4.4**

**Only producer is supported**

[WebAssembly (Wasm)](https://webassembly.org) is a low-level bytecode format designed as a portable target for the compilation of high-level languages like C, C++, and Rust, enabling deployment on the web for client and server applications.

This component provides support to leverage Wasm functions for message transformation.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
    <dependency>
        <groupId>org.apache.camel</groupId>
        <artifactId>camel-wasm</artifactId>
        <version>${camel-version}</version>
    </dependency>
```

## URI format

wasm://functionName?\[options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Wasm component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Wasm endpoint is configured using URI syntax:

wasm:functionName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **functionName** (producer) | **Required** The Function Name. |  | String |

### Query Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **module** (producer) | **Required** Set the module (the distributable, loadable, and executable unit of code in WebAssembly) resource that provides the producer function. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Usage

### Writing A Wasm processor

In _Wasm_, sharing objects between the host, in this case the _JVM_, and the _Wasm_ module is deliberately restricted and as of today, it requires a number of steps:

1.  From the _host_, call a function inside the webassembly module that allocates a block of memory and returns its address, then save it
    
2.  From the _host_, write the data that should be exchanged with the _Wasm_ module to the saved address
    
3.  From the _host_, invoke the required function passing both the address where the data is written and its size
    
4.  From the _Wasm_ module, read the data and process it
    
5.  From the _host_, release the memory when done
    

#### Providing functions for memory management

The module hosting the function **must** provide the functions to allocate/deallocate memory that **must** be named `alloc` and `dealloc` respectively.

Here’s an example of the mentioned functions implemented in [Rust](https://www.rust-lang.org):

```rust
pub extern "C" fn alloc(size: u32) -> *mut u8 {
    let mut buf = Vec::with_capacity(size as usize);
    let ptr = buf.as_mut_ptr();

    // tell Rust not to clean this up
    mem::forget(buf);

    ptr
}

pub unsafe extern "C" fn dealloc(ptr: &mut u8, len: i32) {
    // Retakes the pointer which allows its memory to be freed.
    let _ = Vec::from_raw_parts(ptr, 0, len as usize);
}
```

#### Data shapes

It is not possible to share a Java object with the Wasm module directly, and as mentioned before, data exchange leverages Wasm’s memory that can be accessed by both the host and the guest runtimes. At this stage, the data structure that the component exchange with the Wasm function is a subset of the Apache Camel Message, containing headers the body encoded as a base64 string:

```java
public static class Wrapper {
    @JsonProperty
    public Map<String, String> headers = new HashMap<>();

    @JsonProperty
    public byte[] body;
}
```

#### Data processing

The component expects the processing function to have the following signature:

```rust
fn function(ptr: u32, len: u32) -> u64
```

-   it accepts two 32bit unsigned integers arguments
    
    -   a pointer to the memory location when the input data has been written (`ptr`)
        
    -   the size of the input data (`len`)
        
    
-   it returns a 64bit unsigned integer where:
    
    -   the first 32bit represents a pointer to the return data
        
    -   the last 31bit represents the size of the return data, which must have the same data shape discussed above unless there is an error (see below)
        
    -   the most significant bit of the returned data size is reserved to signal an error, so if it is set, then the return data could contain an error message/code/etc
        
    

Here’s an example of a complete function:

```rust
#[derive(Serialize, Deserialize)]
struct Message {
    headers: HashMap<String, serde_json::Value>,

    #[serde(with = "Base64Standard")]
    body: Vec<u8>,
}

#[cfg_attr(all(target_arch = "wasm32"), export_name = "process")]
#[no_mangle]
pub extern fn process(ptr: u32, len: u32) -> u64 {
    let bytes = unsafe {
        slice::from_raw_parts_mut(
            ptr as *mut u8,
            len as usize)
    };

    let mut msg: Message = serde_json::from_slice(bytes).unwrap();



    let out_vec = serde_json::to_vec(&msg).unwrap();
    let out_len = out_vec.len();
    let out_ptr = alloc(out_len as u32);

    unsafe {
        std::ptr::copy_nonoverlapping(
            out_vec.as_ptr(),
            out_ptr,
            out_len as usize)
    };

    return ((out_ptr as u64) << 32) | out_len as u64;
}
```

## Examples

Supposing we have compiled a Wasm module containing the function above, then it can be called in a Camel Route by its name and module resource location:

```java
 try (CamelContext cc = new DefaultCamelContext()) {
    FluentProducerTemplate pt = cc.createFluentProducerTemplate();

    cc.addRoutes(new RouteBuilder() {
        @Override
        public void configure() throws Exception {
            from("direct:in")
                    .toF("wasm:process?module=classpath://functions.wasm");
        }
    });
    cc.start();

    Exchange out = pt.to("direct:in")
            .withHeader("foo", "bar")
            .withBody("hello")
            .request(Exchange.class);

    assertThat(out.getMessage().getHeaders())
            .containsEntry("foo", "bar");
    assertThat(out.getMessage().getBody(String.class))
            .isEqualTo("HELLO");
}
```

## Spring Boot Auto-Configuration

When using wasm with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-wasm-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.wasm.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.wasm.enabled** | Whether to enable auto configuration of the wasm component. This is enabled by default. |  | Boolean |
| **camel.component.wasm.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.language.wasm.enabled** | Whether to enable auto configuration of the wasm language. This is enabled by default. |  | Boolean |
| **camel.language.wasm.module** | Set the module (the distributable, loadable, and executable unit of code in WebAssembly) resource that provides the expression function. |  | String |
| **camel.language.wasm.trim** | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. | true | Boolean |