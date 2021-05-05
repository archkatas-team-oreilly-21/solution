# 2. Chat bot service

Date: 2021-05-04

## Status

Accepted

## Context

We need to improve overall customer experience, reduce the possibility of "wrong consultant shows up" problem and reduce the system load.

## Decision

We will introduce Chat Bot service that would communicate with the knowledge base and ask suggestive questions about the issue.

## Consequences

It would help customers to better identify and describe the problem in the ticket to help system better match the expert.
Experts would have more information about the problem upfront, which helps to reduce requests to the knowledge base and overall time to fix the problem.
For really simple and common problems Chat Bot would guide how to fix those without even expert involvement, if possible.
