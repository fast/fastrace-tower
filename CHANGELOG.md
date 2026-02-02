# CHANGELOG

All significant changes to this project will be documented in this file.

## Unreleased

## v0.2.0 (2026-02-02)

### Breaking Changes

* `FastraceServerLayer` now requires construction; use `FastraceServerLayer::default()` or `with_span_context_extractor`.

### New Features

* Added a configurable span context extractor; default reads `traceparent` and starts a new trace when missing or invalid.
* Added ability for extractors to return `None` to keep noop spans.

### Improvements

* Updated documentation for the new constructor and extractor behavior.
