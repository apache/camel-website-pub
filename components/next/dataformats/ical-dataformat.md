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

The iCal dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **validating** (common) | `false` | `Boolean` | Whether to validate the iCal document. |

## Message Body

The message body at each side of the iCal data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `pojo` (`net.fortuna.ical4j.model.Calendar`) | An ical4j Calendar, such as unmarshal gives. Text is not parsed: unmarshal the iCalendar text first. |
| **Marshal output** | `stream`, as text | The iCalendar text in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as text | An iCalendar (.ics) document, which ical4j reads as UTF-8. |
| **Unmarshal output** | `pojo` (`net.fortuna.ical4j.model.Calendar`) | An ical4j Calendar of the document. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

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