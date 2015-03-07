====================
Multipart Hypermedia
====================

This document specifies a new multipart media type,
``multipart/hypermedia`` (not registered with the IANA (yet)),
which defines a method of combining
multiple media types at a given resource,
for the purpose of encouraging media types
that are purpose-made to describe hypermedia concepts
without including that data in
the representation of the resource itself.

For example, this allows a resource to use a plain JSON object
to represent the domain-specific data of the model,
while allowing a more specialized type to model
more complex hypermedia concepts, such as forms or links.


---------
The Parts
---------
* meta (optional)
  Metadata about a resource, in the format of HTTP headers.
  The intent is that most HTTP headers should be valid in this part.
  This will hopefully allow
* resource (optional)
  The representation of the resource itself.
  This is what would be shown if this media type were not used.
* actions (optional)
  An analog to HTML forms, this part gives all important details of
  actions that can be taken, and paths to take to other resources.
* links (optional)
  Map link relations to uniform resource identifiers.
* embeds (optional)
  Embedded entities. **Must** be URI addressable.
  **May** be partial representations of the addressed resource.
  It is expected that these will be included only for resources
  linked in another section.
  Embedded entities **may** also be of this media type, recursively.


-------------------
Content Negotiation
-------------------
When specifying the expected content type in HTTP,
parameters for each of the parts may be specified.
The name of the parameter is the same as the part identifier,
and the value should be a valid ``Accepts`` header,
in double quotation marks.

One limitation is that this cannot be done recursively,
because there is no way to quote inner quotation marks.
This means that even if ``embeds`` use this same media type,
the parameters **must not** be used,
because it would break the quoting rules.
