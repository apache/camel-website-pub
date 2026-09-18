# Stripe

**Since Camel 4.17**

**Only producer is supported**

The Stripe component provides integration with the [Stripe](https://stripe.com/) payment platform API using Stripe Java SDK.

Stripe is a popular payment processing platform that allows businesses to accept payments, send payouts, and manage their online businesses. This component enables Apache Camel routes to interact with Stripe’s API for operations such as:

-   Creating and managing customers
    
-   Processing payments and payment intents
    
-   Managing products and prices
    
-   Handling subscriptions
    
-   Creating and managing invoices
    
-   Processing refunds
    
-   And more
    

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-stripe</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

stripe:operation\[?options\]

Where `operation` is one of the following:

-   `charges` - Create, retrieve, update, list, and capture charges
    
-   `customers` - Create, retrieve, update, delete, and list customers
    
-   `paymentIntents` - Create, retrieve, update, cancel, and list payment intents
    
-   `paymentMethods` - Create, retrieve, update, and list payment methods
    
-   `refunds` - Create, retrieve, update, and list refunds
    
-   `subscriptions` - Create, retrieve, update, cancel, and list subscriptions
    
-   `invoices` - Create, retrieve, update, and list invoices
    
-   `products` - Create, retrieve, update, delete, and list products
    
-   `prices` - Create, retrieve, update, and list prices
    
-   `balanceTransactions` - Retrieve and list balance transactions
    

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. You can set them directly via Java code, or through the properties component.

```java
StripeComponent stripe = context.getComponent("stripe", StripeComponent.class);
stripe.setApiKey("sk_test_...");
```

### Configuring Endpoint Options

You usually use the endpoint for configuring the API operation and parameters specific to each call.

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

The Stripe component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiBase** (advanced) | Override the default Stripe API base URL (for testing purposes). |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **apiKey** (security) | The Stripe API key for authentication. |  | String |

## Endpoint Options

The Stripe endpoint is configured using URI syntax:

stripe:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The Stripe operation to perform.

Enum values:

-   charges
    
-   customers
    
-   paymentIntents
    
-   paymentMethods
    
-   refunds
    
-   subscriptions
    
-   invoices
    
-   products
    
-   prices
    
-   balanceTransactions
    





 |  | StripeOperation |

### Query Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiBase** (advanced) | Override the default Stripe API base URL (for testing purposes). |  | String |
| **apiKey** (security) | The Stripe API key for authentication. |  | String |

## Message Headers

The Stripe component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelStripeOperation** (producer) Constant: [`OPERATION_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-stripe/latest/org/apache/camel/component/stripe/StripeConstants.html#OPERATION_HEADER) | The operation to perform. |  | String |
| **CamelStripeMethod** (producer) Constant: [`METHOD_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-stripe/latest/org/apache/camel/component/stripe/StripeConstants.html#METHOD_HEADER) | The method to invoke (create, retrieve, update, delete, list, cancel, capture). |  | String |
| **CamelStripeObjectId** (producer) Constant: [`OBJECT_ID`](https://javadoc.io/doc/org.apache.camel/camel-stripe/latest/org/apache/camel/component/stripe/StripeConstants.html#OBJECT_ID) | The ID of the object to retrieve, update, or delete. |  | String |

## Authentication

The Stripe component requires a Stripe API key for authentication. You can obtain your API keys from the Stripe Dashboard.

### Getting Your Stripe API Key

#### Step 1: Create a Stripe Account

1.  Go to [Stripe’s website](https://stripe.com/)
    
2.  Click "Sign up" or "Start now"
    
3.  Fill in your email, password, and country
    
4.  Verify your email address by clicking the link sent to your email
    
5.  Complete your account setup by providing business information
    

#### Step 2: Access the Stripe Dashboard

1.  Log in to your Stripe account at [dashboard.stripe.com](https://dashboard.stripe.com/)
    
2.  You will land on the Stripe Dashboard home page
    

#### Step 3: Get Your API Keys

1.  In the Stripe Dashboard, click on the "Developers" link in the left sidebar
    
2.  Click on "API keys" in the submenu
    
3.  You will see two types of keys:
    
    -   **Publishable key**: Used in client-side code (not needed for this component)
        
    -   **Secret key**: Used for server-side API calls (this is what you need)
        
    
4.  For testing, use the **Test mode** keys (toggle is at the top right)
    
    -   Test keys start with `sk_test_…​`
        
    -   Test mode allows you to make API calls without processing real payments
        
    
5.  For production, switch to **Live mode** (requires account verification)
    
    -   Live keys start with `sk_live_…​`
        
    -   **WARNING**: Never use live keys for testing or development!
        
    
6.  Click "Reveal test key" to view your secret API key
    
7.  Copy the key starting with `sk_test_…​`
    

#### Important Security Notes

-   **Never commit API keys to version control** (Git, SVN, etc.)
    
-   **Never expose API keys in client-side code**
    
-   **Use environment variables or secure configuration management** for production
    
-   **Always use test keys for development and testing**
    
-   **Rotate your API keys regularly** for security
    
-   **Use restricted API keys** in production for least privilege access
    

### Configuring Authentication in Camel

You can configure the API key in several ways:

#### Option 1: Component Level (Recommended for Single Key)

```java
StripeComponent stripe = context.getComponent("stripe", StripeComponent.class);
stripe.setApiKey("sk_test_...");
```

#### Option 2: Endpoint Level with Property Placeholder

```java
from("direct:start")
    .to("stripe:customers?apiKey={{stripe.apiKey}}");
```

Then in `application.properties`:

stripe.apiKey=sk\_test\_...

#### Option 3: System Property (Recommended for Production)

```java
from("direct:start")
    .to("stripe:customers?apiKey={{STRIPE_API_KEY}}");
```

Set via system property:

mvn camel:run -DSTRIPE\_API\_KEY=sk\_test\_...

## Usage Examples

The Stripe component accepts both Map objects and JSON strings as input, providing flexibility for different integration scenarios.

### Creating a Customer

Using a Map:

```java
from("direct:createCustomer")
    .setBody(constant(Map.of(
        "email", "customer@example.com",
        "name", "John Doe",
        "description", "New customer"
    )))
    .to("stripe:customers?apiKey={{stripe.apiKey}}")
    .log("Created customer: ${body.id}");
```

Using JSON:

```java
from("direct:createCustomerJson")
    .setBody(constant("""
        {
            "email": "customer@example.com",
            "name": "John Doe",
            "description": "New customer"
        }
    """))
    .to("stripe:customers?apiKey={{stripe.apiKey}}")
    .log("Created customer: ${body.id}");
```

### Creating a Payment Intent

Using a Map:

```java
from("direct:payment")
    .setBody(constant(Map.of(
        "amount", 2000L,  // Amount in cents ($20.00)
        "currency", "usd",
        "payment_method_types", List.of("card"),
        "description", "Payment for order #12345"
    )))
    .to("stripe:paymentIntents?apiKey={{stripe.apiKey}}")
    .log("Payment intent created: ${body.id}");
```

Using JSON (useful when integrating with REST endpoints):

```java
from("rest:post:/payments")
    .log("Received payment request: ${body}")
    // Body is already JSON from REST endpoint
    .to("stripe:paymentIntents?apiKey={{stripe.apiKey}}")
    .log("Payment intent created: ${body.id}");
```

### Retrieving a Customer

```java
from("direct:getCustomer")
    .setHeader(StripeConstants.OBJECT_ID, constant("cus_xxxxx"))
    .setHeader(StripeConstants.METHOD_HEADER, constant(StripeConstants.METHOD_RETRIEVE))
    .to("stripe:customers?apiKey={{stripe.apiKey}}")
    .log("Retrieved customer: ${body.email}");
```

### Updating a Payment Intent

```java
from("direct:updatePayment")
    .setHeader(StripeConstants.OBJECT_ID, simple("${exchangeProperty.paymentIntentId}"))
    .setHeader(StripeConstants.METHOD_HEADER, constant(StripeConstants.METHOD_UPDATE))
    .setBody(constant(Map.of(
        "description", "Updated description",
        "metadata", Map.of("order_id", "12345")
    )))
    .to("stripe:paymentIntents?apiKey={{stripe.apiKey}}");
```

### Listing Customers

```java
from("direct:listCustomers")
    .setHeader(StripeConstants.METHOD_HEADER, constant(StripeConstants.METHOD_LIST))
    .setBody(constant(Map.of("limit", 10)))
    .to("stripe:customers?apiKey={{stripe.apiKey}}")
    .log("Found ${body.data.size()} customers");
```

### Creating a Product with Price

```java
from("direct:createProduct")
    // Create product
    .setBody(constant(Map.of(
        "name", "Premium Subscription",
        "description", "Monthly premium access"
    )))
    .to("stripe:products?apiKey={{stripe.apiKey}}")
    .setProperty("productId", simple("${body.id}"))
    // Create price for the product
    .process(exchange -> {
        Map<String, Object> priceParams = new HashMap<>();
        priceParams.put("product", exchange.getProperty("productId", String.class));
        priceParams.put("currency", "usd");
        priceParams.put("unit_amount", 2999L);  // $29.99
        priceParams.put("recurring", Map.of("interval", "month"));
        exchange.getMessage().setBody(priceParams);
    })
    .to("stripe:prices?apiKey={{stripe.apiKey}}")
    .log("Created product ${exchangeProperty.productId} with price ${body.id}");
```

### Processing a Refund

```java
from("direct:refund")
    .setBody(constant(Map.of(
        "charge", "ch_xxxxx",
        "amount", 1000L,  // Partial refund of $10.00
        "reason", "requested_by_customer"
    )))
    .to("stripe:refunds?apiKey={{stripe.apiKey}}")
    .log("Refund processed: ${body.id}");
```

### Canceling a Payment Intent

```java
from("direct:cancelPayment")
    .setHeader(StripeConstants.OBJECT_ID, simple("${header.paymentIntentId}"))
    .setHeader(StripeConstants.METHOD_HEADER, constant(StripeConstants.METHOD_CANCEL))
    .to("stripe:paymentIntents?apiKey={{stripe.apiKey}}")
    .log("Payment intent canceled: ${body.id}");
```

## Running Integration Tests

The Stripe component includes comprehensive integration tests that verify functionality against the Stripe API.

### Prerequisites

1.  A Stripe account (free to create)
    
2.  A test API key (obtained from the Stripe Dashboard as described above)
    
3.  Maven 3.x and Java 11 or higher
    

### Running the Tests

Provide the API key via system property:

```bash
mvn verify -Dtest=Stripe*IntegrationTest -DSTRIPE_API_KEY=sk_test_51...
```

#### Running Specific Test Classes

```bash
# Test customer operations
mvn verify -Dtest=StripeCustomerIntegrationTest -DSTRIPE_API_KEY=sk_test_51...

# Test payment intent operations
mvn verify -Dtest=StripePaymentIntentIntegrationTest -DSTRIPE_API_KEY=sk_test_51...

# Test product operations
mvn verify -Dtest=StripeProductIntegrationTest -DSTRIPE_API_KEY=sk_test_51...
```

#### Running All Tests

```bash
mvn verify -DSTRIPE_API_KEY=sk_test_51...
```

### Test Safety

All integration tests:

-   **Only use test mode API keys** (verified by checking `sk_test_` prefix)
    
-   **Create temporary test data** that is cleaned up after each test
    
-   **Never process real payments** or affect production data
    
-   **Can be run unlimited times** without cost
    
-   **Automatically skip** if no API key is provided
    

### Viewing Test Results in Stripe Dashboard

1.  Log in to the Stripe Dashboard
    
2.  Ensure you’re in **Test mode** (toggle at top right)
    
3.  Navigate to the relevant section:
    
    -   Customers: [https://dashboard.stripe.com/test/customers](https://dashboard.stripe.com/test/customers)
        
    -   Payments: [https://dashboard.stripe.com/test/payments](https://dashboard.stripe.com/test/payments)
        
    -   Products: [https://dashboard.stripe.com/test/products](https://dashboard.stripe.com/test/products)
        
    

You can see all the test data created during integration test runs.

## Supported Operations and Methods

### Charges

 
| Method | Description |
| --- | --- |
| `create` | Create a charge for a payment |
| `retrieve` | Retrieve a charge by ID |
| `update` | Update a charge’s metadata |
| `list` | List all charges |
| `capture` | Capture a previously uncaptured charge |

### Customers

 
| Method | Description |
| --- | --- |
| `create` | Create a new customer |
| `retrieve` | Retrieve a customer by ID |
| `update` | Update customer information |
| `delete` | Delete a customer |
| `list` | List all customers |

### Payment Intents

 
| Method | Description |
| --- | --- |
| `create` | Create a payment intent |
| `retrieve` | Retrieve a payment intent by ID |
| `update` | Update payment intent information |
| `cancel` | Cancel a payment intent |
| `list` | List all payment intents |

### Payment Methods

 
| Method | Description |
| --- | --- |
| `create` | Create a payment method |
| `retrieve` | Retrieve a payment method by ID |
| `update` | Update payment method information |
| `list` | List all payment methods |

### Refunds

 
| Method | Description |
| --- | --- |
| `create` | Create a refund |
| `retrieve` | Retrieve a refund by ID |
| `update` | Update refund metadata |
| `list` | List all refunds |

### Subscriptions

 
| Method | Description |
| --- | --- |
| `create` | Create a subscription |
| `retrieve` | Retrieve a subscription by ID |
| `update` | Update subscription information |
| `cancel` | Cancel a subscription |
| `list` | List all subscriptions |

### Invoices

 
| Method | Description |
| --- | --- |
| `create` | Create an invoice |
| `retrieve` | Retrieve an invoice by ID |
| `update` | Update invoice information |
| `list` | List all invoices |

### Products

 
| Method | Description |
| --- | --- |
| `create` | Create a product |
| `retrieve` | Retrieve a product by ID |
| `update` | Update product information |
| `delete` | Delete a product |
| `list` | List all products |

### Prices

 
| Method | Description |
| --- | --- |
| `create` | Create a price |
| `retrieve` | Retrieve a price by ID |
| `update` | Update price metadata |
| `list` | List all prices |

### Balance Transactions

 
| Method | Description |
| --- | --- |
| `retrieve` | Retrieve a balance transaction by ID |
| `list` | List all balance transactions |

## Error Handling

The Stripe API may return various errors. The component propagates these as exceptions:

```java
from("direct:createPayment")
    .doTry()
        .to("stripe:paymentIntents?apiKey={{stripe.apiKey}}")
        .log("Payment successful: ${body.id}")
    .doCatch(com.stripe.exception.CardException.class)
        .log("Card was declined: ${exception.message}")
    .doCatch(com.stripe.exception.InvalidRequestException.class)
        .log("Invalid parameters: ${exception.message}")
    .doCatch(com.stripe.exception.AuthenticationException.class)
        .log("Authentication failed - check API key")
    .doCatch(com.stripe.exception.ApiException.class)
        .log("Stripe API error: ${exception.message}")
    .end();
```

## Additional Resources

-   [Stripe API Documentation](https://stripe.com/docs/api)
    
-   [Stripe Testing Guide](https://stripe.com/docs/testing)
    
-   [API Keys Documentation](https://stripe.com/docs/keys)
    
-   [Stripe Java SDK](https://github.com/stripe/stripe-java)