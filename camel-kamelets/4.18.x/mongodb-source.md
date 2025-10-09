# ![mongodb source](_images/kamelets/mongodb-source.svg) MongoDB Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume data from MongoDB.

## Configuration Options

The following table summarizes the configuration options available for the `mongodb-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **collection** | MongoDB Collection | **Required** The name of the MongoDB collection to bind to this endpoint. | string |  |  |
| **database** | MongoDB Database | **Required** The name of the MongoDB database. | string |  |  |
| **hosts** | MongoDB Hosts | **Required** A comma-separated list of MongoDB host addresses in `host:port` format. | string |  |  |
| **password** | MongoDB Password | The user password for accessing MongoDB. | string |  |  |
| **persistentTailTracking** | MongoDB Persistent Tail Tracking | Specifies to enable persistent tail tracking, which is a mechanism to keep track of the last consumed data across system restarts. The next time the system is up, the endpoint recovers the cursor from the point where it last stopped consuimg data. This option will only work on capped collections. | boolean | false |  |
| **ssl** | Enable Ssl for Mongodb Connection | whether to enable ssl connection to mongodb. | boolean | true |  |
| **sslValidationEnabled** | Enables Ssl Certificates Validation and Host name checks. | IMPORTANT this should be disabled only in test environment since can pose security issues. | boolean | true |  |
| **tailTrackIncreasingField** | MongoDB Tail Track Increasing Field | The correlation field in the incoming data which is of increasing nature and is used to position the tailing cursor every time it is generated. | string |  |  |
| **username** | MongoDB Username | The username for accessing MongoDB. The username must be present in the MongoDB’s authentication database (`authenticationDatabase`). By default, the MongoDB `authenticationDatabase` is 'admin'. | string |  |  |

## Dependencies

At runtime, the `mongodb-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:mongodb
    
-   camel:jackson
    

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
      uri: "kamelet:mongodb-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## MongoDB Source Kamelet Description

### Authentication

This Kamelet supports MongoDB authentication using username and password credentials. The connection can be configured with or without authentication depending on your MongoDB setup.

### Configuration

The MongoDB Source Kamelet supports the following configurations:

-   **Hosts**: MongoDB server hosts and ports (required)
    
-   **Collection**: MongoDB collection name to query (required)
    
-   **Database**: MongoDB database name (required)
    
-   **Username**: Username for authentication (optional)
    
-   **Password**: Password for authentication (optional)
    
-   **Query**: MongoDB query filter in JSON format
    
-   **Tail**: Enable tailable cursor for real-time changes
    
-   **Create Collection**: Auto-create collection if it doesn’t exist
    

### Output Format

The Kamelet outputs MongoDB documents as JSON objects, preserving the original document structure including ObjectId fields.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:mongodb-source"
      parameters:
        hosts: "mongodb.example.com:27017"
        database: "analytics"
        collection: "events"
        username: "mongouser"
        password: "mongopass"
        query: '{"status": "active"}'
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Tailable Cursor

```yaml
- route:
    from:
      uri: "kamelet:mongodb-source"
      parameters:
        hosts: "mongodb.example.com:27017"
        database: "logs"
        collection: "app_logs"
        username: "mongouser"
        password: "mongopass"
        tail: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Replica Set Example

```yaml
- route:
    from:
      uri: "kamelet:mongodb-source"
      parameters:
        hosts: "mongo1.example.com:27017,mongo2.example.com:27017,mongo3.example.com:27017"
        database: "production"
        collection: "orders"
        username: "mongouser"
        password: "mongopass"
        query: '{"created_at": {"$gte": {"$date": "2023-01-01T00:00:00Z"}}}'
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Query Format

MongoDB queries should be provided in standard MongoDB JSON query format. The kamelet supports complex queries including operators like $gte, $lte, $in, etc.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/mongodb-source.kamelet.yaml)