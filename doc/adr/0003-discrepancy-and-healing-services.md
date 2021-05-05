# 3. Discrepancy and Healing services

Date: 2021-05-04

## Status

Accepted

## Context

We need to address ticket loss and inconsistencies.

## Decision

We will introduce Discrepancy service that would look for differences among created, assigned, resolved tickets and report to the Healing service for inconsistencies if any. Healing service would try to resolve the issue. If automatic correction is not possible, manager would be notified.

## Consequences

It would assist managers with any ticket issues, which would result in better ticket handling.