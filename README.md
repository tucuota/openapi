# TuCuota's OpenAPI Specification

This repository contains [OpenAPI specifications][openapi] for TuCuota's API.

[Changelog](https://github.com/tucuota/openapi/releases/)


Files can be found in the `openapi/` directory:

* `spec1.{json,yaml}:` OpenAPI 3.0 spec matching the public TuCuota API.
* `fixtures1.{json,yaml}`: Test fixtures for resources in spec3. See below for more information.

## Vendor Extensions

The specification ships with a few vendor-specific fields to help represent
information in ways that are difficult in OpenAPI by default.

### `x-polymorphicResources`

Some API responses are "polymorphic" in that they might return multiple types
of resources which is a case that OpenAPI can't handle. In these cases the spec
will reference a "synthetic" resource which is an aggregate of the properties
common to all the possible resources. It will also include the field
`x-polymorphicResources` which references those resources more precisely.

For example:

``` yaml
definitions:
  ...
  external_account_source:
    properties:
      ...
    x-polymorphicResources:
      oneOf:
      - "$ref": "#/definitions/cbu"
      - "$ref": "#/definitions/card"
```

### `x-resourceId` and Fixtures

Resources include `x-resourceId` which is a canonical name for each resource.
It can be used in conjunction with `openapi/fixtures{2,3}.{json,yaml}` to look
up a sample representation (otherwise known as a "fixture") of the resource.

For example:

``` yaml
# spec.yaml
---
definitions:
  ...
  charge:
    ...
    x-resourceId: charge

# fixtures.yaml
---
invoice_line_item:
  ...
```

[openapi]: https://www.openapis.org/