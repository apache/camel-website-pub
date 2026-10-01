# Large payloads

Camel can move large files, such as several gigabytes, between components without loading them into memory. This does not happen with every configuration, though: a few defaults and a few route constructs load the whole message body into the heap. This page explains which ones, and how to configure the most common components to stream large payloads.

## Stream caching

[Stream caching](stream-caching.md) is enabled by default, but spooling to disk is **not**. When a message body is a stream, such as an `InputStream` returned by a component, stream caching copies it into a re-readable cache the next time a processor needs the body. Without spooling, that cache is kept in memory, so a stream of several gigabytes ends up in the heap.

For routes that handle large payloads, choose one of the following:

-   Enable spooling, so bodies above the spool threshold (128 KB by default) are cached in a temporary file:
    
    ```properties
    camel.main.streamCachingSpoolEnabled = true
    # a volume with room for the largest payload times the number of concurrent exchanges
    camel.main.streamCachingSpoolDirectory = /data/camel-spool
    ```
    
    The body can then be read many times, for example by redelivery, and the heap stays bounded. The cost is one full copy of the payload to the spool directory. In containers, make sure the spool directory is writable and large enough.
    
-   Disable stream caching for the route, so the stream is passed from component to component as-is:
    
    ```java
    from("sftp:...?streamDownload=true")
        .streamCache("false")
        .to("http:...");
    ```
    
    Nothing is copied, but the body can only be read once. Do not use steps that read the body again, such as redelivery, a `choice` on the body, `multicast`, `wireTap` or `recipientList`.
    

A body that is a file (`java.io.File`, `java.nio.file.Path`, or the file of the [File](../components/4.22.x/file-component.md) component) is not cached, as it can already be read many times. Keeping a large payload as a file is often the cheapest option.

## Route steps that load the whole body

Even when the components stream, the following steps load the whole body into memory:

-   converting the body to a `String` or `byte[]`, for example with `convertBodyTo(String.class)`
    
-   using `${body}` in a [Simple](../components/4.22.x/languages/simple-language.md) expression, including `.log("${body}")`
    
-   unmarshalling the whole body with a data format, such as JSON or XML
    
-   tracing the body with the [Tracer](tracer.md) or the [Backlog Tracer](backlog-tracer.md); the body is converted before it is clipped to the maximum number of characters
    
-   the [Split](../components/4.22.x/eips/split-eip.md) EIP without `streaming()`
    

To process a large file record by record, split it in streaming mode, for example `split(body().tokenize("\n")).streaming()`.

## Components

The following table describes how the most common components handle large payloads, and which options make them stream. When a stream is received, stream caching applies to it as described above.

  
| Component | Receiving (consumer, download) | Sending (producer, upload) |
| --- | --- | --- |
| [File](../components/4.22.x/file-component.md) | The body is the file; it is not read until it is used. | A `File` or `InputStream` body is streamed to the file. With `charset`, the body is converted while it is written. |
| [FTP](../components/4.22.x/ftp-component.md), [SFTP](../components/4.22.x/sftp-component.md), [SMB](../components/4.22.x/smb-component.md) | By default the whole file is loaded into memory. Set `streamDownload=true` to receive an `InputStream`, or `localWorkDirectory` to download to a local file first (the body is then a file). | A `File` or `InputStream` body is streamed. With `charset`, the body is converted while it is uploaded. |
| [SCP](../components/4.22.x/scp-component.md) | Not supported. | The whole body is loaded into memory. |
| [AWS S3](../components/4.22.x/aws2-s3-component.md) | By default (`includeBody=true`) the whole object is loaded into memory. Set `includeBody=false` to receive the object stream, and `autocloseBody=true` to close it when the exchange is done. | A file, or a stream whose length is known (a stream cache, or the `CamelAwsS3ContentLength` header), is uploaded as a stream. Otherwise the body is copied first to find its length: with stream caching and spooling enabled the copy is a temporary file, otherwise it is in memory. Use `multiPartUpload=true` to upload large objects in parts. |
| [Azure Storage Blob](../components/4.22.x/azure-storage-blob-component.md), [Azure Storage Data Lake](../components/4.22.x/azure-storage-datalake-component.md) | The blob is received as a stream. With `fileDir`, the blob is downloaded to a file. | Same as AWS S3. For blobs, the length can also be given with the `CamelAzureStorageBlobUploadSize` header. |
| [Google Storage](../components/4.22.x/google-storage-component.md) | With `includeBody=true` the object is copied into a stream cache (a temporary file when spooling is enabled). With `downloadFileName`, the object is downloaded to a file. | Same as AWS S3. The length can also be given with the `CamelGoogleCloudStorageContentLength` header. |
| [MinIO](../components/4.22.x/minio-component.md), [IBM Cloud Object Storage](../components/4.22.x/ibm-cos-component.md) | MinIO loads the whole object into memory when the body is included. | Same as AWS S3. |
| [HTTP](../components/4.22.x/http-component.md) | The response is copied into a stream cache (a temporary file when spooling is enabled). With `disableStreamCache=true` the producer returns the raw response stream, which the route’s stream caching then handles; disable stream caching on the route to pass it on without any copy. | A `File` or `InputStream` body is streamed. A `Content-Encoding: gzip` request header compresses the whole body in memory. |
| [Platform HTTP](../components/4.22.x/platform-http-component.md) | By default the whole request body is loaded into memory. Multipart file uploads are written to temporary files, and a single uploaded file becomes the body. With `useStreaming=true` the request body is written into a stream cache as it arrives (a temporary file when spooling is enabled), and the route starts once the whole request is received. | A `File` or `InputStream` response body is streamed to the client. |
| [Vert.x HTTP](../components/4.22.x/vertx-http-component.md) | The whole response is loaded into memory. | The whole request body is loaded into memory, unless it is a Vert.x `ReadStream`. |
| [Netty HTTP](../components/4.22.x/netty-http-component.md) | The whole response is loaded into memory, up to `chunkedMaxContentLength` (1 MB by default). With `disableStreamCache=true`, chunked responses are streamed. | With `disableStreamCache=true`, an `InputStream` body is sent chunked. Otherwise it is loaded into memory. |

### Platform HTTP request size limits

The size of an uploaded request is limited by the runtime:

-   Camel Main and Camel JBang: `camel.server.maxBodySize`. When it is not set, the Vert.x default of 10 MB applies. With `useStreaming=true` this limit does not apply, so limit the size of requests in front of Camel if needed.
    
-   Quarkus: `quarkus.http.limits.max-body-size`, and the `quarkus.http.body.*` options for file uploads. See the Quarkus documentation.
    
-   Spring Boot: `spring.servlet.multipart.max-file-size` and `spring.servlet.multipart.max-request-size` for multipart uploads. See the Spring Boot documentation.
    

On Camel Main, Camel JBang and Quarkus, `useStreaming=true` does not accept multipart requests; use a separate endpoint for multipart uploads.

## Examples

### From SFTP to HTTP

Receive the remote file as a stream and send it on without copying it:

```java
from("sftp:host/inbox?username=...&streamDownload=true")
    .streamCache("false")
    .to("http:backend/upload");
```

The HTTP producer sends the stream with chunked transfer encoding. Alternatively, keep stream caching and set `localWorkDirectory` on the SFTP endpoint, so the file is downloaded to disk and the body is a file.

### From Platform HTTP to AWS S3

Multipart uploads are written to temporary files by the HTTP server, and the uploaded file is then sent to S3 from disk:

```java
from("platform-http:/upload?httpMethodRestrict=POST")
    .setHeader(AWS2S3Constants.KEY, header(Exchange.FILE_NAME))
    .to("aws2-s3:my-bucket");
```

Raise the request size limit of the runtime, as described above.

For a raw request body (not multipart), enable spooling and use `useStreaming=true`:

```java
from("platform-http:/upload?httpMethodRestrict=PUT&useStreaming=true")
    .to("aws2-s3:my-bucket?keyName=upload.bin");
```

The request is written to the spool directory while it is received, and S3 uploads it from there with its known length.

### From AWS S3 to SFTP

Receive the object as a stream and upload it without copying it:

```java
from("aws2-s3:my-bucket?includeBody=false&autocloseBody=true")
    .streamCache("false")
    .setHeader(Exchange.FILE_NAME, header(AWS2S3Constants.KEY))
    .to("sftp:host/outbox?username=...");
```

### Downloading a large file over HTTP

```java
from("timer:download?repeatCount=1")
    .streamCache("false")
    .to("http:server/big-file?disableStreamCache=true")
    .to("file:downloads?fileName=big-file");
```