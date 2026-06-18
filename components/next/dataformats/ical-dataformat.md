# iCal

**Since Camel 2.12**

The ICal dataformat is used for working with [iCalendar](http://en.wikipedia.org/wiki/ICalendar) messages.

A typical iCalendar message looks like:

_Java-only: example of an iCalendar message format_

```java
BEGIN:VCALENDAR
VERSION:2.0
PRODID:-//Events Calendar//iCal4j 1.0//EN
CALSCALE:GREGORIAN
BEGIN:VEVENT
DTSTAMP:20130324T180000Z
DTSTART:20130401T170000
DTEND:20130401T210000
SUMMARY:Progress Meeting
TZID:America/New_York
UID:00000000
ATTENDEE;ROLE=REQ-PARTICIPANT;CN=Developer 1:mailto:dev1@mycompany.com
ATTENDEE;ROLE=OPT-PARTICIPANT;CN=Developer 2:mailto:dev2@mycompany.com
END:VEVENT
END:VCALENDAR
```

## Options

The iCal dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **validating** (common) | `false` | `Boolean` | Whether to validate. |

## Basic Usage

To unmarshal and marshal the message shown above, your route will look like the following:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:ical-unmarshal")
    .unmarshal("ical")
    .to("mock:unmarshaled")
    .marshal("ical")
    .to("mock:marshaled");
```

```xml
<route>
  <from uri="direct:ical-unmarshal"/>
  <unmarshal><ical/></unmarshal>
  <to uri="mock:unmarshaled"/>
  <marshal><ical/></marshal>
  <to uri="mock:marshaled"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:ical-unmarshal
      steps:
        - unmarshal:
            ical: {}
        - to:
            uri: mock:unmarshaled
        - marshal:
            ical: {}
        - to:
            uri: mock:marshaled
```

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ical</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using ical with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-ical-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.ical.enabled** | Whether to enable auto configuration of the ical data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.ical.validating** | Whether to validate. | false | Boolean |