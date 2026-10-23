# Fiber Middleware

⚠️ This README may be for the latest development version, which may contain unreleased changes. Please ensure you're looking at the README for the latest release version.

Middleware for the [Fiber web server](https://github.com/gofiber/fiber) for use with [deepmap/oapi-codegen](https://github.com/deepmap/oapi-codegen).

## Options

`OapiRequestValidatorWithOptions` accepts an `Options` struct whose `Options`
field is passed through to kin-openapi's `openapi3filter`.

This middleware enables `openapi3filter.Options.KeepValidatedValue` by default,
which keeps the decoded, validated request body on the validated request behind
a `ValidatedValue()` method, so that a handler such as an oapi-codegen strict
server can bind exactly the value that was validated rather than decoding the
body a second time. Set `Options.DiscardValidatedValue` to `true` to turn this
off, for instance to limit memory retention for very large request bodies; it
overrides any `KeepValidatedValue` set in `Options.Options`.

Note that fiber handlers do not receive the validated value yet: this
middleware validates a `net/http` copy of the request converted from the fiber
context, so nothing kept on that copy reaches the handler. The default is set
for consistency with the other oapi-codegen middlewares and for a future change
that exposes the value.

Licensed under the Apache-2.0.
