# Fiber Middleware

⚠️ This README may be for the latest development version, which may contain unreleased changes. Please ensure you're looking at the README for the latest release version.

Middleware for the [Fiber web server](https://github.com/gofiber/fiber) for use with [deepmap/oapi-codegen](https://github.com/deepmap/oapi-codegen).

## Validated request body

The middleware enables kin-openapi's `openapi3filter.Options.KeepValidatedValue` by default. Fiber does not run on `net/http`, so the validator works on a converted copy of the request; after a request body passes validation, the middleware stores the decoded value that was validated in the Fiber context under `ValidatedBodyLocalsKey` (`x-oapi-codegen-validated-body`), readable with `ValidatedBody(c)`. The body bytes seen by the handler (`c.Body()`) are unchanged. oapi-codegen strict servers that support it bind that value instead of decoding the body a second time, so the handler sees exactly what was validated (for example, `encoding/json`'s case-insensitive member matching can no longer make a request validate as one value but bind as another).

To opt out, for instance to limit memory retention for very large request bodies, set `Options.DiscardValidatedValue = true`. This setting overrides `Options.Options.KeepValidatedValue`.

Licensed under the Apache-2.0.
