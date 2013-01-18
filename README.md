# JSON/Hypcos – JSON Hypermedia Controls

## Introduction

### Overview

JSON is a popular media type used for building web APIs. While good as a data format, JSON is not a hypermedia type as it lacks means of application flow control (hypermedia controls). Although attempts were made to build a JSON-based hypermedia type (most notably [Hypertext Applicataion Language – HAL][hal]), still JSON implementations aren't on par with more mature XML-based hypermedia types.

JSON hypermedia controls (Hypcos) are not intended to become the missing all-in-one JSON hypermedia type but rather to provide standard building blocks for constructing new and extending existing hypermedia types. JSON hypcos intentionally duplicate (actually combine) some of the existing efforts, overlap or even conflict with each other. API designers are encouraged to cherry-pick and mix JSON hypcos together to define a media type.

### Hypermedia Factor

Mike Amundsen defined a classification of media types based on the level of hypermedia support. [H-Factor][hfactor] identifies 9 values which can either be supported by a media type or not:

1. [LE]: Embedding links
2. [LO]: Outbound links
3. [LT]: Templated queries
4. [LN]: Non-Idempotent updates
5. [LI]: Idempotent updates
6. [CR]: Control data for read requests
7. [CU]: Control data for update requests
8. [CM]: Control data for interface methods
9. [CL]: Control data for links

Hypcos cover all the listed H-Factor values being a valuable foundation for a full-fledged hypermedia type.

## Hypermedia Controls

### Link Value
The simplest possible way to describe a linked resource is to represent its URI as a value of a JSON attribute:

```javascript
"venue": "http://api.example.com/venues/123"
```

The name of the attribute conveys the relation type ([CL] factor) while the URL value represents [LO].

### Link Object
A link object is a more sophisticated representation of a link concept in JSON. Derived from [HAL] links, link objects provide extensibility to links:

```javascript
{
  "href": "http://api.example.com/venues/123"
}
```

In its simplest form the link object only represents the [LO] factor, but its power is in combination with other hypcos.

### Template
Pre-constructed and pre-filled JSON object that the client can alter before sending back to the server. The client alters only the parts it understands, thus template is a way to get hidden fields of HTML forms in JSON. When used in a Link Hypco can provide [LN] H-Factor.

### Descriptor
Embed [JSON Schema][schema] snippets to describe semantics of data.


## Integration
Hypermedia controls defined in this document are standard building blocks which can be reused individually or all at once. Since Hypcos are defined as JSON objects with only optional attributes every JSON media type can be gradually enriched by JSON hypcos to provide required level of application flow control.

## References
1. [Hypertext Application Language][hal]
2. [H Factor][hfactor]
3. [JSON Schema][schema]

[hfactor]: http://amundsen.com/hypermedia/hfactor/
[LE]: http://amundsen.com/hypermedia/hfactor/#le
[LO]: http://amundsen.com/hypermedia/hfactor/#lo
[LT]: http://amundsen.com/hypermedia/hfactor/#lt
[LN]: http://amundsen.com/hypermedia/hfactor/#ln
[LI]: http://amundsen.com/hypermedia/hfactor/#li
[CR]: http://amundsen.com/hypermedia/hfactor/#cr
[CU]: http://amundsen.com/hypermedia/hfactor/#cu
[CM]: http://amundsen.com/hypermedia/hfactor/#cm
[CL]: http://amundsen.com/hypermedia/hfactor/#cl
[hal]: http://stateless.co/hal_specification.html
[schema]: http://json-schema.org/