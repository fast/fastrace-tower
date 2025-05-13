# fastrace-tower

[![Crates.io](https://img.shields.io/crates/v/fastrace-tower.svg?style=flat-square&logo=rust)](https://crates.io/crates/fastrace-tower)
[![Documentation](https://img.shields.io/docsrs/fastrace-tower?style=flat-square&logo=rust)](https://docs.rs/fastrace-tower/)
[![MSRV 1.80.0](https://img.shields.io/badge/MSRV-1.80.0-green?style=flat-square&logo=rust)](https://www.whatrustisit.com)
[![CI Status](https://img.shields.io/github/actions/workflow/status/fast/fastrace-tower/ci.yml?style=flat-square&logo=github)](https://github.com/fast/fastrace-tower/actions)
[![License](https://img.shields.io/crates/l/fastrace-tower?style=flat-square)](https://github.com/fast/fastrace-tower/blob/main/LICENSE)

`fastrace-tower` is a middleware library that connects [fastrace](https://crates.io/crates/fastrace), a distributed tracing library, with [tower](https://crates.io/crates/tower), modular and reusable components for building robust networking clients and servers. This integration enables seamless trace context propagation across microservice boundaries in applications based on tower.

## What is Context Propagation?

Context propagation is a fundamental concept in distributed tracing that enables the correlation of operations spanning multiple services. When a request moves from one service to another, trace context information needs to be passed along, ensuring that all operations are recorded as part of the same trace.

`fastrace-tower` implements the [W3C Trace Context](https://www.w3.org/TR/trace-context/) standard for propagating trace information between services. This ensures compatibility with other tracing systems that follow the same standard.

## Features

- 🔄 **Automatic Context Propagation**: Automatically inject trace context into outgoing gRPC requests.
- 🌉 **Seamless Integration**: Works seamlessly with the `fastrace` library for complete distributed tracing.
- 📊 **Full Compatibility**: Works with fastrace's collection and reporting capabilities.

## How It Works

1. When a client makes a request, `FastraceClientLayer` detects if there's an active trace and adds a `traceparent` HTTP header with the trace context.
2. When a server receives the request, `FastraceServerLayer` extracts the trace context from the `traceparent` header and creates a new span as a child of the received context.
3. If no trace context is provided, the server creates a new root span.

This process ensures that all operations across services are properly connected in the resulting trace, providing visibility into the entire request lifecycle.

## License

This project is licensed under the [Apache-2.0](./LICENSE) license.
