# 1. Service-based approach

Date: 2021-04-27

## Status

Accepted

## Context

We need to migrate the existing monolith system to better architecture.

## Decision

We will go with service-based architecture with a single data store (with additional analytics DB) since its much easier to migrate than to a microservices architecture.

## Consequences

This architecture would perform much better than the existing monolith, would solve the current problems (deployability, testability, scalability, performance issues) and would meet all of the requirements for the system.